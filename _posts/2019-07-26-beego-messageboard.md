---
layout: post
title: "beego-messageboard"
date: 2019-07-26
author: jjnoob
categories:
- 2019-07
tags:
- beego
- golang
---

* content
{:toc}


> 照着别人的代码一点一点的看, 一点一点的敲. 


[参考-wujiangwei](https://studygolang.com/user/wujiangwei/articles)

[参考项目的源码](https://github.com/wujiangweiphp/beegostudy)

[参考-看云](https://www.kancloud.cn/hello123/beego/126086)


# 一. 实现注册模块

1. 准备表
2. 准备模板register.tpl
3. 准备路由router
4. 准备模型models
5. 准备控制器controllers
6. 运行

## (1) 准备表
数据库是`my_blog`, 表名是`user`.

```sql
CREATE TABLE `user` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(50) NOT NULL,
  `password` varchar(50) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8;
```

## (2) 准备模板
表单 + ajax提交数据
> ajax() 方法通过 HTTP 请求加载远程数据。


## (3) 准备路由
路径: `/routers/router.go`

`init`函数体里面添加:
```go
beego.Router("/user/register", &controllers.UserController{},"get:Register")
beego.Router("/user/saveUser", &controllers.UserController{},"post:SaveUser")
```

###  固定路由
固定路由也就是全匹配的路由，如下所示：
```go
beego.Router("/", &controllers.MainController{})
beego.Router("/admin", &admin.UserController{})
beego.Router("/admin/index", &admin.ArticleController{})
beego.Router("/admin/addpkg", &admin.AddController{})
```
如上所示的路由就是我们最常用的路由方式，一个固定的路由，一个控制器，然后根据用户请求方法不同请求控制器中对应的方法，典型的 RESTful 方式。

[看云-自定义方法及RESTful规则](https://www.kancloud.cn/hello123/beego/126122)

## (4) 准备模型
路径: `/models/user.go`

[看云-对象的CRUD操作](https://www.kancloud.cn/hello123/beego/126104)

```go
package models

import (
    "fmt"
    "github.com/astaxie/beego/orm"
    _ "github.com/go-sql-driver/mysql"
)

type User struct {
    Id       int
    Name     string `orm:"size(50)"`
    Password string `orm:"size(50)"`
}

func init() {
    orm.RegisterDriver("mysql", orm.DRMySQL) //设置驱动
    orm.RegisterDataBase("default", "mysql", "root:@/my_blog?charset=utf8", 30)//连接数据库
    orm.RegisterModel(new(User)) //注册模型
}

/**
    添加一条数据
 */
func (user User) SaveOne() (int, error) {
    o := orm.NewOrm()
    if created, id, err := o.ReadOrCreate(&user,"name"); err == nil {
        if created {
            return int(id) , nil
        } else {
            //更新
            user.Id = int(id)
            if num, err := o.Update(&user); err == nil && num > 0 {
                return int(id) , nil
            }
        }
    }
    return 0 , fmt.Errorf("save fail")
}
```

## (5) 准备控制器
路径: `controllers/user.go`

```go
package controllers

import (
    "github.com/astaxie/beego"
    "goblog/models"
)

//所有控制器都需要组合
type UserController struct {
    beego.Controller
}

//如果我们返回的是json类型，我们需要先定义一个结构体
type ResponseJson struct {
    State int
    Message string
    Data int
}


func (c *UserController) Register() {
    c.TplName = "register.tpl"
}

func (c *UserController) SaveUser() {
    user := models.User{}
    user.Name = c.Input().Get("name")
    user.Password = c.Input().Get("password")

    response := ResponseJson{State:0,Message:"ok"}
    if id, err := user.SaveOne(); err != nil {
        response.State = 500
        response.Message = "保存失败，请稍后再试"
    } else {
        response.Data = id
    }
    c.Data["json"] = response
    c.ServeJSON()
}
```

使用json直接在函数里加上：
```go
response := ResponseJson{State:0,Message:"ok"}
c.Data["json"] = response
c.ServeJSON()
```

[看云-更多类型返回细节](https://www.kancloud.cn/hello123/beego/126130)

[看云-获取web参数](https://www.kancloud.cn/hello123/beego/126125)


# 二. 实现登录和退出
登录和退出的流程：

1. 输入用户名、密码传到后台
2. 数据库查询结果是否匹配
3. 匹配成功保存 session 跳转首页
4. 退出登录 删除session 

> 这里用到了beego的三个知识点：`session`, `数据库查询`, `跳转`.

## (1) 设置session
在`app.conf`中开启`session`:
```go
sessionon = true
```

### 设置session
> 变量`c`为控制器中传入的指针对象

```go
c.SetSession("Username","bego")
```

### 获取session
```go
c.GetSession("Username")
```

### 删除session
```go
c.DelSession("Username")
```

[看云-session](https://www.kancloud.cn/hello123/beego/126126)

## (2) 跳转重定向

> beego的跳转在控制器中已经封装好, 直接调用

```go
func (c*MainController) Get() {
    username := c.GetSession("Username")
    if username == nil {
        c.Redirect("/user/login", 302)
        return 
    }
    //other code
}
```

[看云-跳转重定向](https://www.kancloud.cn/hello123/beego/126123)

## (3) 数据库读取
> 使用`orm`的`Read`方法, 需要一个`User`指针, 并使用字段`name`, `password`匹配.

```go
func (user User) GetOne() (int, error) {
    orm.Debug = ture
    o := orm.NewOrm()
    if err := o.Read(&user,"name","password"); err != nil || user.Id <= 0 {
        return 0, errors.New("用户名或密码错误")
    } else {
        return user.Id,nil
    }
}
```
[看云-数据库查询](https://www.kancloud.cn/hello123/beego/126104)

## (4) 访问首页

### 路由
```go
beego.Router("/",&controllers.MainController{})
```

### 模板
> 跳过


### 控制器
```go
func (c *MainController) Get() {
    username := c.GetSession("Username")
    if username == nil {
        c.Redirect("/user/login", 302)
        return
    }
    c.Data["Username"] = username
    c.TplName = "index.tpl"
}
```
## (5) 登录页
### 路由
```go
beego.Router("/user/login", &controllers.UserController{},"get:Login")
beego.Router("/user/sign", &controllers.UserController{}, "post:Sign")
beego.Router("/user/logout", &controllers.UserController{}, "post:Logout")
```

### 模板
> 跳过


### 控制器
```go
func (c.UserController) Login() {
    c.TplName = "login.tpl"
}

func (c *UserController) Sign() {
    user := models.User{}
    user.Name = c.Input().Get("name")
    user.Password = c.Input().Get("password")

    response := ResponseJson{State:0,Message:"ok"}
    if user.Name == "" || user.Password == ""{
        response.State = 500
        response.Message = "用户名或密码不能为空"
    }else {
        if id,err := user.GetOne(); err != nil || id ==0 {
            response.State = 500
            response.Message = err.Error()
        } else {
            c.SetSession("username", user.Name)
        }
    }
    c.Data["json"] = response
    c.ServeJSON()
}

func (c *UserController) Logout() {
    c.DelSession("Username")
    response := ResponseJson{State:0,Message:"ok"}
    c.Data["json"] = response
    c.ServeJSON()
}
```

### 模型
```go
/*
    查询单个用户信息
*/
func (user User) GetOne() (int, error){
    orm.Debug = ture
    o := orm.NewOrm()
    if err := o.Read(&user, "name", "password"); err != nil || user.Id <=0 {
        return 0, errors.New("用户名或密码错误")
    } else {
        return user.Id,nil
    }
}
```

# 四. 留言功能

留言本实现流程:
1. 用户登录, 填写留言
2. 展示留言列表(分页查询和搜索)
3. 实现留言增删改查

## (1) 增加留言表
```sql
CREATE TABLE `leave_message` (
    `id` int(11) unsigned NOT NULL AUTO_INCREMENT,
    `uid` int(11) NOT NULL DEFAULT '0' COMMENT '来自用户表user的id',
    `content` text NOT NULL COMMENT '留言内容',
    `status` tinyint(2) NOT NULL DEFAULT '1' COMMENT '是否展示 0 否 1 是',
    `create_at` datatime NOT NULL COMMENT '创建时间',
    `updata_at` datatime NOT NULL COMMENT '更新时间',
    PRIMARY KEY (`id`),
    KEY `uid` (`uid`) USING BTREE 
) ENGINE = MyISAM AUTO_INCREMENT=1 DEAFAULT CHARSET=UTF8 COMMENT='留言板';
```

> MYSQL中索引的存储类型有两种：BTREE和HASH，具体和表的存储引擎相关, 用BTREE来创建索引，提高查询效率

## (2) 增加路由
> emm, 好像有问题, 没有和源代码对应起来

```go
beego.Router("/msg/", &controllers.MessageController{}, "get:Index")
beego.Router("/msg/list", &controllers.MessageController{}, "get:List")
beego.Router("/msg/addmsg", &controllers.MessageController{}, "post:AddMsg")
beego.Router("/msg/delmsg", &controllers.MessageControllers{}, "post:DelMsg")
```

> 一般查询用`get`, 数据修改用`post

## (3) 增加控制器
```go
type MessageController struct {
    beego.Controller
}

func (c *MessageController) List() {
    msg := models.LeaveMessage{}
    limit,_ := c.GetInt("limit")
    page,_ := c.GetInt("page")
    content := c.Input().Get("content")
    response := ResponseJson{}
    response.Message = "ok"
    response.State = 0
    if messages. err := msg.GetList(limit,page,content) ; err != nil {
        response.Message = err.Error()
        response.State = 500
    } else {
        response.Data = messages
    }
    c.Data["json"] = response
    c.ServeJSON()
}

func (c *MessageController) Index() {
    c.TplName = "message.top"
}

func (c *MessageController) AddMsg() {
    username := c.GetSession("username")
    content := c.Input().Get("content")
    id,_ := c.GetInt("id",0)
    response := ResponseJson{}
    response.Message = "ok"
    response.State = 0
    if content == "" {
        response.Message = "留言内容不能为空"
        response.State = 500
        c.Data["json"] = response
        c.ServeJSON()
        return
    }
    if username == "" || username == nil{
        response.Message = "当前用户尚未登陆, 请先登陆"
        response.State = 501
        c.Data["json"] = response
        c.ServeJSON()
        return 
    }
    msg := models.LeaveMessage{}
    msg.Content = content
    msg.Id = id
    if id,err := msg.SaveMessage(username.(string)); err != nil {
        response.Message = "保存失败, 请稍后再试"
        response.State = 503
    } else {
        response.Data =id
    }
    c.Data["json"] = response
    c.ServeJSON()
    return
}

func (c *MessageController) DelMsg() {
    username := c.GetSession("username")
    id,_ := c.GetInt("id",0);
    response := ResponseJson{}
    response.Message = "ok"
    response.State = 0
    msg := models.LeaveMessage{}
    msg.Id = id
    if username == "" || username == nil{
        response.Message = "当前用户尚未登陆, 请先登录"
        response.State = 501
        c.Data["json"] = response
        c.ServeJSON()
        return 
    }
    if err := msg.DelMsg(username.(string)); err != nil {
        response.Message = "删除失败, 请稍后再试"
        response.State = 503
    }
    c.Data["json"] = response
    c.ServeJSON()
    return
}
```

## (4) 模型
```go
package models

import (
    "errors"
    "github.com/astaxie/beego/orm"
    "log"
    "time"
)

type LeaveMessage struct {
    Id int 
    Uid int
    content string
    Status int
    CreateAt time.Time `orm:"type(datetime)"`
    UpdateAt time.Time `orm:"type(datetime)"`
}

type MsgData struct {
    Id int
    Content string
    Name string
    CreateAt time.Time
}

type MessageList struct {
    Count int
    List []MsgData
}

func init() {
    orm.RegisterModel(new(LeaveMessage))
}

/**
    添加留言
*/

func (msg *LeaveMessage) SaveMessage(username string) (int, error){
    o := orm.NewOrm()
    user := User{Name: username}
    if err := user.GetUserId(); err != nil {
        return 0, err
    }

    msg.Uid = user.Id
    msg.Status = 1
    msg.UpdateAt = time.Now()

    if msg.Id > 0 {
        //需要判断是否是自己的留言
        //这里读到的有可能会覆盖自己的结构, 需要重新开启一个
        msgr := LeaveMessage{Id:msg.Id, Uid:msg.Uid}
        if err := o.Read(&msgr, "uid", "id"); err != nil {
            log.Printf("update user %v error, error info is %v, is not yourself \n", msg,err)
            return 0, errors.New("不能修改别人的留言")
        }
        msg.CreateAt = time.Now()
        if num, err := o.Update(msg, "content","update_at"); num == 0 || err != nil {
            log.Printf("update user %v error, error info is %v \n", msg, err)
            return 0, errors.New("保存失败, 请稍后再试")
        }
    } else {
        if id, err := o.Insert(msg); err != nil || id <= 0{
            log.Printf("insert user %v error, error info is %v \n", msg, err)
            return 0, error.New("保存失败, 请稍后再试")
        }
    }
    return msg.Id, nil
}

/**
    搜索留言 分页
    1. 联表查询记录列表
    2. 筛选符合条件的结果
    3. 加入分页
*/

func (msg LeaveMessage) GetList(limit, page int, content string) (MessageList, error){
    qb, _ := orm.NewQueryBuilder("mysql")
    qb2, _ := orm.NewQueryBuilder("mysql")
    if limit == 0{
        limit = 20
    }
    offset := 0
    if page > 0 {
        offset = (page - 1) * limit
    }
    qb.Select("count(*)"). 
        From("leave_message").
        LeftJoin("user").On("leave_message.uid = user.id")
    if content != "" {
        qb2.Where("content like '%" + content + "%' ")
    }

    qb2.Select("user.name, leave_message.id,leave_message.content,leave_message.create_at").
        Form("leave_message").
        LeftJoin("user").On("leave_message.uid = user.id")
    if content != "" {
        qb2.Where("content like '%" + content + "%' ")
    }
    qb2.OrderBy("leave_message.id desc").Limit(limit).Offset(offset)

    sqlCount := qb.String()
    sqlRows := qb2.String()

    o := orm.NewOrm()
    var messageList MessageList
    var count []int

    o := orm.NewOrm()
    var messageList MesageList
    var count []int
    var msgDatas []MsgData
    if num, err := o.Raw(sqlCount).QueryRows(&count); err != nil || num == 0 {
        return MessageList{}, errors.New("查询失败, 请稍后再试")
    }
    messageList.Count = count[0]
    if num, err := o.Raw(sqlRows).QueryRows(&msgDatas); err != nil || num == 0{
        return MessageList{}, errors.New("查询失败, 请稍后再试")
    }
    messageList.List = msgDatas
    return messageList, nil
}

/**
    删除留言
*/
func (msg *LeaveMessage) DelMsg(username string) error {
    o := orm.NewOrm()
    user := User{Name: username}
    if err := user.GetUserId(); err != nil {
        return err
    }
    msg.Uid = user.Id
    msg.Status = 1
    msg.CreateAt = time.Now()
    msg.UpdateAt = time.Now()

    if msg.Id > 0 {
        //需要判断是否是自己的留言
        if err := o.Read(msg, "uid", "id"); err != nil {
            log.Print("delete user %v error, error info is %v, is not yourself \n", msg, err)
            return errors.New("不能删除别人的留言")
        }
        if num, err := o.Delete(msg, "id"); err != nil || num == 0{
            log.Printf("delete user %v error info is %v, is not yourself \n", msg, err)
            return errors.New("删除失败, 请稍后再试")
        }
        return nil
    } else {
        return errors.New("请选择你要删除的留言")
    }
}
```

## (5) 模板
> 跳过

