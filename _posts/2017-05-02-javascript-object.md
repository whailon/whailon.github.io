---
layout: default
title: javascript 对象
---
#### {{ page.title }}
{{ page.date | date: "%Y-%m-%d" }}
------

##### 1.创建直接的实例
```python
var obj = new Object();
obj.propertyName = value;
```
这个例子创建了对象的一个新实例，并向其添加了一个属性，propertyName是属性名，value是属性值

##### 2.字面量定义
```python
var obj = {
    propertyName: value
}
```
直接定义了一个变量，变量属性propertyName,值value

##### 3.使用对象构造器
```python
function Person(name, age){
    this.name = name;
    this.age = age;
}
```
本例使用函数来构造对象,创建 JavaScript 对象实例:

~~~
var me = new Person("whl", 30);
~~~

待续...