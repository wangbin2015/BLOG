---
layout: post
title: 迷惑人的this call apply
description: "迷惑人的this call apply"
modified: 2015-07-30
category: JavaScript
tags: [JavaScript]
---

　　因个人知识有限，若发现文章中错误，欢迎发邮件与我进行讨论，邮箱：wangbin2014@hotmail.com，同时，欢迎关注[我的github账号](https://github.com/wangbin2015)     
　　今天的博文封面于2015年5月3日拍摄于大连历史博物馆，她今年8月去美国留学，祝一路顺风。           　　        

***

　　可能，每一个初学前端的弱鸡都会纠结于arguments、this、call、apply的用法，而我并不纠结，我只是抓狂。慢慢地梳理这几个知识点，其实也是可以理解的，本文部分案例摘选于《JS高级程序设计》。

### 一、 一切皆因Function而起

　　JavaScript中函数很有意思，每个函数都是Function的实例，与其他引用类型一样有自己的属性和方法。迷惑众人许久的arguments、this、call、apply、bind都是从哪来又扮演什么作用呢？ 
      
### 二、arguments和this      

　　函数执行时自动添加arguments和this两个特殊对象，arguments是一个类数组对象（并不是数组），包含传入函数的所有参数，而this引用的是函数执行的环境对象。        
　　arguments有一个名叫callee的属性，该属性是一个指针，指向拥有这个arguments对象的函数本体，可用它解耦实现递归调用。          
　　下面是一个阶乘函数       
   
    function factorial(num){
        if(num<=1){
            return 1;
        }else{
            return num*factorial(num-1)
        }
    }           
    
    function factorial(num){
        if(num<=1){
            return 1;
        }else{
            return num*arguments.callee(num-1)
        }
    }         

　　与其他语言大相径庭的是，JavaScript的this总是指向一个对象，而具体指向哪个对象是在运行时基于函数的执行环境动态绑定了，说起来有些拗口。在实际应用中，this的指向分为以下4种：      

* 作为方法的调用     
* 作为普通函数调用     
* 构造器调用      
* call、apply调用     

**1、作为对象方法的调用**            
　　当函数作为对象的方法被调用时，this指向该对象：   
       
    var obj={
        a:1,
        getA:function(){
            alert(this===obj);//true
            alert(this.a);    //1
        }
    }
    obj.getA();
    
**2、作为普通函数调用**           
　　当函数不作为对象的属性被调用时，也就是常说的普通函数的调用，此时this指向全局对象。在浏览器的JavaScript中，全局对象是window对象。
     
    window.name='cat';
    var myObject={
        name:'dog',
        getName:function(){
            return this.name;
        }
    }
    var getName=myObject.getName;
    alert(getName());//cat
 
**3、构造器调用**         
　　构造器的外表跟普通函数一模一样，它们的区别在于调用方式。当用new操作符调用函数时，该函数总会返回一个对象，通常情况下，构造器里面的this就指向返回的这个对象。
         
    var a=function(){
        this.name='dog';
    }
    var b=new a;
    alert(b.name);//dog
    
**4、call、apply调用**       
　　跟作为普通函数调用相比，用Function.prototype.call和Function.prototype.apply可以动态地改变函数的this。   
 
    var a={
        name:'dog',
        getName:function(){
            return this.name;
        }
    }
    var b={
        name:'cat';
    }
    alert(a.getName());
    alert(a.getName.call(b));
    
　　具体call和apply怎样区别，会在下面进行叙述。

### 三、call和apply     

　　call 和 apply 都是为了改变某个函数运行时的 context 即上下文而存在的，换句话说，就是为了改变函数体内部 this 的指向。因为 JavaScript 的函数存在「定义时上下文」和「运行时上下文」以及「上下文是可以改变的」这样的概念。
二者的作用完全一样，只是接受参数的方式不太一样。例如，有一个函数 func1 定义如下：

    var func=function(arg1, arg2){};
    
　　就可以通过 func1.call(this, arg1, arg2); 或者 func1.apply(this, [arg1, arg2]); 来调用。其中 this 是你想指定的上下文，它可以是任何一个 JavaScript 对象(JavaScript 中一切皆对象)。
call必须把参数逐个列举出来，而 apply 另一个参数可以是数组也可以是arguments对象。

    function sum(num1,num2){
        return num1+num2;
    }
    function callSum1(num1,num2){
        return sum.apply(this,[num1,num2])
    }
    function callSum2(num1,num2){
        return sum.apply(this,arguments)
    }
    alert(callSum1(1,2));
    alert(callSum2(1,2));
            
    function sum(num1,num2){
        return num1+num2;
    }
     function callSum(num1,num2){
        return sum.call(this,num1,num2)
    }
     alert(callSum2(1,2));
     
　　至于使用call()还是apply()，完全取决于你采用哪种给函数传递参数的方式最方便。如果你打算传入arguments对象或者包含函数中先接收到的也是一个数组，那么使用apply()肯定更方便。否则，选择call()更合适。在不给函数传递参数的情况下，使用哪种方法都无所谓。         
**1、使用call()和apply()借用其他函数的方法**  
         
    function cat(){}
    cat.prototype={
        food:"fish",
        say: function(){
            alert("I love "+this.food);
        }
    }
    var blackCat = new cat;
    blackCat.say();
    
　　但是如果我们有一个对象whiteDog = {food:"bone"},我们不想对它重新定义say方法，那么我们可以通过call或apply用blackCat的say方法：blackCat.say.call(whiteDog);
所以，可以看出call和apply是为了动态改变this而出现的，当一个object没有某个方法，但是其他的有，我们可以借助call或apply用其它对象的方法来操作。用的比较多的，通过document.getElementsByTagName选择的dom 节点是一种类似array的array。它不能应用Array下的push,pop等方法。我们可以通过：

    var domNodes = Array.prototype.slice.call(document.getElementsByTagName("*"));
    
　　这样domNodes就可以应用Array下的所有方法了。      
**2、使用call()和apply()扩充函数作用域**     

    window.color='red';
    var o={color:blue};
    function sayColor(){
        alert(this.color);
    }
    sayColor();//red
    sayColor.call(this);//red
    sayColor.call(window);//red
    sayColor.call(o);//blue      
            
　　使用call()或是apply()来扩充作用域最大的好处，就是对象不需要与方法有任何耦合关系。
    
    
