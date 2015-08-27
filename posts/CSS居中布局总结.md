---
layout: post
title: CSS居中布局总结
description: "CSS居中布局总结"
modified: 2015-07-29
category: CSS
tags: [CSS,布局]
---

### 水平居中

#### 方法一：inline-block+text-align
    
    <div class="parent">
      <div class="child">Demo</div>
    </div>
    
    <style>
      .child {
        display: inline-block;
      }
      .parent {
        text-align: center;
      }
    </style>
    
- 优点：兼容性佳（甚至可以兼容 IE 6 和 IE 7）      

#### 方法二：table+margin

    <div class="parent">
      <div class="child">Demo</div>
    </div>
    
    <style>
      .child {
        display: table;
        margin: 0 auto;
      }
    </style>

- 优点：无需设置父元素样式 （支持 IE 8 及其以上版本）

#### 方法三：absolute+transform

    <div class="parent">
      <div class="child">Demo</div>
    </div>
    
    <style>
      .parent {
        position: relative;
      }
      .child {
        position: absolute;
        left: 50%;
        transform: translateX(-50%);
      }
    </style>

- 优点：绝对定位脱离文档流，不会对后续元素的布局造成影响         
- 缺点：transform 为 CSS3 属性，有兼容性问题

#### 方法四：flex+justify-content

<div class="parent">
  <div class="child">Demo</div>
</div>

<style>
  .parent {
    display: flex;
    justify-content: center;
  }

  /* 或者下面的方法，可以达到一样的效果 */

  .parent {
    display: flex;
  }
  .child {
    margin: 0 auto;
  }
</style>

- 优点：只需设置父节点属性，无需设置子元素         
- 缺点：有兼容性问题

***

### 垂直居中

#### 方法一：table-cell + vertical-align

      <div class="parent">
        <div class="child">Demo</div>
      </div>
      
      <style>
        .parent {
          display: table-cell;
          vertical-align: middle;
        }
      </style>

- 优点：兼容性好（支持 IE 8，一下版本需要调整页面结构至 table）

#### 方法二：absolute + transform

      <div class="parent">
        <div class="child">Demo</div>
      </div>
      
      <style>
        .parent {
          position: relative;
        }
        .child {
          position: absolute;
          top: 50%;
          transform: translateY(-50%);
        }
      </style>

- 优点：绝对定位脱离文档流，不会对后续元素的布局造成影响          
- 缺点：transform 为 CSS3 属性，有兼容性问题

#### 方法三：flex + align-items

      <div class="parent">
        <div class="child">Demo</div>
      </div>
      
      <style>
        .parent {
          display: flex;
          align-items: center;
        }
      </style>

- 优点：只需设置父节点属性，无需设置子元素        
- 缺点：有兼容性问题

***

### 水平垂直居中

#### 方法一：inline-block + text-align + table-cell + vertical-align

      <div class="parent">
        <div class="child">Demo</div>
      </div>
      
      <style>
        .parent {
          text-align: center;
          display: table-cell;
          vertical-align: middle;
        }
        .child {
          display: inline-block;
        }
      </style>

#### 方法二：absolute + transform

      <div class="parent">
        <div class="child">Demo</div>
      </div>
      
      <style>
        .parent {
          position: relative;
        }
        .child {
          position: absolute;
          left: 50%;
          top: 50%;
          transform: translate(-50%, -50%);
        }
      </style>

#### 方法三：flex + justify-content + align-items

      <div class="parent">
        <div class="child">Demo</div>
      </div>
      
      <style>
        .parent {
          display: flex;
          justify-content: center;
          align-items: center;
        }
      </style>
