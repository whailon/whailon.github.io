# 重构个人博客项目
2022-01-27
------

## 需要实现功能
+ 布局调整，增加侧边栏
+ gitbook生成静态html

## gitbook安装

```bash
npm install -g gitbook-cli
```

## gitbook使用
切换项目根目录，接着执行以下命令

```bash
gitbook init
```

执行完后，项目根目录多出两个文件，README.md(项目简介)和SUMMARY.md(项目目录结构配置)

## 写目录
* 根据markdown语法，中括号里是这个目录的名字，小括号里是路径。
* 写完目录后再次执行gitbook init Gitbook会查找SUMMARY.md中描述的目录和文件，如果没有则会创建。

## 写文章
写完目录后，创建新md文件，可以使用markdown在线编辑器写好文章复制到新文件内，执行gitbook build，生成
同名html文件