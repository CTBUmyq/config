---
title: Node.js小爬虫
date: 2017-06-05 14:48:00
comments: true
layout: post
reword: true
tags:
	- Node.js
	- Node.js小爬虫
categories:
	- Node.js
keywords: Node.js，Node.js小爬虫

---

### 一、视频地址
慕课网 http://www.imooc.com/video/7965
### 二、直接上源码
<!--more-->
```
/** * http小爬虫 
* @author 牟一全
* @version 1.0 
*/ 
/** 
* 获取http模块 
*/ 
var http = require('http'); 
/** 
* 获取cheerio模块 
*/ 
var cheerio = require('./node_modules/cheerio'); 
/** 
* 解析的目标网页 
*/ 
var url = 'http://www.imooc.com/learn/348'; 
/**
* 
* 将爬取到的网页内容进行过滤调整 
* @param {string} html 
* @returns {{chapterTitle:string,videos:[{title:string,time:string,id:string}]}} 返回过滤到的对象 */ 
function filterChapters(html) { 
	// cheerio加载html 
	var $ = cheerio.load(html); 
	var chapters = $('.chapter'); 
	var courseData = []; 
	var chapter, Title, videos, chapterData; 
	var videos, videoTitle, id; 
	chapters.each(function (value) { 
	chapter = $(this); 
	/** nodeType返回值说明 
	* 1-ELEMENT 
	* 2-ATTRIBUTE 
	* 3-TEXT 
	* 4-CDATA 
	* 5-ENTITY REFERENCE 
	* 6-ENTITY 
	* 7-PI (processing instruction) 
	* 8-COMMENT 
	* 9-DOCUMENT 
	* 10-DOCUMENT TYPE 
	* 11-DOCUMENT FRAGMENT 
	* 12-NOTATION */ 
	// 过滤不提取子类中的text 
	Title = chapter.find('strong').contents().filter(function () { 
		return this.nodeType == 3; 
	}).text().trim(); 
	chapterData = { 
		"chapterTitle": Title, 
		"videos": [] 
	} 
	videos = chapter.find('.video').children('li'); 
	videos.each(function (value) { 
		video = $(this).find('.J-media-item'); 
		
		// 这个title包含了video的title和这个video的时间,两者用换行符分割 
		videoTitles = video.contents().filter(function () { 
			return this.nodeType == 3; 
		}).text().trim().split('\n'); 
		
	id = video.attr('href').split('video/')[1]; 
	
	chapterData.videos.push({ 
		"title": videoTitles[0].trim(), 
		"time": videoTitles[1].trim(), 
		"id": id 
		}); 
	}); 
	courseData.push(chapterData); 
	}); 
	return courseData; 
} 
/** 
* 打印课程信息 
* @param {{chapterTitle:string,videos:[{title:string,time:string,id:string}]}} courseData 课程信息 
*/ 
function printCoursrInfo(courseData) { 
	var courseMessage = ''; 
	courseData.forEach(function (value, index) { 
		courseMessage += value.chapterTitle + '\n'; 
		value.videos.forEach(function (value, index) { 
			courseMessage += '[' + value.id + '] ' + value.title + ' time:' + value.time + '\n'; 
		}); 
		courseMessage += '\n'; 
	}); 
	console.log(courseMessage); 
} 
http.get(url, function (res) { 
	var html = ''; 
	
	res.on('data', function (data) { 
		html += data; 
	}); 
	
	res.on('end', function () { 
		var courseData = filterChapters(html); 
		printCoursrInfo(courseData); 
	}); 
}).on('error', function () { console.log('课程爬取失败!!!!'); });

```
### 三、什么是cheerio
相当于html的jquery，但是服务的是服务端，就不是前端了
### 四、说明
只能爬取静态页面的资源，比如ajax动态渲染是爬取不到的
### 五、体会
在each循环内部反复的声明变量会使内存没有必要的损耗,更好的做法是延长变量的生命周期,在函数的顶部先定义,然后每次改变它们的值,由于这些变量本身的类型还是一致的,职责单一,在V8的速度上也会更快，最好还是在上一级申明变量，避免重复声明。