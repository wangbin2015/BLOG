---
layout: post
title: JavaScript兼容总结
description: "JavaScript兼容总结"
modified: 2015-08-27
category: JavaScript
tags: [JavaScript]
---

　　因个人知识有限，若发现文章中错误，欢迎发邮件与我进行讨论，邮箱：wangbin2014@hotmail.com，同时，欢迎关注[我的github账号](https://github.com/wangbin2015)     
　　今天的博文封面于2015年5月3日拍摄于大连历史博物馆，她今年8月去美国留学，祝一路顺风。           　　        

***
####1、document.formName.item("itemName") 问题
*说明：*IE下,可以使用`document.formName.item("itemName")`或`document.formName.elements["elementName"]`
Firefox下，只能使用`document.formName.elements["elementName"]`        
*解决方法：*统一使用`document.formName.elements["elementName"]`

