---
layout: post
title: javascript常用函数
description: "javascript常用函数"
modified: 2015-08-26
category: javascript
tags: [javascript]
---

#### 事件绑定与移除的兼容写法
```javascript
		var EventUtil={
			addHandler:function(element,type,handler){
				if(element.addEventListener){
					element.addEventListener(type,handler,false);
				}else if(element.attachEvent){
					element.attachEvent('on'+type,handler)
				}else{
					element['on'+type]=handler;
				}
			},
			removeHandler:function(element,type,handler){
				if(element.removeEventListener){
					element.removeEventListener(type,handler,false);
				}else if(element.detachEvent){
					element.detachEvent('on'+type,handler)
				}else{
					element['on'+type]=null;
				}
			}
		}
```
#### 封装Ajax
```javascript
		function ajax(url, options) {
			if (window.XMLHttpRequest) {
				xhr = new XMLHttpRequest;
			} else {
				xhr = new ActiveXObject('Microsoft.XMLHTTP');
			}
			xhr.open('GET', url);
			xhr.send();
			xhr.onreadystatechange = function() {
				if (xhr.readyState == 4) {
					if (xhr.status == 200) {
						options.onsuccess(xhr);
					}
				}
			}
		}
```
#### 封装Cookie
```javascript
		var CookieUtil = {
        set: function(name, value, expires) {
            var cookie = encodeURIComponent(name) + '=' + encodeURIComponent(value);
            var oDate = new Date;
            oDate.setDate(oDate.getDate() + expires);
            if (expires) {
                cookie += '; expires' + '=' + oDate;
            }
            document.cookie = cookie;
        },
        get: function() {
            var cookie = {};
            var all = document.cookie;
            if (all == '') {
                return cookie;
            };
            var list = all.split('; ')
            for (var i = 0; i < list.length; i++) {
                var item = list[i].split('=');
                if (decodeURIComponent(item[0]) == arguments[0]) {
                    return decodeURIComponent(item[1]);
                };
            };
        },
        remove: function(name, value, expires) {
            this.set(name, '', new Date(0));
        }
    }
```
