CSS 圆形渐变边框，背景透明

## 读完我可以收获

- CSS 圆形、圆角渐变边框的实现方式
- background-clip、text-stroke 的使用

## 背景

![iShot_2023-06-21_16 (1)](../assets/iShot_2023-06-21_16%20(1).gif)

从 w3c 得知 border-image 不受 border-radius 的影响，因此没办法简单的实现这种效果。

> https://www.w3.org/TR/css-backgrounds-3/#corner-clipping

在网上找到的很多方式，大多是是通过元素叠加实现的，如：大的渐变背景 + 小的纯色背景/纯色伪元素。

【动图】

>  这位大佬的文章写的很好：可以先去看一下，本文只是简单补充下其他情况【这篇文章】https://juejin.cn/post/6844903972281516045

但是这种情况下，想要背景镂空只保留边界就没办法了。今天思考的时候，突然想到了 background-clip 文字裁剪，它可以让背景只在文字内显示，这个就能实现我想要的背景镂空的效果！

【文字裁剪的图片】

关于 background-clip 属性，是用来设置背景的裁剪范围的，主要分为 border-box, content-box, padding-box, text, 我们此处使用的就是 text。详细可以参考：

https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-clip

【文字裁剪图片】

如果我希望实现一个圆形边框的话，只需要找一个完美的圆就好了，然后使用文字裁剪让文字之外的部分透明，我找啊找找到了好多形状，比如这个 ◯，下面请看实践。

## 实践

先看代码：

```less
.box {
  margin: 0 50px;
  width: 100px;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  overflow: visible;
  font-size: 50px;
  position: relative;
  color: transparent;
  -webkit-text-stroke: white 2px;

  &::after {
    width: 100%;
    height: 100%;
    font-size: 100px;
    font-family: Arial;
    position: absolute;
    top: 0;
    left: 0;
    background-image: linear-gradient(135deg, #43c6ac, #f8ffae);
    background-clip: text;
    -webkit-background-clip: text;
    -moz-background-clip: text;
    color: transparent;
    display: flex;
    align-items: center;
    justify-content: center;
    -webkit-text-stroke-color: transparent;
  }
}
```

![image-20230621162656212](../assets/image-20230621162656212.png)

我们需要的只是一个伪元素，在伪元素中写一个 ◯，设置背景并设置文字裁剪。最后调整位置叠加到我们的盒子的边框上。

小 tips：

我们会发现边框的宽度不好调节，这或许可以通过 font-weight 进行调节，但是它的粒度和范围都很有限。

这里我发现了另一个奇妙的属性：text-stroke 文字描边，可以通过它调节文字描边宽度，font-weight 设为400 即可。

此外，如果文字的大小使用 font-size 不能满足要求，我们可以借助 transform：scale 再次调整。

## 总结 & 源码

源码在这里，有需要的可以参考一下：

https://code.juejin.cn/pen/7247051025881202745

## 注意事项

由于同一个文字在各种字体下的大小样式都不同，我们在使用此方法时要设置好字体，通用的字体最好，如 Arial，所有浏览器都会支持，并且建议加 !important 避免系统字体干扰。

字符集来源，建议测试下低版本浏览器的兼容性：

https://en.wiktionary.org/wiki/Appendix:Unicode/Geometric_Shapes

https://caniuse.com/?search=text-stroke
