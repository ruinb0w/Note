```html
<canvas id="canvas" width="800" height="600"></canvas>
<script>
    let canvas = docuemtn.getElementById("canvas");
    const ctx = canvas.getContext();
    // 也可以修改canvas的宽高
    canvas.width = 1280;
    canvas.height = 720;
</script>
```

画

* 移动画笔 `ctx.moveTo(x,y)`

* 画线 `ctx.lineTo(x,y)`

* 画矩形 `ctx.rect(起始X, 起始Y, 宽, 高)`

* 闭合线条路径 `closePath()`

* 圆 `ctx.arc(x,y, startAngle, endAngle, counterClockWise)`

  > 注意angle要使用弧度

清除

* `clearRect(x,y, width, height)`

样式

* 描线样式 `ctx.strokeStyle=样式`

* 填充样式 `ctx.fillStyle=样式`

* 线条粗细 `ctx.lineWidth()`

* 字体 `ctx.font="italic small-caps bold 12px arial"`

* 基线 `ctx.textBaseline = "bottom|"`

* 水平对齐 `ctx.textAlign= "left|center|right"`

  > 与x坐标对齐

渲染

*  渲染线条 `ctx.stroke()`
* 填充内容 `ctx.fill()`
* 绘制并渲染文字 `ctx.strokeText("内容",x,y)`
* 绘制并渲染填充文字 `ctx.fillText("内容",x,y)`

矩形

* 画并渲染 `ctx.strokeRect()`
* 画并渲染 `ctx.fillRect()`

阴影

* 阴影颜色 `ctx.shadowColor=颜色值`
* blur `ctx.shadowBlur = 像素值`
* X轴偏移 `ctx.shadowOffsetX = 像素值`
* Y轴偏移 `ctx.shadowOffsetY = 像素值`

图片

```js
// 创建图片实例
let img = new Image();
img.src = '图片路径';
img.onload = function(){
    ctx.drawImage(img, x, y)
    //获取图片宽高
    let width = img.width;
    let height = img.height;
}
```

* 绘制并渲染图片 `ctx.drawImage(img, x, y[,width, height])`
* 裁剪并绘制并渲染图片 `ctx.drawImage(img, 截取图片的x, 截取图片的y, 画布x, 画布y[,width,height])`

### canvas状态

canvas是基于状态的, 例如

```js
ctx.strokStyle='green';
ctx.moveTo(0,0)
ctx.lineTo(100, 0)
ctx.stroke()

ctx.strokStyle='black';
ctx.moveTo(100,0)
ctx.lineTo(200, 0)
ctx.stroke()
```

这样你会得到两条黑色的线, 如果你想一绿一黑, 需要使用 `ctx.begingPath()` ,开启一个新的状态

```
ctx.strokStyle='green';
ctx.moveTo(0,0)
ctx.lineTo(100, 0)
ctx.stroke()

ctx.begingPath()
ctx.strokStyle='black';
ctx.moveTo(100,0)
ctx.lineTo(200, 0)
ctx.stroke()
```

> 默认开启新状态会继承旧状态 

开启新状态 `ctx.begingPath()`

### 公式

Math.PI/180 对应1度的弧度

$Math.sin(角度 \times Math.PI/180)=\frac{对边}{斜边}$

$Math.cos(角度 \times Math.PI/180) = \frac{邻边}{斜边}$
