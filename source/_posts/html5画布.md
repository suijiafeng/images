title: html5+css3画布
author: suijiafeng
tags: []
categories: []
date: 2016-10-13 01:26:00
---
[TOC]

# 目录

## 画布的概念

canvas原意为帆布，在html页面中用于展示绘图效果,所有画图的过程使用js来实现。

## 画布的用途

1. 绘图
2. 数据可视化(重点)
3. 动画与游戏
4. banner 广告等。

## 画布的兼容性

- canvas 的兼容性非常强, 只要支持该标签的, 基本功能都一样, 因此不用考虑兼容性问题.
- canvas 本身就是一张画布. 整个绘图过程是由 JavaScript 来完成， canvas 对象提供了各种绘图用的 api.
- 如果浏览器不支持 canvas 标签, 那么就会将其解释为 div 标签. 因此常常在 canvas 中嵌入文本, 以提示用户浏览器的能力.

## 怎么使用

1. 拿到画布
2. 创建画图工具
3. 移动画笔
4. 颜色填充 、描边

### 绘制基本形状的api的总结

- 创建画图工具 canvas.getContext("2d")

- 移动画笔 context.moveTo(x, y)

- 画一条直线 context.lineTo(x, y)

- 描边 context.stroke();

- 填充 context.fill();

- 设置描边颜色 context.strokeStyle = "red";

- 设置填充颜色 context.fillStyle = "green";

- 创建一张新的玻璃纸 context.beginPath();

- 闭合路径context.closePath();

- 我们可以这样想象：ctx在画图时，并不是直接把线画到画布上，而是画在玻璃纸上

  - 当执行stroke时，把玻璃纸向画布上做一次印刷，再执行一次stoke会再印刷一次
  - 为了避免重复印刷，我们的做法是， 再拿一张新的玻璃纸，在新的玻璃纸上绘制
  - 再次执行stroke就会使用新玻璃纸上的图形
  - beginPath， 创建一个新玻璃纸的过程， 叫做, 路径就是玻璃纸上的图形元素；
  - closePath，会自动将lineTo的最后一个点和最近的moveTo点连接起来，


- stroke()和fill()
    - stroke是描边，（素描）
    - fill是填充，（上色）
    - fill会自动执行一次closePath
- strokeStyle和fillStyle
    - strokeStyle，描边颜色
    - fillStyle, 填充颜色

### 路径

- 路径就是画布上的线条
- 路径是有方向的

### 非零填充原则

- 路径围成的区域内部，任意一点拉一条射线，找到所有与其相交的路径。顺时针为1， 逆时针为-1. 将所有的相交的路径的值相加。 如果不等于零则对该区域进行填充


## 画矩形

​	**只有矩形、圆形的有api  ,三角形这些需要自己绘制**

1. 用线条连成一个矩形；

   最笨，最麻烦

2. 使用ctx.rect()方法；

   绘制出一个矩形的路径， 适应性是最强的,使用最为广泛

   ```html
   // context.rect(x, y, w, h); 分别代表 x y 坐标 ，矩形 宽 高
   // context.rect(100, 100, 200, 150);
   // context.strokeStyle = 'red';
   // context.fillStyle = 'green';
   // context.fill();
   ```

3. 使用ctx.fillRect()方法。第三种方法会重新开启一个新的路径

   创建一个填充的矩形，只能填充不能描边

          // context.fillRect(100, 100, 200, 150);

4. 使用 ctx.strokeRect()方法。

   绘制一个描边的矩形，只能描边不能填充

       context.strokeRect(100, 100, 200, 150);
   注意方法 3 、4 在调用方法的时候就已经描边或者填充了，所以如果想要修改他的边框或者填充色，那就得在它之前修改。

、、、、、、、、、、---

webPack 项目打包软件--简书/gitup上有资料，可学习下

、、、、、、、、、、--

## 画圆形的方式

