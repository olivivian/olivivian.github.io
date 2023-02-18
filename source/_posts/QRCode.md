
---
title: 前端生成二维码和条形码
date: 2021-10-19
tags: 插件
categories: 前端
img: https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/hexo/9.jpg
summary: 前端插件QRCode的使用实战
---

# 前端插件QRCode.js生成二维码

> [QRCode.js 文档](http://code.ciaoca.com/javascript/qrcode/)<br/>[ npm package 地址](https://www.npmjs.com/package/qrcodejs2)<br/>[github 地址](https://github.com/davidshimjs/qrcodejs)

## 基本使用

### 插件安装

```
cnpm install qrcodejs2 --save
// 或者
npm install qrcodejs2 --save
```



### 插件导入   

使用commonjs或者es6模块方式

```
import QRCode from 'qrcodejs2';
// 或者
let QRCode = require('qrcodejs2');
```

>  参考资料：👉【[说说前端的模块化机制](https://juejin.cn/post/7002240927871795213)】



### 页面容器

页面增加一个容器标签

```
<div id="qrcode" ref="qrcode"></div>
```



### 实例化

```
 creatQrCode() {
      let text = '二维码内容';
      let qrcode = new QRCode(this.$refs.qrcode, {
        text: text, //二维码内容字符串
        width: 128, //图像宽度
        height: 128, //图像高度
        colorDark: '#000000', //二维码前景色
        colorLight: '#ffffff', //二维码背景色
        correctLevel: QRCode.CorrectLevel.H, //容错级别
      })
}
```



## 问题处理

### 1、清除已经生成的二维码

```
方案一：this.$refs.qrcode.innerHTML = ''; 

方案二： qrcode.clear(); // 清除二维码方法二

```

### 2、动态替换二维码的内容

```
let string='新的内容'

qrcode.makeCode(string)
```



### 3、报错提醒 Error: code length overflow ？

这是因为url太长，导致二维码加载报错，可以调低容错率来处理。

修改参数：`correctLevel: QRCode.CorrectLevel.H` ，容错级别，由低到高分别为L M Q H



### 4、字符串较长，二维码显示模糊怎么办？

可以尝试先将生成的二维码倍数扩大，然后在css上面固定显示宽高，这样可以扩大显示像素精度

```
.qrcode-wrap{
	width: 128px;
	height: 128px;
}
.qrcode-wrap canvas,
.qrcode-wrap img {
	width:100%;
	height:100%;
}

 <div id="qrcode" ref="qrcode" class="qrcode-wrap"></div>
 
 creatQrCode() {
      let text = '二维码内容';
      let qrcode = new QRCode(this.$refs.qrcode, {
        text: text, 
        width: 128 * 3, //宽扩大3倍
        height: 128 * 3, //高扩大3倍
        colorDark: '#000000', 
        colorLight: '#ffffff', 
        correctLevel: QRCode.CorrectLevel.H, 
      })
}
```



### 5、二维码想要带白边怎么办？

插件默认生成的图片是没有边框的

![image-20211018211116289](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/18/image-20211018211116289.png)



**如果只想在页面显示上有边框**

方案一：直接给容器上面加样式，利用padding的特性，挤出白边

```
.qrcode-border{
        display: flex;
        width: 128px;
        height: 128px;
        box-sizing: border-box;
        padding: 10px;/*利用padding*/
        border: 1px solid rgb(204, 204, 204);
    }

<div id="qrcode" ref="qrcode" class="qrcode-border"></div>
```

方案二：给容器加一个带边框样式的父级容器

```
 .qrcode-container{
        display: flex;
        align-items: center;
        justify-content: center;
        width: 150px;
        height: 150px;
        border: 1px solid #cccccc;
    }

<div class="qrcode-container">
        <div id="qrcode" ref="qrcode"></div>
 </div>
```

效果展示

![image-20211018222628872](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/18/image-20211018222628872.png)

PS：如果只想【打印】的白边边框，这两种方案也可以

![image-20211018222808010](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/19/image-20211018222808010.png)



**如果想要页面和下载的二维码都带白边边框**，可以结合插件`html2canvas`来实现（如有其它方案，欢迎分享）

html2canvas 是一款利用javascript进行屏幕截图的插件

```
//安装
cnpm install --save html2canvas

//引入
import html2canvas from "html2canvas";
```



主要思路：

- 先使用QRCode生成二维码图片
- 然后使用html2canvas把带样式的二维码生成新的图片
- 隐藏QRCode生成的二维码图片

```
<div  ref="canvas" class="canvas-box" :style="{display:(originImg===true?'none':'flex')}">
    <div  class="qrcode-box">
        <div ref="qrcode" class="qrcode-img"></div>
    </div>
    <div class="qrcode-text">
        扫一扫
    </div>
</div>

<img :src="imgUrl">
```

*PS：完整的代码太多就单独放在飞书文档了，方便查看和复制*👉 [完整代码](https://z1uuhuab4m.feishu.cn/docs/doccnWxXrvZPBTYp9Xba9CyKRrf)

最终效果

![image-20211018233132225](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/18/image-20211018233132225.png)

> [html2canvas 文档地址](http://html2canvas.hertzen.com/documentation)
>
> [github 地址](https://github.com/niklasvh/html2canvas)



# 前端插件JsBarcode生成条形码

## 安装和引入

```
//安装
cnpm install jsbarcode --save

//引入
import JsBarcode from 'jsbarcode'
```



## 页面容器

```
<template>
  <!-- 条形码容器，可选svg、canvas，或img标签 -->
  <svg id="barcode"></svg>
  <!-- or -->
  <canvas id="barcode"></canvas>
  <!-- or -->
  <img id="barcode"/>
</template
```



## 实例化

不要在DOM还未加载时，调用jsbarcode库，比如create生命周期

简版

```
 JsBarcode('#barcode', 12345678,
       {
         displayValue: true // 是否在条形码下方显示文字
       }
     )
```

![image-20211019000752660](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/19/image-20211019000752660.png)

所有参数

```
 // 生成条形码
  JsBarcode('#barcode', '12345678', {
      format: "CODE39",//选择要使用的条形码类型
      width:3,//设置条之间的宽度
      height:100,//高度
      displayValue:true,//是否在条形码下方显示文字
      text:"Axjy",//覆盖显示的文本
      fontOptions:"bold italic",//使文字加粗体或变斜体
      font:"fantasy",//设置文本的字体
      textAlign:"right",//设置文本的水平对齐方式
      textPosition:"top",//设置文本的垂直位置
      textMargin:5,//设置条形码和文本之间的间距
      fontSize:15,//设置文本的大小
      background:"#eee",//设置条形码的背景
      lineColor:"#FF7F50",//设置条和文本的颜色。
      margin:15//设置条形码周围的空白边距
    })
```

![image-20211019000935843](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/19/image-20211019000935843.png)





> [GitHub 地址](https://github.com/lindell/JsBarcode) <br/>
>
> [文档地址](https://lindell.me/JsBarcode/)<br/>
>
> [条码生成器](https://lindell.me/JsBarcode/generator/)



# 扩展



## 常用条形码类型组成及说明



| 说明                                                         | 图示                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **CODEBAR条码** 这是一个自检码，没有校验位;用照片实验室，图书<br/>馆，内容仅支持0~9、+ - / $ . : 等6个特殊符号 | ![image-20211019005240225](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Typora/typora-user-images/2021/10/19/image-20211019005240225.png) |
| **Code11条码** 只允许11种字元，分别是0-9和"-",为降低检查错误率，<br/>可使用两位的检验码。 | ![](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Axjy/Downloads/2021/10/19/code11.png) |
| **Code39条码**字符集包括数字 、大写字母以及- . $ / + %等字符,通常<br/>运用于资产管理、会员卡、店内码管理、产品卷标 | ![](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Axjy/Downloads/2021/10/19/code39.png) |
| **Code 39 Extended** 这是一个扩展版本，支持完整的ASCII字符集的<br/>Code39条码。如果有一个要求使用Code39条码以外的数字和大写<br/>字母字符，然后这是推荐的条码。这是基于Code39条形码，这也是非常简单和容易使用 | ![](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Axjy/Downloads/2021/10/19/CODE39E.png) |
| **Code93条码** 是 full ASCII 模式，可使用ASCII全部128个字符。 | ![](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Axjy/Downloads/2021/10/19/code93.png) |
| **Code128A** 字符集 包括大写字母、数字、常用标点符号和一些控制符。 | ![](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Axjy/Downloads/2021/10/19/code128a.png) |
| **Code128B**字符集 包括大小写字母、数字、常用标点符号。      | ![](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Axjy/Downloads/2021/10/19/code128b.png) |
| **Code128C**字符集 为纯数字序列。                            | ![](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Axjy/Downloads/2021/10/19/code128c.png) |
| **Code128Auto** 是将上述三种字符集最佳优化组合。             | ![](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Axjy/Downloads/2021/10/19/code128auto.png) |



| 说明                                                         | 图示                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **EAN13商品条码** 是纯数字，而且位数是12位，最后一位为校验码，<br/>组成13位数字。主要用于各种商品零售行业包装印刷。 | ![](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Axjy/Downloads/2021/10/19/ean13.png) |
| **EAN8商品条码** 是纯数字，而且位数是7位，最后一位为校验码，<br/>组成8位数字。主要用于各种商品零售行业包装印刷。 | ![](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Axjy/Downloads/2021/10/19/ean8.png) |
| **GS1-128 (EAN-128)** 是由UPC/EAN指定代表意义规则的128码，<br/>编码方式同code128条码。 | ![](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Axjy/Downloads/2021/10/19/ean128.png) |
| **ISBN条码**：ISBN是“国际标准书号”类型是基于EAN-13,主要用于<br/>出版物书籍类产品。 | ![](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Axjy/Downloads/2021/10/19/isbn.png) |
| **交叉25码**（Interleaved 2 of 5），常用于物流管理，字符集仅为数字<br/>且个数为偶数,为奇数将自动在前面加"0"。 | ![](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Axjy/Downloads/2021/10/19/2of.png) |
| **MSI条形码** 必须是纯的数字0-9，带有一位检验码。主要使用在图书馆<br/>和零售应用中。在MSI字体中，使用圆括号来表示开始和结束字符。 | ![](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Axjy/Downloads/2021/10/19/msi.png) |
| **UPC-A条码** 商品条码是纯数字，而且位数是11位，在编码过后外<br/>加一位校验码，组成12位数字,主要在美国和加拿大使用。 | ![](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Axjy/Downloads/2021/10/19/upca.png) |
| **UPC-E条码** 商品条码是纯数字，是由UPC-A缩减而成，位数是7位，<br/>而且首位必须为0，在编码过后外加一位校验码，组成8位数字。 | ![](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Axjy/Downloads/2021/10/19/upce.png) |



| 说明                                                         | 图示                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **UPC E 2 Digits** 特性同 UPC-A，后面附加之2码条形码通常使用于价格用途。 | ![](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Axjy/Downloads/2021/10/19/u2.png) |
| **UPC-E 5 digits** 特性同 UPC-A，后面附加之5码条形码通常使用于价格用途 | ![](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Axjy/Downloads/2021/10/19/u5.png) |
| **POSTNET**  (邮政数字编码技术)条形码用来对美国邮件代码进行编码,由5位或9位或11位数字组成 | ![](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Axjy/Downloads/2021/10/19/p.png) |
| **Intelligent Mail** 这是“智能邮件”是指美国邮政为国内邮递服务提供的服务条码，你可以提供<br/>5位数字（邮政编码）<br/>9位数字（邮政编码+ 4代码）<br/>11位数字（邮政编码+ 4代码+ 2位数字） | ![](https://gitee.com/Olivivian/PicGoImages/raw/master/img//Axjy/Downloads/2021/10/19/mail.png) |





以上主要只写了Vue版的示例，但是两个插件都是使用原生JavaScript写成，不依赖任何库/框架，所以不论是Jquery还是React都可以用





