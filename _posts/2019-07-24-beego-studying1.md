> 慢慢积累吧.

[项目代码](https://github.com/beego/samples/tree/master/todo)


#  strconv.ParseInt
golang strconv.ParseInt 是将字符串转换为数字的函数.
```go 
func ParseInt(s string, base int, bitSize int) (i int64, err error)
```
1. 参数1 数字的字符串形式
2. 参数2 数字字符串的进制 比如二进制 八进制 十进制 十六进制
3. 参数3 返回结果的bit大小 也就是int8 int16 int32 int64

# `/controllers/default.go`:
```go
// 包声明
package controllers

// 引入包
import (
	"github.com/astaxie/beego"
)

// 声明结构体
type MainController struct {
	beego.Controller
}


func (this *MainController) Get() {
	// TplName 就是需要渲染的模板的名称
	this.TplName = "index.html"

	// 调用渲染方法
	this.Render()
}
```

# `controllers/task.go`:
```go
// 声明包
package controllers

// 引入包
import (
	"encoding/json"
	"strconv"

	"github.com/astaxie/beego"
	"github.com/beego/samples/todo/models"
)

// 声明结构体
type TaskController struct {
	beego.Controller
}

// Example:
//
//   req: GET /task/
//   res: 200 {"Tasks": [
//          {"ID": 1, "Title": "Learn Go", "Done": false},
//          {"ID": 2, "Title": "Buy bread", "Done": true}
//        ]}
func (this *TaskController) ListTasks() {
	//匿名结构体, 将后者数据传入前者
	//对于"Tasks []*models.Task"的理解: *model.Task指针作为[]的存储对象, 变量名为Tasks
	res := struct{ Tasks []*models.Task }{models.DefaultTaskList.All()}

	//json是一种轻量级的数据交换格式
	this.Data["json"] = res

	//通过把要输出的数据放到Data["json"]中，然后调用ServeJSON()进行渲染，就可以把数据进行JSON序列化输出。
	this.ServeJSON()
}

// Examples:
//
//   req: POST /task/ {"Title": ""}
//   res: 400 empty title
//
//   req: POST /task/ {"Title": "Buy bread"}
//   res: 200
func (this *TaskController) NewTask() {
	req := struct{ Title string }{}
	//Json Unmarshal：将json字符串解码到相应的数据结构
	if err := json.Unmarshal(this.Ctx.Input.RequestBody, &req); err != nil {
		//400 Bad Request
		this.Ctx.Output.SetStatus(400)
		this.Ctx.Output.Body([]byte("empty title"))
		return
	}
	t, err := models.NewTask(req.Title)
	if err != nil {
		this.Ctx.Output.SetStatus(400)
		this.Ctx.Output.Body([]byte(err.Error()))
		return
	}
	models.DefaultTaskList.Save(t)
}

// Examples:
//
//   req: GET /task/1
//   res: 200 {"ID": 1, "Title": "Buy bread", "Done": true}
//
//   req: GET /task/42
//   res: 404 task not found
func (this *TaskController) GetTask() {
	//param类型是key/value型的结构, :id就是key.
	id := this.Ctx.Input.Param(":id")
	//info用于golang日志的输出
	beego.Info("Task is ", id)
	//strconv字符串跟int之间的转换类型
	//strconv.ParseInt转换成int型
	intid, _ := strconv.ParseInt(id, 10, 64)
	t, ok := models.DefaultTaskList.Find(intid)
	beego.Info("Found", ok)
	if !ok {
		this.Ctx.Output.SetStatus(404)
		this.Ctx.Output.Body([]byte("task not found"))
		return
	}
	this.Data["json"] = t
	this.ServeJSON()
}

// Example:
//
//   req: PUT /task/1 {"ID": 1, "Title": "Learn Go", "Done": true}
//   res: 200
//
//   req: PUT /task/2 {"ID": 2, "Title": "Learn Go", "Done": true}
//   res: 400 inconsistent task IDs
func (this *TaskController) UpdateTask() {
	id := this.Ctx.Input.Param(":id")
	beego.Info("Task is ", id)
	intid, _ := strconv.ParseInt(id, 10, 64)
	var t models.Task
	//Json Unmarshal：将json字符串解码到相应的数据结构
	if err := json.Unmarshal(this.Ctx.Input.RequestBody, &t); err != nil {
		this.Ctx.Output.SetStatus(400)
		this.Ctx.Output.Body([]byte(err.Error()))
		return
	}
	if t.ID != intid {
		this.Ctx.Output.SetStatus(400)
		this.Ctx.Output.Body([]byte("inconsistent task IDs"))
		return
	}
	if _, ok := models.DefaultTaskList.Find(intid); !ok {
		this.Ctx.Output.SetStatus(400)
		this.Ctx.Output.Body([]byte("task not found"))
		return
	}
	models.DefaultTaskList.Save(&t)
}
```
