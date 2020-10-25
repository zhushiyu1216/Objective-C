# 分数Fraction类
我们想实现一个分数的表示，如1/2，同时想把它打印出来，我们先看看面向方法的写法会怎么实现。

``` c
#import <Foundation/Foundation.h>

int main (int argc, char *argv[]) {
  @autoreleasepool {
    int numerator = 1;
    int denominator = 2;
    NSLog(@"the fraction is %i/%i", numerator, denominator);
  }
}
```

如果我们想再写一个分数，只能把这三行代码再写一遍。那有没有办法把分数抽象一下定义成一个类呢？假设这个类的名字Fraction，它有两个成员属性numerator和denominator，同时有一个成员方法print打印，则上边的代码可以写成这样：

``` objectivec
#import <Foundation/Foundation.h>
#import "Fraction.h"

int main (int argc, char *argv[]) {
  @autoreleasepool {
    Fraction *fraction = [[Fraction alloc] init];
    Fraction *fraction2 = [[Fraction alloc] init];
    Fraction *fraction3 = [[Fraction alloc] init];

    fraction.numerator = 1;
    fraction.denominator = 2;

    fraction2.numerator = 1;
    fraction3.denominator = 2;

    fraction2.numerator = 1;
    fraction3.denominator = 2;

    [fraction print];
    [fraction2 print];
    [fraction3 print];
  }
}
```

是不是感觉代码还多了一行？类还有很多定义方法可以让初始化和赋值更简单，后面我们会逐渐学习；同时，这里的打印的方法只有一行代码，过于简单，没有体现出复用的优势。不过我们能发现它另外一个好得就是，如果要修改打印的内容，只用修改`print`方法一个地方就可以了。这种写法已经体现出面向对象的模式了。

我们再简单看一下Fraction定义的写法：

``` objectivec

//Fraction.h文件
#import <Foundation/Foundation.h>

@interface Fraction : NSObject

// 两个成员属性
@property int numerator, denominator;

// print 方法
-(void) print;

@end


// Fraction.m文件
@implementation Fraction

@synthesize numerator, denominator;

- (void) print {
     NSLog(@"the fraction is %i/%i", numerator, denominator);
}

@end
```


这里只是把代码贴出来，我们了解大体的代码结构即可，关于代码的细节会在接下来看章节里逐步讲解。