**语法：**	arc(x, y, radius, startAngle, endAngle, anticlockwise)`, 画一个以（x,y）为圆心的以`radius`为半径的圆弧（圆），从`startAngle`开始到`endAngle`结束，按照`anticlockwise`给定的方向（默认为顺时针，其值默认false,通常省去不写。）来生成。

**anticlockwise**  :意思，是否是逆时针，为 true 表示逆时针 ，为false 表示顺时针

**注意，**在canvas中，所有的角度都必须转成弧度才能使用，角度转弧度公式`angle/180*Math.PI`



[TOC]

# 目录

## 线条

### 线条粗细

```javascript
<script>
  var canvas = document.getElementById('canvas');
  var context = canvas.getContext('2d');
  //设置线条粗细
  context.lineWidth = 10;
  context.moveTo(300, 200);
  context.lineTo(300, 400);
</script>
```

### 虚线的设置(不是很明白)

```javascript
<script>
        var canvas = document.getElementById("canvas");
        var context = canvas.getContext("2d");

        //先画一条垂直的参考线
        context.moveTo(100, 0);
        context.lineTo(100, 400);
        context.stroke();

        //画虚线
        context.beginPath();
        context.lineWidth = 10;
        //设置虚线的样式，循环使用数组里面的长度，虚线的间隔也占一个长度
        context.setLineDash([5, 10，15]);
        //画虚线的一个偏移
        context.lineDashOffset = 15;
        context.moveTo(100, 100);
        context.lineTo(500, 100);

        context.stroke();
    </script>
```

### 线条的头部 **lineCap**：


默认值：butt   round使用的是最多的。

**JavaScript 语法**：context.lineCap="butt|round|square"; 

## 阴影

```javascript
<script>
    var canvas = document.getElementById("canvas");
    var context = canvas.getContext("2d");
    //画一个矩形
    context.fillStyle = "yellowgreen";
    //阴影的水平偏移
    context.shadowOffsetX = 15;
    //阴影的垂直偏移
    context.shadowOffsetY = 15;
    //阴影的颜色
    context.shadowColor = "red";
    //阴影的模糊程度，值越大，越模糊
    context.shadowBlur = 15;
    context.fillRect(100, 100, 200, 200);
</script>
```

## 渐变

### 线性渐变

```javascript
   <script>
        var canvas = document.getElementById("canvas");
        var context = canvas.getContext("2d");
        //1. 创建一个渐变的对象
        var gradient = context.createLinearGradient(100, 100, 300, 100);
        //2. 添加渐变色
        gradient.addColorStop(0, "red");
        gradient.addColorStop(0.5, "yellow");
        gradient.addColorStop(1, "green");
        //3. 将渐变对象设为画笔颜色
        context.fillStyle = gradient;
        //4. 填充操作
        context.fillRect(100, 100, 300, 200);
   </script>
```

### 径向渐变

> HTML5 canvas createRadialGradient() 方法
>
>   `context.createRadialGradient(*x0*,*y0*,*r0*,*x1*,*y1*,*r1*);`
>
> x0 y0 r0 为开始圆的圆心 和半径  x1 y1 r1 为结束圆的圆心 和半径

```javascript
<script>
        var canvas = document.getElementById('canvas');
        var context = canvas.getContext('2d');
        //1  创建径向渐变对象
        var gradient = context.createRadialGradient(200, 200, 80, 200, 200, 100);
        // 2 给gradient渐变对象添加颜色 
        // 在那个区间会渐变呢？？在两个圆之间的部分 也就是 半径 100-80之间发生渐变
        // red -green 占一半  green- yellow 占一半
        gradient.addColorStop(0, 'red');
        gradient.addColorStop(0.5, 'green');
        gradient.addColorStop(1, 'yellow');
        // 3 将gradient对象设为填充色
        context.fillStyle = gradient;
        // 4 画圆形
        context.arc(200, 200, 100, 0, Math.PI * 2);
        context.fill();
    </script>
