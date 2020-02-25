### 移动端1px问题

#### 产生原因

设备像素比：`window.devicePixelRatio = 物理像素分辨率 / CSS像素分辨率`。目前主流的手机屏幕的 dpr 一般是 2 或者 3。如 iphone x 的 dpr = 3，iphone 6 的 dpr = 2。所以 css 中的 1px 和我们物理设备当中的 1px 是不相等的。这就造成了 1px 问题。

对于前端工程师来说，给到的 ux 设计标准往往是 `750px` 的，所以 dpr = 2 的机型来说，我们在写 css 的时候都是将设计的尺寸除以 2 进行使用的。

#### 一些参考的解决方法

* 方法一：对于 ios 设备，对于 dpr = 2 的两倍屏可以直接使用 `0.5px` 进行设置。但是这个目前兼容性不是很好，ios 高版本应该没有问题，对于安卓和低版本的 ios 来说，兼容性就不乐观了。

* 方法二：使用 [`border-image`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-image)

```css
border: 1px solid transparent;
border-image: url("border.png") 2 repeat;
```

只不过这样以后修改边框就比较麻烦了。

* 方法三：使用伪类，将伪类元素设置绝对定位，与父元素左上角对齐，设置 `height = 1px`，设置 `width = 100%`，然后对 y 方向进行缩放。

```css
div {
  position: relative;

  &::after {
    position: absolute;
    display: block;
    content: '';
    background-color: #ddd;
    width: 100%;
    height: 1px;
    transform: scale(1, 0.5);
    top: 0;
    left: 0;
  }
}
```

可能影响清除浮动

* 方法四：设置 viewport 的 scale 值

```javascript
var viewport = document.querySelector("meta[name=viewport]");
switch (window.devicePixelRatio) {
  case 2:
    viewport.setAttribute('content', 'width=device-width,initial-scale=0.5, maximum-scale=0.5, minimum-scale=0.5, user-scalable=no');
    break;
  case 3:
    viewport.setAttribute('content', 'width=device-width,initial-scale=0.3333333333, maximum-scale=0.3333333333, minimum-scale=0.3333333333, user-scalable=no');
    break;
  default: // window.devicePixelRatio == 1
    viewport.setAttribute('content', 'width=device-width,initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no');
    break;
}
```

这个方法兼容性可以，写起来直接使用 1px 就可以，比较方便。