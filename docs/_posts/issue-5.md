# node设置设置淘宝镜像
2017-08-05
------

最近一直遇到npm install 报错，报错信息显示与phantomjs有关
于是上百度查找好多，有使用cnpm安装的，不知道它是怎么成功的
反正我是没成功，应该是这个组件比较大链接超时了都。所以看到错误提示
显示在
```phthon
C:\Users\Administrator\AppData\Local\Temp\phantomjs
``` 无法找到压缩包
ok,直接从github上面找到对应的压缩包，下载后把压缩包复制到改目录下
然后在npm install ，ok 成功了
