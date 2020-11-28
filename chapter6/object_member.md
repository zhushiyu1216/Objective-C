# 类中含类

类中含类的意思是，一个类中的成员变量的类型也是一个类，在这种情况下需要注意类的封装性，这节我们会从实例中进行学习；另一个可以学到的是@class指令。

我们还以矩形为例子，矩形除了长、宽两个属性，还有一个有原点坐标的属性，我们先定义一个XYPoint类表示会标。

``` objc
@interface XYPoint : NSObject
@property int x, y;
- (void) setX: (int) xVar andY: (int) yVar;
@end

@implementation XYPoint
@synthesize x, y;
- (void) setX: (int) xVar andY: (int) yVar {
  x = xVar;
  y = yVar;
}
@end
```

再来定义Rectangle类，这里注意@class指定，它一般用在interace中声明，说明有一个类，我们在这个文件里并不需要访问这个类的任何属性和方法。实际上是#import的一种简单写法。这种方法并不常用，你可以能看懂即可。

``` objc
@class XYPoint;
@interface Rectangle : NSObject
@property int width, height;
@property XYPoint *origin;

- (void) area;
- (void) perimeter;
@end

@implementation Rectangle 
@synthesize width, height, origin;

- (void) area {
  return width * height;
}

- (void) perimeter {
  return 2 * (width + height);
}

- (NSString *) description {
  return [NSString stringWithFromat: @"[(%i, %i), %i, %i]", origin.x, origin.y, width, height];
}
@end
```

这个实现的方法存在一个问题，就是Rectangle的origin并没有封闭，如我们给origin进行了赋值，但当外部的origin改动时，rectangle内的原点坐标也被改了。如：

``` objc
int main (int argc, char *argv[]) {
  @autoreleasepool{
    XYPoint *point = [[XYPoint alloc] init];
    [point setX: 4 andY: 5];

    Rectangle *rect = [[Rectangle alloc] init];
    rect.width = 200;
    rect.height = 100;
    rect.origin = point;
    NSLog(@"1, rectangle = %@", rect);
    
    [point setX: 2 andY: 9];
    NSLog(@"2, rectangle = %@", rect);
  }
}
```

可以发现，外部的point变化后，rect也被改变了，这就是封闭性没做好。我们接着再重启下往下写：


``` objc
int main (int argc, char *argv[]) {
  @autoreleasepool{
    XYPoint *point = [[XYPoint alloc] init];
    [point setX: 4 andY: 5];

    Rectangle *rect = [[Rectangle alloc] init];
    rect.width = 200;
    rect.height = 100;
    rect.origin = point;
    NSLog(@"1, rectangle = %@", rect);
    
    [point setX: 2 andY: 9];
    NSLog(@"2, rectangle = %@", rect);

    // 获取原点
    XYPoint *origin = rect.origin;
    [origin setX: 1 andY: 7];
    NSLog(@"3, rectangle = %@", rect);
  }
}
```

我们看，当获取到的原点被改了，rect也被改了，这也是封闭性没做好的原因。造成这种情况的本质原因是OC中的变量参数在传递时使用的是值复制，当变量类型是指针时，只复制了指针，并没有复制指针所指向的具体对象。那我们要怎么做呢？

显示写一下origin属性的get和set方法，在这些方法里通过复制的方式设置或返回原点坐标的副本。

``` objc
@implementation Rectangle 
...
- (XYPoint *) origin {
  XYPoint *point = [[XYPoint alloc] init];
  [point setX: origin.x andY: origin.y];
  return point;
}

- (void) setOrigin: (XYPoint *) originParam {
  if (origin == nil) {
    origin = [[XYPoint alloc] init];
  }

  [origin setX: originParam.x andY: originParam.y];
}
@end
```