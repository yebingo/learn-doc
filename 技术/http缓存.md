# http缓存

## 大致概览
<img src="https://api.superbed.cn/pic/5bf7de3cc4ff9e05833a0755" width="800px">

## 强制缓存
1. `Pragma`：只有`no-cache`字段，优先级最高
2. `Cache-Control`：`no-store` 、`no-cache` 、 `private` 、 `public` 、 `max-age`
3. `Expires`：过期时间

## 协商缓存
<img src="https://www.superbed.cn/pic/5bf13cc5c4ff9e24bf0ee0f7" width="800px">

1. `Etag`/`If-None-Match` 文件唯一标识标识符，服务器收到`If-None-Match`，从服务器查找是否有同样标识符的文件，若有返回`304`

2. `Last-Modified`/`If-Modified-Since` 文件最近一次修改时间
