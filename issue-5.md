# node设置设置淘宝镜像
2017-08-05
------

## 原因
由于node安装插件是从国外服务器下载，受网络影响大，速度慢且可能出现异常。
阿里云提供完整的npmjs.org镜像，也就是说我们可以使用阿里布置在国内的服务器来进行node安装。

## 推荐配置
直接在命令行设置
```bash
npm config set registry https://registry.npm.taobao.org
```
检测是否成功
```bash
// 配置后可通过下面方式来验证是否成功
npm config get registry
// 或
npm info express
```

## 问题
最近一直遇到npm install 报错，报错信息显示与phantomjs有关
于是上百度查找好多，有使用cnpm安装的，不知道它是怎么成功的
反正我是没成功，应该是这个组件比较大链接超时了都。
所以看到错误提示显示在

```bash
C:\Users\Administrator\AppData\Local\Temp\phantomjs
``` 

无法找到压缩包。

## 解决方法
直接从github上面找到对应的压缩包，下载后把压缩包复制到改目录下
然后在npm install ，ok 成功了