```

### 步骤

1. 创建渐变对象
2. 给渐变对象添加渐变色
3. 将渐变对象设为填充颜色/描边颜色
4. 画图并填充（描边）

## addColorStop(offset, color)

offset代表百分比，它是一个小数。color该点的颜色

## 绘制文本

1. fillText(text, x, y [, maxWidth]) 在指定的(x,y)位置填充指定的文本，绘制的最大宽度是可选的.

   这种比较常见，出来的字体比较好看。

2. strokeText(text, x, y [, maxWidth]) 在指定的(x,y)位置绘制文本边框，绘制的最大宽度是可选的.

   镂空效果。

## 文本对齐选项

1. font = value: 当前我们用来绘制文本的样式. 这个字符串使用和 CSS font 属性相同的语法. 默认的字体是 10px sans-serif。

2. textAlign = value: 文本对齐选项. 可选的值包括：start, end, left, right or center. 默认值是 start。

   ​

   ![img](file:///E:/%E7%94%BB%E5%B8%83/%E8%B5%84%E6%96%99/%E5%A4%87%E8%AF%BE%E7%AC%94%E8%AE%B0/chapters/img/2017-08-04-15-59-02.png)

   **文字水平对齐**

   ```javascript
    <script>
           var canvas = document.getElementById('canvas');
           var context = canvas.getContext('2d');
           //绘制参考线
           context.moveTo(300, 0);
           context.lineTo(300, 400);
           context.stroke();
           //文字部分
           //设置字体样式
           context.font = '20px 微软雅黑';
           // 设置文本对齐方式
           context.textAlign = 'center';
           //设置文字内容
           context.fillText("text", 300, 100);
           // --------------------
           // 设置文本对齐方式
           context.textAlign = 'left';
           //设置文字内容
           context.fillText("text", 300, 150);
           // --------------------
           // 设置文本对齐方式
           context.textAlign = 'right';
           //设置文字内容
           context.fillText("text", 300, 200);
           //---------设置镂空文字  strokeText 只会对文字进行描边，而不会对文字部分进行颜色的填充。
           // 设置文本对齐方式
           context.textAlign = 'right';
           //设置文字内容 
           context.strokeText("text", 300, 300);
       </script>
   ```


1. textBaseline = value: 基线对齐选项. 可选的值包括：top, hanging, middle, alphabetic, ideographic, bottom。默认值是 alphabetic。

   ​

   ![![img](file:///E:/%E7%94%BB%E5%B8%83/%E8%B5%84%E6%96%99/%E5%A4%87%E8%AF%BE%E7%AC%94%E8%AE%B0/chapters/img/2017-08-04-15-41-00.png?lastModify=1507340203)](file:///E:/%E7%94%BB%E5%B8%83/%E8%B5%84%E6%96%99/%E5%A4%87%E8%AF%BE%E7%AC%94%E8%AE%B0/chapters/img/2017-08-04-15-41-00.png)

   **文字垂直对齐**

   ```javascript
    <script>
           var canvas = document.getElementById('canvas');
           var context = canvas.getContext('2d');
           // 1 绘制一条参考线,方便观看
           context.moveTo(0, 200);
           context.lineTo(600, 200);
           context.stroke();
           // 2 文本设置
           context.font = '20px 微软雅黑';
           // context.textAlign='start | left | center | right |end';
           // context.textBaseline='top | hanging | middle | alphabetic | ideographic | bottom';
           //--------默认状态下
           context.fillText('你妹的', 200, 200);
           //--------bottom 对齐
           context.textBaseline = 'bottom';
           context.fillText('你妹的', 300, 200);
           //--------center 对齐
           context.textBaseline = 'center';
           context.fillText('你妹的', 400, 200);
           //--------top 对齐
           context.textBaseline = 'top';
           context.fillText('你妹的', 500, 200);
       </script>
   ```


1. direction = value: 文本方向。可能的值包括：ltr, rtl, inherit。默认值是 inherit。

## 计算文本大小

+ measureText()： 返回一个 TextMetrics对象的宽度、所在像素

  语法：*context*.measureText(*text*).width;`  text 为要测量的文本

  ```javascript
  <script>
          var canvas = document.getElementById('canvas');
          var context = canvas.getContext('2d');
          var txt = "你妹sdfsdfsdfsdfsdfsdfsdfsdsdf的"
          context.font = '30px 微软雅黑';
          context.fillText(txt, 300, 200); //这一句代码会把参数设置上，并印刷，所以要改变参数，必须在此之前，如果在这之后修改，不会印刷，不会表现出来，看不到效果。
          context.font = '100px 微软雅黑';
          // |context.textAlign='start | left | center | right |end';
          var width = context.measureText(txt).width;
          console.log(width);
      </script>
     
  ```

