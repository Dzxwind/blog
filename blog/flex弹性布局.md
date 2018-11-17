# CSS技巧：Flex弹性布局
在项目开发过程中，我们经常会遇到一些关于布局方面的问题。  
一个好的布局能够让你在接下来的开发过程中事半功倍，甚至可以连带将响应式一并解决。  
***
## 引入
比如说我们希望实现这样子的布局  
![布局1](../src/assets/images/Flex/layout1.jpg)
假设，我们的html代码是这样的：
```
<div class="box father">
  <div class="box_i son"></div>
  <div class="box_i son"></div>
  <div class="box_i son"></div>
</div>
```
在这里，我设定了.father和.son的公共样式：  
其中，父级盒子使用了灰色背景色，子级盒子使用了绿色为背景色，为方便看出边框，使用深绿色作为边框。实际布局我将使用.box和.box_i来实现
```
.father {
    width: 800px;
    height: 200px;
    background-color: #eeeeee;
    margin: 0 auto;
}

.son {
  height: 100%;
  background: #42b983;
  border: 1px solid #148351;
  width: 25%;
}
```
传统的css布局大多都是这样子的：
```
.box{
  float:left;
  overflow:hidden;  //此处也可以给.box增加一个after伪元素来进行clearfix的操作
}

.box_i:nth-child(2){
  margin: 0 12.5%;
}
```
> 什么是clearfix?  
clearfix是常用的一种清除浮动的方式，当父元素是标准级，子元素是浮动级时，父元素会因为子元素的浮动而失去高度。我们常用的做法是给父元素overflow:hidden或者使用clearfix。  
```
// 比如在上面的例子中，我们如果不使用overflow:hidden，就可以这么写:  
.box::after {
  content: "";
  display: block;
  height: 0;
  clear: both;
  visibility: hidden;
}
```
```
// 如果你使用的是scss你甚至可以将这个实用的方法编写成一个mixin(混合器)
@mixin clearfix {
  &::after {
    content: "";
    display: block;
    height: 0;
    clear: both;
    visibility: hidden;
  }
}
// 实际使用
.box{
  @include clearfix;
}
```
话题扯回来。。。你可以看到，使用传统布局时，有一下几个问题
* 我们必须要知道父元素和子元素的宽度才可以做到这种布局。但是很多情况下，我们是得不到这个宽度的。
* 使用float时，必须要做清除浮动，否则很有可能对后面的布局造成影响。
* 如果这个布局需要改进成响应式，很有可能需要用到@media的媒体查询。

## flex布局
那么接下来，我们该请出我们的重量级嘉宾登场了！！！