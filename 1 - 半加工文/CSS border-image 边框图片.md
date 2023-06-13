CSS border-image 边框图片

## 读完我可以收获

- border-image 的各属性、含义
- border-image 的使用场景及注意事项
- 边框渐变与圆角无法同时生效的解决办法
- 背景图片自适应文案拉伸的方法

## 介绍

1. 效果

把一张图盖到元素的 border 上，实现花边。

【一个背景图】——》【一个边框】==》【成品】

2. 属性：共有五个属性

2.1 border-image-source: 这个和背景格式一样，url() 或渐变。

2.2 border-image-slice: ，设置四个方向的分割线，将图像裁减成 9 个区域，外面一圈会贴到边框上，中间部分会被丢弃，加上 fill 后，中间会被保留。

【设置的值与切线图像】——》【成品】

2.3 border-image-width: 图像的宽度，值为相对于边框的倍数，默认是 1（与边框宽度一样），一般不需要调整。

2.4 border-image-outset: 图像向外偏移的宽度，超出边框盒的大小，不会影响布局，就像 outline 一样

2.5 border-image-repeat: 边框图像的填充规则，不会影响四个顶点的图像，可以对横竖分别设置规则

- stretch：拉伸图片
- repeat：平铺，就像贴瓷砖，但是不是整数个，会有裁切
- space：平铺，会保证整数个，但是可能瓷砖之间有空隙
- round：平铺，会保证整数个，不会有空隙，但是会对瓷砖缩放

缩写时为：border：  border-image-source border-image-slice / border-image-width / border-image-outset / border-image-repeat

下面用一张图感受下效果，也可以点击这里去体验

【border-image 各属性变化】

## 使用场景

花边，利用 border-image 的平铺特性，可以实现比较精美的花边效果。

【花边图片】

聊天气泡，相比 background，border-image 的优势在于可以适应内容的高度，不会引起图片两端的变形。更多关于聊天旗袍的实现方式可以查看：这篇文章。

【聊天气泡】

## 注意事项

border-image 作用在 border 上，所以使用的前提是设置了 boder，boder-width 和 border-style 都需要设置，border-color 建议设置为 transparent

border-radius 不会影响 border-image 的表现，所以如果有圆角的需求，需要更改图片，或使用其他方式：其他方式可以参考：这篇文章。

○ 加 background-clip

https://www.jianshu.com/p/b9d34f384e67

https://www.w3.org/TR/css-backgrounds-3/#corner-clipping

https://juejin.cn/post/6844903972281516045

## 兼容性

根据 can i use 显示，除了几个特殊属性，可以放心使用

https://caniuse.com/?search=border-image

## 参考

https://developer.mozilla.org/en-US/docs/Web/CSS/border-image