## 图片绘制

### 1.原样

+ 三参模式：

  **写法：** img :图像 x,y 放置的位置

  ```javascript
  *context*.drawImage(*img*,*x*,*y*);
  ```

### 2.缩放

+ 五参模式

  **写法：** img :图像 x,y 放置的位置  *width*,*height* 图片的宽 高

  ```	javascript
  *context*.drawImage(*img*,*x*,*y*,*width*,*height*);
  ```

### 3.裁剪

+ 九参模式

  **写法：**img 图像 sx,sy 开始裁剪的坐标位置,swidth,sheight：裁剪图像的宽 高；x,y :裁剪的图像放置的位置，weidth,height,裁剪图像要显示的宽 高。

  ```javascript
  *context*.drawImage(*img*,*sx*,*sy*,*swidth*,*sheight*,*x*,*y*,*width*,*height*);
  ```

  注意的地方：w3c上有说很多参数可以省略，亲测发现，不能省略。

### md中代码的输入

英文状态下输入  ```  加 回车,右下角可以选择语言类型。





## 前天的知识复习

### 更丰富的样式
* 线条
  * 画线或者是描边时的样式设置
  * lineWith
  * lineCap = "round" //butt， square
  * setLineDash([5， 10, 15])
  * lineDashOffset //设置虚线的偏移
* 阴影
  * shadowOffsetX
  * shadowOffsetY
  * shadowColor
  * shadowBlur //模糊程度
* 渐变
  1. 创建渐变对象
    * context.creatLinearGradient(x0, y0, x1, y1)
    * var gra= context.createRadialGradient(x0, y0, r0,  x1, y1, r1)
  2. 添加渐变色
    * addColorStop(offset, color)
  3. 将渐变对象设为填充色或者是描边色
    * context.fillStyle = gra
  4. 绘制图形并填充

### 文字的绘制
* 设置文字的字体 context.font = "20px 微软雅黑"
* 画描边文字 strokeText("text", x, y)
* 填充文字fillText("text", x, y)
* 水平对齐 textAlign = "left" //right, center, 看线在文字哪一边，就是什么对齐
* 垂直对齐 textBaseline = "top" //bottom, middle

### 图片绘制
* 三参模式 drawImage(image, x, y) //原大小显示
* 五参模式 drawImage(image, x, y, width, height) //缩放显示
* 九参模式 draImage(image, x0, y0, width0, height0, x1, y1, width1, height1) //x0, y0, width0, height0从原始图片从哪一个点开始裁剪，多大。后面的四个参数是在画布上的什么位置粘贴

### 例子
* 移动的小人
* 键盘控制小人移动

### 变形和动画
* 缩放
	* scale(x, y)
* 平移
	* translate(x, y)
* 旋转
	* rotate(raidan) //整个坐标系，围绕坐标原点旋转
* 动画实现原理
	* 当我们以足够快的速度逐帧播放图片时，会超出人眼的识别的极限，让人错以为整个过程是连续
	* setInterval(function(){}, 16.7);
	* var animation =  window.reqeustAnimationFrame(方法名）
		* 递归调用
		* 性能比较好，可以自动的适应游览器的刷新频率
	* window.cancelAnimationFrame(animation) 结束动画

原始状态
save(原始状态)
	//平移和旋转坐标系
	save（平移和反方向旋转90度的状）
	restore()
	save（平移和反方向旋转90度的状）
	restore()
	save（平移和反方向旋转90度的状）
	restore()
restore（）
	
	



















