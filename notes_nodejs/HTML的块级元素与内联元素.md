## 块级元素的特点：

1.  块级元素既可以容纳内联元素也可以容纳块级元素。
2.  块级元素在默认的情况下是独占一行的。
3.  块级元素大小是可以控制的，css可以通过width与height设定高度和宽度。宽度默认值就是它所在容器宽度的100%。
4.  块级元素可以设置margin和padding属性.
5.  块级元素对应属性display：block；

## 内联元素的特点：

1.  内联元素默认情况下可以和其他内联元素元素在一行上。
2.  内联元素默认情况下的大小是不可以控制的。
3.  内联元素可以产生代码换行和空格。
4.  内联元素对应属性display：inline；
5.  内联元素只能容纳文本或者内联元素。

> img：图片是内联元素

内联元素的margin和padding属性,水平方向的padding-left,padding-right,margin-left,margin- right都产生边距效果,但竖直方向的padding-top,padding-bottom,margin-top,margin-bottom却不 会产生边距效果.

display：inline-block；可以让元素具有块级元素和行内元素的特性：既可以设置长宽，可以让padding和margin生效，又可以和其他行内元素并排。

当a链接的href为空时点击会刷新页面。