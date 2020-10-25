# Fraction类实例分析

这一小节我们结构Fraction类，把OC中类的定义、实例化、变量封状、方法访问等都串起来讲一下。

为了便于理解成员变量等，更深入了解类的定义，我们不使用@property命令来声明属性，每一个变量都自己写，并自行进行封装。

##1、先定义Fraction类，即`@interface`部分：

``` objc

#import <Foundation/Foundation.h>
@interface Fraction : NSObject

/// get 分子
- (int) numerator;
/// 设置分子
/// @param numerator 分子
- (void) setNumerator: (int) numerator;

/// get 分母
- (int) denominator;
/// 设置分母
/// @param denominator 分母
- (void) setDenominator: (int) denominator;

/// 打印
- (void) print;
@end
```

我们把分子和分母这两个成员变量都用get和set方法封装了起来，同时，这里注意一下OC注释的常用表示方式，与C和Java都不太一样。interface中一共定义了5个方法。

## 2、再来定义Fraction类的`@implementation`部分：

``` objc
#import "Fraction.h"

@implementation Fraction
{
  int _numerator; //分子
  int _denominator; //分母
}

- (int) numerator {
  return _numerator;
}

- (void) setNumerator: (int) numerator {
  _numerator = numerator;
}

- (int) denominator {
  return _denominator;
}

- (void) setDenominator: (int) denominator {
  _denominator = denominator;
}

- (void) print {
  NSLog(@"the fraction is %i/%i", _numerator, _denominator);
}
@end
```

## 再来看看main函数中对它的调用：

``` objc
#import "Fraction.h"

int main (int argc, char * argv[]) {
  @autoreleasepool {
    Fraction *fraction;
    fraction = [Fraction alloc];
    fraction = [fraction init];
    // 上边是对象变量的声明和初始化，一般用一个语句表示即可：
    // Fraction *fraction = [[Fraction alloc] init];

    //设置分子分母为1/3
    fraction.numerator = 1; //这一句也可以用方法调用的写法：[fraction setNumerator: 1];
    fraction.denominator = 3;

    // 打印分数
    [fraction print];
  }
}
```

对于程序调用部分，还有以下几点说明：  
（1）要理解这里的fraction指针，它存储的只是Fraction对象在内存中的地址，而不是对象本身，跟C的指针意义是一样的；  
（2）alloc分配内容和init初始化两个方法都是Fraction从父类NSObject中继承来的；  
（3）alloc + init两个方法还有一个简便的替代方法：[Fraction new]；不过一般不使用这个方法，平时定义类时要在init方法中附加一些参数的初始化；  
（4）OC中常称方法调用为消息发送，比如[fraction print]一般称为：print方法发送给fraction；