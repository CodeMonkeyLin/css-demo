## 前端基本单位
### px
- px像素（Pixel）。相对长度单位。像素px是相对于显示器屏幕分辨率而言的
### em 
- em(相对长度单位，相对于当前对象内文本的字体尺寸)
### vw vh
-  vw：viewpoint width，视窗宽度，1vw等于视窗宽度的1%。
- vh：viewpoint height，视窗高度，1vh等于视窗高度的1%。
> 与百分比区别，vwvh不包含滚动条
### rem
- rem  相对的HTML根元素字体大小
> 可以结合vw解决移动端自适应，例如640px设计稿设1rem=100px代码如下

```css
html {
      font-size: 15.625vw;
}
```

## 视口

viewport 是指 web 页面上用户的可见区域。

viewport 的大小是和设备相关的，在移动端例如手机上，viewport 的大小是比 PC 端要小的，一般无论手机还是平板，默认的 viewport 大小都是 980px 。
### 手机端配置viewport

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
```
> 配置viewport,rem才能起作用
- width:设置layout viewport  的宽度，为一个正整数，或字符串"width-device"
- initial-scale:设置页面的初始缩放值，为一个数字，可以带小数
- minimum-scale:允许用户的最小缩放值，为一个数字，可以带小数
- maximum-scale:允许用户的最大缩放值，为一个数字，可以带小数
- height:设置layout viewport  的高度，这个属性对我们并不重要，很少使用
- user-scalable:是否允许用户进行缩放，值为"no"或"yes", no 代表不允许，yes代表允许