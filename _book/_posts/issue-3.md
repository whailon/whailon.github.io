# 滚动加载
2017-05-11
------

打开浏览器，调整下浏览器窗口高度，让页面可以滚动。
先了解三个变量


> * document.body.scrollTop 滚动条滚动的距离
> * window.innerHeight 浏览器窗口高度
> * document.body.clientHeight 内容高度


> 原理：当滚动条滚动距离 + 浏览器窗口高度 >= 内容高度 触发加载数据

```python
  document.addEventListener('scroll', function () {
    var scrollTop = document.body.scrollTop
    if(scrollTop + window.innerHeight >= document.body.clientHeight) {
      // 触发加载数据
      loadMore()
    }
  })
  function loadMore () {
    // todo
  }
```