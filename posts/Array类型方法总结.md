---
layout: post
title: Array类型方法总结
description: "Array类型方法总结"
modified: 2015-08-01
category: JavaScript
tags: [JavaScript]
---

　　因个人知识有限，若发现文章中错误，欢迎发邮件与我进行讨论，邮箱：wangbin2014@hotmail.com，同时，欢迎关注[我的github账号](https://github.com/wangbin2015)                  　　        

***
　　现在时间22：57，更新完这篇文章应该也是下半夜了。谷歌到的关于数组的博文比较有限，或许是这知识点比较简单。简单数了一下，大概有23种方法，
不整理一下真的很难记住，也不会应用到实际当中。       
　　本文完全基于《高级程序设计第三版》。    

### 一、检测数组方法（2）   
  
* instanceof操作符：一个全局作用域下，确定某个对象是不是数组
* Array.isArray()方法：多个作用域下，确定某个对象是不是数组        
    
### 二、转换方法（4） 

* toString()方法：返回由数组中每个值的字符串形式拼接成的一个以逗号分隔的传统字符串
* toLocalString()方法：返回由数组中每个值的字符串形式拼接成的一个以逗号分隔的本地环境字符串
* valueOf()方法：其操作与 Array.toString 和 Array.join 方法相同
* join()方法：接收一个作分隔符的字符串，返回包含所有数组项的字符串
    
### 三、栈方法（2）  

* push()方法：接收任意数量的参数，把它们逐个添加到数组末尾，返回修改后数组的长度
* pop()方法：从数组末尾移除最后一项，减少数组的length值，然后返回移除的项

### 四、队列方法（2）  

* shift()方法：移除数组中的第一个项并返回该项，同时将数组长度减一    
**结合shift()和push()方法，可以实现在列表末端添加项，从列表前端移除项**
* unshift()方法：在数组前端添加任意个项并返回新数组的长度     
**结合unshift()和pop()方法，可以实现在列表前端添加项，从列表末端移除项**

### 五、重排序方法（2）

* sort()方法：默认情况下，该方法会调用每个数组项的toString()转型方法，然后比较得到的字符串，按升序排列
    
**最佳方案：sort()方法接收一个比较函数作为参数**

    function compare(a,b){
        if(a<b){
            return -1;
        }else if(a>b){
            return 1;
        }else{
            return 0;
        }
    }
    var values=[0,1,5,10,15]
    values.sort(compare);
    alert(values);       
         
对于数值类型或者其valueOf()方法会返回数值类型的对象类型，可以使用一个更简单的比较函数。

    function compare(a,b){
        return a-b;
    }
    
* reverse()方法：反转数组顺序

### 六、操作方法（3）  

* concat()方法：
* slice()方法：
* splice()z方法：

### 七、位置方法（2）  

* indexOf()方法：
* lastIndexOf()方法：

### 八、迭代方法（5）  

* every()方法
* filter()方法
* forEach()方法
* map()方法
* some()方法

### 九、归并方法（2）  
 
* reduce()方法：
* reduceRight()方法：   
