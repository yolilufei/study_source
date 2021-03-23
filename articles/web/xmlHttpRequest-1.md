### XMLHttpRequest 系列一

#### 系列目录
  1. <a style="color: red">初识 XMLHttpRequest</a>
  2. XMLHttpRequest 原理解析
  3. 手写axios


#### 简介
> [引用自MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest): XMLHttpRequest（XHR）对象用于与服务器交互。通过 XMLHttpRequest 可以在不刷新页面的情况下请求特定 URL，获取数据。这允许网页在不影响用户操作的情况下，更新页面的局部内容。XMLHttpRequest 在 AJAX 编程中被大量使用  

从这段话里可以总结出XMLHttpRequest(后面统一简称XHR)的几个特点:
- 用于客户端和服务端交互
- 局部刷新
- 可异步请求

说起 XHR，我们都很熟悉，有人说：不就是接口请求用的吗，没什么大不了的。确实，XHR现在主要被应用在接口请求中，而我们最常用的请求库比如 axios 等就是基于 XHR 的。但是你真的了解 XHR 吗？XHR为什么可以异步请求数据？中止 XHR 请求的原理是什么？XHR 如何兼容低版本IE？XHR 和 fetch 有什么区别。。。
 
带着这些问题，让我们深入了解 XHR 到底是什么。

#### 初识XHR
todo：初始化XHR，介绍XHR的属性、方法、事件、兼容性等