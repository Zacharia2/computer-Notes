**TODO：等待修改**

CSS常用布局之宽高自适应 [https://www.w3cschool.cn/css_series/css_series-uhmf24qa.html](https://www.w3cschool.cn/css_series/css_series-uhmf24qa.html)

元素的宽度自适应很好实现，高度要等比例变化的话，就需要一个css知识点：

> 元素的margin和padding属性的值（无论是上下边距还是左右边距）如果设置为百分比，都是以宽度为基准计算。
> 
> 也就是说，在已知宽高比的情况下，css虽然不能确定height的值，但是可以确定padding-top等属性的值。

实现思路：

1、算出宽高比（高 / 宽），并设置为padding-top的值，height设置为0（由padding-top撑起元素的高度）。

2、此时元素的实际内容被挤到了下方，所以用绝对定位改变其位置。

代码：

```html
<div class="ac_coupon-wrap">
    <div class="ac_coupon-content">
        <!-- 内容 -->
    </div>
</div>
```

```css
.ac_coupon-wrap {
    height: 0;
    padding-top: 15.16%;
    position: relative;
    .ac_coupon-content {
        position: absolute;
        top: 0;
        width: 100%;
        height: 100%;
        background-size: cover;
    }
}
```
