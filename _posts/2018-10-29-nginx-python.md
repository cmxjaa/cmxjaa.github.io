---
layout: post
title: "在Ubuntu虚拟机上使用Nginx部署Flask应用"
date: 2018-10-29
author: jjnoob
categories:
- 2018-10
tags:
- nginx
---

> ### 环境为ubuntu18.04虚拟机

# **一、前提条件**

首先，我们需要PIP与virtualenv：
```bash
sudo apt-get install python-setuptools
sudo easy_install pip   // 也可以通过其他方式安装
sudo pip install virtualenv
```
安装Nginx和uwsgi:
```bash
sudo apt-get install nginx
sudo /etc/init.d/nginx start
```
```bash
sudo pip install uwsgi
```
#### 通过添加源的方式在debian9上安装nginx：(以下可忽略，直接跳到 二、)
参考[Nginx中文文档](https://nginx.org/en/linux_packages.html)

清理残余的旧版本
```bash
sudo apt-get remove nginx nginx-common nginx-full
```
安装nginx PGP签名文件
```bash
wget http://nginx.org/keys/nginx_signing.key
sudo apt-key add nginx_signing.key
```
使用sudo编辑/etc/apt/source.list文件,在文件末追加以下
```bash
deb http://nginx.org/packages/mainline/debian/ stretch nginx
deb-src http://nginx.org/packages/mainline/debian/ stretch nginx
```
更新软件源并安装nginx
```bash
sudo apt-get update
sudo apt-get install nginx
sudo nginx -v
```
# **二、示例应用步骤1（尚未配置nginx）**

将托管的应用是经典的“Hello, world!”。这个应用只有一个页面。将所有应用相关的文件存放在/var/www/demoapp文件夹中。下面创建这个文件夹并在其中初始化一个虚拟环境：

```bash
sudo mkdir /var/www
sudo mkdir /var/www/demoapp
```

由于我们使用root权限创建了这个文件夹，它目前归root用户所有，让我们更改它的所有权给你登录的用户
```bash
sudo chown -R linge /var/www/demoapp/
```
创建并激活一个虚拟环境，在其中安装Flask：
```bash
cd /var/www/demoapp
virtualenv venv
. venv/bin/activate
pip install flask
```
使用下面的代码创建hello.py文件：
```python
from flask import Flask
app = Flask(__name__)
 
@app.route("/")
def hello():
    return "Hello World!"
 
if __name__ == "__main__":
    app.run(host='0.0.0.0', port=8080)
```
执行刚创建的脚本：
```bash
python hello.py
```
通过浏览器访问服务器的8080端口,可以看到页面上出现了hello world !

![img](/screenshots/nginxflaskpython01.png)

注意：因为80端口已被Nginx使用，这里我使用8080端口

现在应用是由Flask内置的web服务托管的，对于开发和调试这确实是个不错的工具，但不推荐在生产环境中使用。此时就需要nginx.


# **二、示例应用步骤2（配置nginx）**

首先删除掉Nginx的默认配置文件：
```bash
sudo rm /etc/nginx/sites-enabled/default
```
创建一个我们应用使用的新配置文件/var/www/demoapp/demoapp_nginx.conf：
```nginx
server {
    listen      80;
    server_name localhost;
    charset     utf-8;
    client_max_body_size 75M;
 
    location / { try_files $uri @yourapplication; }
    location @yourapplication {
        include uwsgi_params;
        uwsgi_pass unix:/var/www/demoapp/demoapp_uwsgi.sock;
    }
}
```
将刚建立的配置文件使用符号链接到Nginx配置文件文件夹中，重启Nginx：
```bash
sudo ln -s /var/www/demoapp/demoapp_nginx.conf /etc/nginx/conf.d/
sudo /etc/init.d/nginx restart
```
访问服务器的公共ip地址，你会看到一个错误:502 Bad Gateway

这个错误是正常的，它代表Nginx已经使用了我们新创建的配置文件，但在链接到我们的Python应用网关uWSGI时遇到了问题。到uWSGI的链接在Nginx配置文件的第10行定义：
```bash
uwsgi_pass unix:/var/www/demoapp/demoapp_uwsgi.sock;
```
这代表Nginx和uWSGI之间的链接是通过一个socket文件，这个文件位于/var/www/demoapp/demoapp_uwsgi.sock。因为我们还没有配置uWSGI，所以这个文件还不存在，因此Nginx返回“bad gateway”错误，让我们马上修正它吧。

### 配置uWSGI
创建一个新的uWSGI配置文件/var/www/demoapp/demoapp_uwsgi.ini：
```
[uwsgi]
#application's base folder
base = /var/www/demoapp
 
#python module to import
app = hello
module = %(app)
 
home = %(base)/venv
pythonpath = %(base)
 
#socket file's location
socket = /var/www/demoapp/%n.sock
 
#permissions for the socket file
chmod-socket    = 666
 
#the variable that holds a flask application inside the module imported at line #6
callable = app
 
#location of log files
logto = /var/log/uwsgi/%n.log
```
创建一个新文件夹存放uWSGI日志，更改文件夹的所有权：
```bash
sudo mkdir -p /var/log/uwsgi
sudo chown -R ubuntu:ubuntu /var/log/uwsgi
```
执行uWSGI，用新创建的配置文件作为参数：
```
uwsgi --ini /var/www/demoapp/demoapp_uwsgi.ini
```

![img](/screenshots/nginxflaskpython02.png)

接下来访问你的服务器，现在Nginx可以连接到uWSGI进程了,可以看到页面上出现了hello world! 

![img](/screenshots/nginxflaskpython03.png)

我们现在基本完成了，唯一剩下的事情是配置uWSGI在后台运行，这是uWSGI Emperor的职责。

### uWSGI Emperor
uWSGI Emperor 负责读取配置文件并且生成uWSGI进程来执行它们。创建一个初始配置来运行emperor:   /etc/init/uwsgi.conf：
```
description "uWSGI"
start on runlevel [2345]
stop on runlevel [06]
respawn

env UWSGI=/usr/local/bin/uwsgi
env LOGTO=/var/log/uwsgi/emperor.log

exec $UWSGI --master --emperor /etc/uwsgi/vassals --die-on-term --uid www-data --gid www-data --logto $LOGTO
```
最后一行运行uWSGI守护进程并让它到/etc/uwsgi/vassals文件夹查找配置文件。创建这个文件夹，在其中建立一个到链到我们刚创建配置文件的符号链接。
```bash
sudo mkdir /etc/uwsgi
```
同时，最后一行说明用来运行守护进程的用户是www-data。为简单起见，将这个用户设置成应用和日志文件夹的所有者。
```bash
sudo chown -R www-data:www-data /var/www/demoapp/
sudo chown -R www-data:www-data /var/log/uwsgi/
```
注意：我们先前安装的Nginx版本使用“www-data”这个用户来运行Nginx，其他Nginx版本的可能使用“Nginx”这个替代用户。

由于Nginx和uWSGI都由同一个用户运行，我们可以在uWSGI配置中添加一个安全提升项。打开uWSGI配置文件，将chmod-socket值由666更改为644：
```
...
#permissions for the socket file
chmod-socket    = 644
```
现在我们可以运行uWSGI了：
```
uwsgi --ini /var/www/demoapp/demoapp_uwsgi.ini
```
最后，Nginx和uWSGI被配置成启动后立即对外提供我们的应用服务。


> ## END

Thanks!

http://python.jobbole.com/84286/

https://www.cnblogs.com/geons/p/install_nginx.html

https://nginx.org/en/linux_packages.html
