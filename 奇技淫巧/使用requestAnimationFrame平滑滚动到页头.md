### 使用requestAnimationFrame平滑滚动到页头

```html
<div>
  <p>你好中国</p>
  <p>你好中国</p>
  <p>你好中国</p>
  .... <!-- 多放一点p标签 -->
</div>
<div style="position: fixed; top: 0; right: 0;">
  <button id="requestAnimationFrameBtn">点击回到顶部（使用requestAnimationFrame）</button>
  <button id="scrollSmoothBtn">点击回到顶部（使用scroll - 'smooth' 方式）</button>
</div>
```

```javascript
(function() {

  // 滑动到顶部
  var scrollToTopUsedByRequestAnimationFrame = function () {
    var drag = 10;
    // 距离顶部的距离
    const gap = document.documentElement.scrollTop || document.body.scrollTop;
    if (gap > 0) {
      // 设置一个动画, 每次执行 gap - gap / drag 长度
      window.requestAnimationFrame(scrollToTopUsedByRequestAnimationFrame);

      /*
      window.scrollTo({
        top: gap - gap / drag,
        left: 0,
        behavior: "smooth" 
      })
      */
     window.scrollTo(0, gap - gap / drag);
    }
  };

  var scrollToTopUsedBySmooth = function () {
    window.scrollTo({
      top: 0,
      left: 0,
      // 采用平滑过渡实现
      behavior: "smooth" 
    });
  };

  document.getElementById('requestAnimationFrameBtn').addEventListener('click', scrollToTopUsedByRequestAnimationFrame);
  document.getElementById('scrollSmoothBtn').addEventListener('click', scrollToTopUsedBySmooth);
})();
```