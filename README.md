# 移动端旅游评论推荐网站
这是一个比较完整的移动端练习，素材又是从网上扒拉下来的（单纯用来学习^_^）。

## to do
首先一鼓作气把效果全部用自己的思路实现一遍，然后反复去优化代码。
现在(09.16)第一步马上要结束了，还剩下两个页面切换和一个图片滚动的函数，加油！

## 时间轴
### 09.15-16
完成了静态页面的布局以及页面切换的js。    

## 开发笔记
### 坑
- 先看这段代码:
css部分:    
```css
.mask {
    transition:1s;
}
```
```js
addClass(oMask,"pageShow");
oMask.style.opacity=1;  
```
我设置了mask模块的转换完成时间为1s，js部分中pageShow的作用是把原来的display:none转换成display:block,目的是先把这个模块显示出来，然后再让它完成一个1s之内从opacity为0到opacity为1的转变。    
然而结果并没有如我所愿，而是很简单粗暴地直接显示出来了，没有淡入的那个过程，查了一下资料，自己现在理解的原因是： 
>当display在none和block之间转换的时候，需要时间去渲染，这段代码里，在设置了display:block之后立刻设置了opacity:1,这时浏览器还没把模块渲染出来，就读取了opacity＝1的设定，然后在渲染出来那一刻它就是不透明的了，这个转换就体现不出来了。    

因此我们需要给它留出渲染的时间，等渲染结束了，再去设置opacity，这时候transition就是起作用的了:    
```
addClass(oMask,"pageShow");
setTimeout(function(){
    oMask.style.opacity=1;  
},14);
````
至于这个时间为啥选14，因为在网上查到各浏览器的最小延迟时间都在10-15微秒之间，我就取了个14，这里主要是想取一个尽可能小的时间延迟，就算是这么小的时间延迟，也已经够浏览器渲染出这个模块了。（亲测）
