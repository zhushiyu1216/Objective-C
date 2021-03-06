# 类继承

## 什么是继承
继承是面向对象软件技术当中的一个概念，与多态、封装共为面向对象的三个基本特征。继承可以使得子类具有父类的属性和方法或者重新定义、追加属性和方法等。

继承中子类继承父类的特征和行为，使得子类对象（实例）具有父类的属性和方法，或子类从父类继承方法，使得子类具有父类相同的行为。

子类的创建可以增加新数据、新功能，可以继承父类全部的功能，但是不能选择性的继承父类的部分功能。继承是类与类之间的关系，不是对象与对象之间的关系。

例如：先定义一个类叫车，车有以下属性：车体大小、颜色、轮胎、方向盘、品牌、速度、排气量，由车这个类派生出轿车和卡车两个类，为轿车添加一个小后备箱，而为卡车添加一个大货箱。

``` mermaid
    graph TB
    A(基类) -->B("车(父类)")
    B --> C(轿车)
    B --> D(卡车)
    C --> E(大众)
    C --> F(红旗)
```

## 继承的好处
+ 提高了代码的复用性，能够大大缩短开发周期；
+ 提高了代码的维护性；
+ 让类与类之间产生了关系，是多态的前提；

本章包含四小节和一个小练习：

+ [OC类的继承关系](chapter6/inheritance_relatation.md)
+ [子类扩展新方法](chapter6/subclass_add_methods.md)
+ [子类覆盖父类的方法](chapter6/override_method.md)
+ [类中含类](chapter6/object_member.md)
+ [练习](chapter6/exercise.md)

#### Demo代码下载
 [点击下载](http://objective-c.codebook.cf/chapter6/OC_inherit.zip)

 #### 视频教程
 <iframe src="//player.bilibili.com/player.html?aid=801012811&bvid=BV1Fy4y1v7uz&cid=277014827&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true" width="800" height="600"> </iframe>

[打赏](../include/donate.md ':include')