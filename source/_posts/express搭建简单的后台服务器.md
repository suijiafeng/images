title: express搭建后台服务器
author: suijiafeng
tags: []
categories: []
date: 2018-06-08 00:58:00
---

在实际开发的项目的过程中，有时候需要数据Api接口，但是，又因为种种原因，后端人员迟迟不能提供api接口。这个时候，[mockjs](http://mockjs.com/ "mockjs")可以模拟各种随机数据。但是对于像我这样懒的小伙伴，我想给你推荐一个更好，更方便的express搭建服务端框架，废话少说，跟着下面的步骤，就可以轻松搭建一个属于自己的模拟本地服务器。

#### 安装Express 应用生成器 ####

此时，默认你已经安装了[nodejs](https://nodejs.org/en/)


####  运行这个命令装一下Express 应用生成器。 ####

    npm install express-generator -g

#### 然后创建一个应用，并安装依赖。 ####

     express myapp
     cd myapp
     npm install

这时候，myapp文件夹里的文件结构如下：
    
     //myapp

    ├── app.js
    ├── bin
    │   └── www
    ├── package.json
    ├── public
    │   ├── images
    │   ├── javascripts
    │   └── stylesheets
    │   └── style.css
    ├── routes
    │   ├── index.js
    │   └── users.js
    └── views
    ├── error.jade
    ├── index.jade
    └── layout.jade


将你想要模拟服务器引用的文件放在pubilc里面，
例如：`public/myJSON.json`
最后，还有配置一个跨域名的访问的权限，

        `// app.js
        var app = express();
        app.all('*', function(req, res, next) {
        res.header("Access-Control-Allow-Origin", "*");  //这里的“*”，指的是来访者白名单。
        res.header("Access-Control-Allow-Headers", "X-Requested-With");
        res.header("Access-Control-Allow-Methods","PUT,POST,GET,DELETE,OPTIONS");
        res.header("X-Powered-By",' 3.2.1')
        res.header("Content-Type", "application/json;charset=utf-8");
        next();
        });`
    
#### 启动express服务器 ####

    npm start

然后在浏览器中打开 http://localhost:3000/myJson.json,
就能模拟跨域服务器文件访问了。