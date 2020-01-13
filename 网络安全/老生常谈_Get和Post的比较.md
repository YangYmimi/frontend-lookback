### 老生常谈 - Get和Post的比较

#### 作用

GET 用于获取资源，而 POST 用于传输实体主体。

#### 参数

* GET请求参数通过URL进行拼接，本身是没有参数长度限制的，只不过由于不同浏览器或者Web服务器的限制，导致GET请求会有些长度限制；POST请求参数通过实体携带。

* URL只支持 ASCII 码，所有GET请求参数会有编码的现象，特别是带有中文字符的参数；POST请求支持标准字符集，所以我们看到的请求参数不会存在编码情况

#### 安全性

> 说一个HTTP方法是安全的，是说这是个不会修改服务器的数据的方法。也就是说，这是一个对服务器只读操作的方法。我们叫 `idempotent`。安不安全的定义是这个方法需不需要服务器修改数据。客户端不需要服务端修改数据，也就不会给服务端造成不必要的负担。浏览器调用安全的方法就不用考虑会给服务端造成什么危害，这样服务端就允许客户端预加载资源。

安全的方法有：GET、HEAD、OPTIONS；不安全的方法有：PUT、DELETE、POST

#### 幂等性

> 同样的请求被执行一次与连续执行多次的效果是一样的，服务器的状态也是一样的。

幂等的方法有：GET、HEAD、PUT、DELETE；不幂等的方法有：POST

#### 可缓存性

GET 方法本身是可缓存的，POST 方法绝大多数情况下不可缓存。关于缓存的内容可以针对性的复习：**HTTP缓存** 相关内容。

参考：

* [HTTP安全性?](https://developer.mozilla.org/zh-CN/docs/Glossary/safe)
* [HTTP幂等性?](https://developer.mozilla.org/zh-CN/docs/Glossary/%E5%B9%82%E7%AD%89)
* [HTTP2介绍](https://developers.google.com/web/fundamentals/performance/http2/?hl=zh-cnyouxia)
* [Web性能优化与HTTP2](https://www.kancloud.cn/digest/web-performance-http2)