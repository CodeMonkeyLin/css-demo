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

## 前端响应式图像设计
### 像素密度的选择：srcset属性
>根据DPR识别

```html
<img srcset="./img/img.png,
    ./img/img1.jpg 3x,
    ./img/img2.jpg 2x" src="./img/img.png"> 
```
上面代码中，srcset属性给出了三个图像 URL，适应三种不同的像素密度。

图像 URL 后面的像素密度描述符，格式是像素密度倍数 + 字母x。1x表示单倍像素密度，可以省略。浏览器根据当前设备的像素密度，选择需要加载的图像。

如果srcset属性都不满足条件，那么就加载src属性指定的默认图像。

### srcset 和 sizes
>根据屏幕DPR*屏幕宽度

```html
 <img srcset="./img/elva-fairy-320w.jpg 320w,
    ./img/elva-fairy-480w.jpg 480w,
    ./img/elva-fairy-640w.jpg 640w,
    ./img/elva-fairy-800w.jpg 800w" src="./img/img1.jpg" sizes="(max-width: 320px) 280px,
    (max-width: 480px) 440px,
    (max-width: 640px) 640px,
    800px">
```
有了这些属性，浏览器会：

- 查看设备宽度
- 检查sizes列表中哪个媒体条件是第一个为真
- 查看给予该媒体查询的槽大小
- 加载srcset列表中引用的最接近所选的槽大小的图像
> 如果支持浏览器以视窗宽度为480px来加载页面，那么(max-width: 480px)的媒体条件为真，因此440px的槽会被选择，所以elva-fairy-480w.jpg将加载，因为它的的固定宽度（480w）最接近于440px。800px的照片大小为128KB而480px版本仅有63KB大小—节省了65KB。现在想象一下，如果这是一个有很多图片的页面。使用这种技术会节省移动端用户的大量带宽。
>> 在 HTML 文件中的 head 标签里， 需设置 
```html
<meta name="viewport" content="width=device-width">
```

### picture标签，source标签
```html 
<picture>
    <source srcset="./img/img.png,
                ./img/img@2x.png 2x" media="(min-width: 990px)">
    <source srcset="./img/img1.jpg,
                ./img/img2.jpg 2x" media="(min-width: 750px)">
    <img srcset="./img/elva-800w.JPG,
                ./img/elva-800w.JPG 2x" alt="Shopify Merchant, Corrine Anestopoulos">
</picture>
```
media进行媒体查询，图片后面的+x根据设备DPR识别

### 参考文章
https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images
http://www.ruanyifeng.com/blog/2019/06/responsive-images.html

## @supports
在不支持某些特定css的浏览器下实现渐进增强式设计早期解决方案采取使用[Modernizr](https://modernizr.com),现在可以使用@supports进行更优处理
### 语法规则
```css
@supports <条件规则> {
  /* 特殊样式规则 */
}
```
>一个支持条件是由一个或者多个由不同的逻辑操作符组成的表达式声明组合而成的.使用小括号可以调整这些表达式之间的运算优先级

### 基本操作
```css
@supports (display: grid) {
    .selector {
        background: yellow;

    }
}
```
>检测是否支持指定的CSS属性

### 布尔操作

#### not
```css
@supports (display:flex) {
    .selector {
        float: left;
    }
}	
```
>检测是否不支持指定的CSS属性

#### and
```css
@supports (display: table-cell) and (display: list-item) {
    .selector {
        display: block;
    }
}
```
>检测多个CSS属性支持情况

#### or
```css
@supports ((perspective: 10px) or (-moz-perspective: 10px) or (-webkit-perspective: 10px) or (-ms-perspective: 10px) or (-o-perspective: 10px)) {
    .selector {
        background: yellow;
    }
}
```
>允许我们在条件中列出多个属性：值对，只要一个为true，就会应用块中的样式。相关用例属于具有前缀的属性。
### 参考文章
https://developer.mozilla.org/zh-CN/docs/Web/CSS/@supports