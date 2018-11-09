# npm装包太慢怎么办
`npm`装包太慢，但又因为想读取`package-lock.json`而不能使用yarn？那你可以试试下面的办法：

```bash
npm --registry=https://registry.npm.taobao.org i
```

以上方法是使用`npm`进行安装，会读取`package-lock.json`，同时使用的是`淘宝镜像源`，所以速度更快。
