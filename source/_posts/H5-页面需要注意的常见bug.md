---
title: H5 页面需要注意的常见bug
date: 2018-05-08 14:53:58
tags: H5
---

## 场景一：页面弹出遮盖层或者弹窗的时候，上下滑动页面，页面底部的内容依旧可以滚动。

解决方法：

```javascript
// 禁止页面滑动
document.addEventListener('touchmove', function(event) {
    //判断条件,条件成立才阻止背景页面滚动,其他情况不会再影响到页面滚动
    if(slideFlag != 0){
        event.preventDefault();
    }
})
```

## 场景二：input输入框注意要限制空格输入

解决方法：

```javascript
// String.prototype.trim
var a = ' 123 abc '
a.trim()
```

## 场景三：发送ajax请求的时候要考虑无网络的情况

解决方法：

```javascript
// 异步接口在无网络时的提示：
.catch(err = {
  toast('网络不给力, 请稍后再试！');
})
```

## 场景四：英文输入法在input输入框输入英文的时候会出现自动校正的行为

解决方法：
在input输入框修改autocorrect属性为off：autocorrect="off"

## 场景五：安卓部分手机focus输入框的时候，页面不会将输入框定位到窗口的中间位置导致手机键盘遮挡输入框的情况

解决方法：

```javascript
$('input').focus(function(){
  var element = document.getElementById('');
  var time = setTimeout(function(){
  element.scrollIntoView();
  },100); // 设定延时执行的原因是因为如果不加延时安卓手机在input框未聚焦的时候长按input框的不会出现粘贴按钮
  })
```

## 场景六：遮盖层的属性设置为position:fixed;height:100%;width:100%的时候，当页面resize时有些浏览器可能能会出现蒙层上方未遮盖的情况

解决方法：
遮盖层的高度设定更大一些，比如：height: 300%;top:-30%;

## 场景七：在手机号输入框input添加属性type="tel"，虽然手机会弹出数字输入框，但是依旧可以输入部分特殊符号

解决方法：
对此类input输入框附加限制只能输入数字处理

## 场景八：设置了遮盖层出现的时候无法上下滑动页面，但是在ios系统里双击页面某个位置系统会自动实现上下滑动的效果

解决方法：
禁止遮盖层的所有点击事件

## 场景九：在有input输入框的场景下若执行toast会在手机键盘消失前出现，会导致页面resize的时候toast的位置发生变化

解决方法：添加500毫秒左右的延时

```javascript
var time = setTimeout(function(){
toast('网络不给力, 请稍后再试！');
},500);
```
