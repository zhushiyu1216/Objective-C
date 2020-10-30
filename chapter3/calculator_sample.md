# Calculator类

本节我们将创建一个Calculator类，可以称为计算器类，这个类会包含加、减、乘、除四种运算，通过这些运算，我们把前两节学习的数据类型和运算符进行一下练习。

先声明一个Calculator类，这个类的用法是可以不停的进行运算，如a + b * c / d，所以它会有一个累计结果，在这个结果上还可以不停的运算。除了加、减、乘、除四个方法外，还有一个clear方法用于清除之前的运算结果。

声明如下：

``` objc
#import <Foundation/Foundation.h>

@interface Calculator : NSObject

/// 结果
@property double accumulator;

/// 清除
- (void) clear;

/// 加法
/// @param value  value
- (void) add: (double) value;

/// 减
/// @param value  value
- (void) subtract: (double) value;

/// 乘
/// @param value  value
- (void) multiply: (double) value;

/// 除
/// @param value  divide
- (void) divide: (double) value;

@end
```

我们看看implemention里的实现代码:

``` objc
#import "Calculator.h"

@implementation Calculator

@synthesize accumulator;

- (void) clear {
    self.accumulator = 0;
}
- (void) add: (double) value {
    self.accumulator += value;
}
- (void) subtract: (double) value {
    self.accumulator = self.accumulator - value;
}
- (void) multiply: (double) value {
    self.accumulator = self.accumulator * value;
}
- (void) divide: (double) value {
    self.accumulator /= value;
}

@end
```

做一下调用测试：

``` objc
#import <Foundation/Foundation.h>
#import "Calculator.h"

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        Calculator *c = [[Calculator alloc] init];
        c.accumulator = 0;
        [c add: 200.];
        [c divide: 15.5];
        [c subtract: 10.3];
        [c multiply: 5];
        
        NSLog(@"the result is %g", c.accumulator);

        [c clear];
        [c add: 30.5];
        NSLog(@"the result is %g", c.accumulator);
    }
    return 0;
}
```

大家可以运行一下，同时不断调整占位符、强制类型转换等进行测试。
