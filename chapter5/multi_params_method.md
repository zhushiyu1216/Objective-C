# 多参数方法
多参数方法我们在前面章节中讲过，这里分分别对有参数名和无参数名再做一下讲解，同时，因为这章讲的是类的属性相关知识，所以我们也主要讲set方法的多参数。

## 带参数名的多参数方法

我们在属性一节讲到，每个属性会被生成一个set方法，这样比较方便我们对一个属性赋值，但如果想一次对多个属性赋值，则就需一个一个属性的写，显得没那么方便。此时比较常见的方式是定义一个多参数的set方法，如：

``` objc
- void setAge: (int) age andName: (NSString*) name andWeight: (float) weight;
```

上边这个方法可以一次性设置多个属性，对每一个参数都有一个命名，同时，OC里常用`and`进行一下关联，这样显得方法更容易阅读。

## 不带参数的多参数方法

方法中的参数名不是必须的，可以省略掉，如：

``` objc
- void set: (int) a : (NSString *) n : (float) w;
```

此时在调用时也忽略参数名，直接传入值即可： 

``` objc
[person set: 15 : @"xiaoming" : 1.2];
```

## 使用多参数重写第二章的Fraction分数类

``` objc
@interface Fraction : NSObject

@property int numerator, denominator;

/// 一次设置两个属性的值
- (void) setTo: (int) n over: (int) d;

@end

@implementation Fraction

@synthesize numerator, denominator;
- (void) setTo: (int) n over: (int) d {
  numerator = n;
  denominator = d;
}
@end
```

注意个成员方法`setTo: over:`，它的参数名定义为n和d，如果定义成numerator和denominator，此时会导致对类的两个属性屏蔽，从而使用赋值失效。如果已经对属性进行了synthesize合成，则要避免将入参名定义为和属性名一样。