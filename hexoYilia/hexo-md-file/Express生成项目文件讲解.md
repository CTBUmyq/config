---
title: Express生成项目文件讲解
date: 2017-06-08 09:58:11
reword: true
comments: true
tags:
	- Node.js
	- Express
categories:
	- Node.js
	- Express
keywords: Node.js,Express
description: Express项目生成文件讲解

---
我们使用express生了package.json，它只产生了javascript和route/index.js。模板引擎ejs文件有index.js，此外还有样式表style.css。
### 一、app.js工程的入口
&emsp;分析代码:
1.我们导入了express模块，前面我们通过npm install依赖上了,在这里就可以直接通过require获取。
2.route是一个文件夹形式的本地模块，即./route/index.js，它的功能是伪指定的路径组织返回内容，相对于MVC架构的控制器。
3.通过express.createServer()函数创建一个应用的实例，后面的所有操作都是针对这个实例进行。
4.app.set是Express的参数设置工具，接受一个键(key)和一个值(value)，可以用的参数如下：

|    参数 |描述     | 
| --- | --- |
|   basepath  |基础机制，通常用于res.redirect()跳转   |  
|    views | 视图文件的目录，存放模块文件    |  
|    view engine | 视图模块引擎(推荐使用ejs)    |  
| view options| 全局视图参数对象|
|view cache|启用视图缓存|
|case sensitive routes|路径区分大小写|
|strict routing|严格模式，启用后不会忽略路径末尾的"/"|
|json callback|开启透明的jsonp支持|
5.Express依赖于connect，提供了大量的中间件，可以通过app.use启用。app.connect中启用了五个中间件:
bodyParse:解析客户端请求
router: 项目路径的支持
static： 提供静态文件支持
errorHandler:错误控制器
6.app.get('/',routes.index)，是一个路由控制器，用户访问'/'路径，则routes.index来控制。
### 二、routes/index.js是路由文件，相当于控制器，用于组织展示的内容
&emsp;app.js通过app.get('/',routes.index)将
### 三、我的项目app.js源码
```

/**
 * Module dependencies.
 */
/*引用模块*/
var express = require('express')
  , routes = require('./routes')
  , user = require('./routes/user')
  , http = require('http')
  , util=require('util')
  , path = require('path')
  ,engine=require('./system');
/*实例化express对象*/
var app = express();

/*配置app的参数和启用中间件*/
app.configure(function(){
  app.set('port', process.env.PORT || 3000);
  //告诉我们的页面模版目录
  app.set('views', __dirname + '/views');
  //告诉它我们使用那种模版引擎
  app.set('view engine', 'ejs');
  app.use(express.favicon());
  app.use(express.logger('dev'));
  app.use(express.bodyParser());
  app.use(express.methodOverride());
  app.use(app.router);
  app.use(express.static(path.join(__dirname, 'public')));
});

//配置开发模式
app.configure('development', function(){
  app.use(express.errorHandler());
});
//指定路由控制
app.get('/', routes.index);
app.get('/pcat', routes.pcat);
app.get('/user/:username',function(req,res){
            res.send("user ："+req.params.username);
        });

app.get('/users', user.list);
app.all('/test/:username',function(req,res,next){
	console.log("all methods is call");
	//我们在这里验证用户名是否存在。
	//如果存在直接send或者调用next(new Error('用户已经存在'));
	//如果不存在我们调用next()把控制权交给下一个路由规则
	next();
	res.send('all的路由规则完毕。')
});
 app.get('/test/:username',function(req,res){
     res.send("user："+req.params.username)
})
app.get('/abc',routes.pcat)
//改造ejs引擎中的方法
app.engine('ejs', engine);
//将layout的模版布局模版设置为默认
app.locals._layoutFile='layout'
//片段视图
app.get('/list',function(req,res){
	res.render('list',{
		title:'片段视图',
		items:['marico',1991,'pcat']
	})
});
//视图助手
app.locals({
	inspect:function(obj){
		return util.inspect(obj,true)+"    解析成功";
	}
})
app.get('/view',function(req,res){
	res.locals({
		headers:function(req,res){
			return req.headers;
		}
	})
	res.render('view',{title:"PCAT"});
})
//创建服务并监听端口
http.createServer(app).listen(app.get('port'), function(){
  console.log("Express server listening on port " + app.get('port'));
});
```