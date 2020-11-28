# OC类的继承关系

## 一切从根类（NSObject）开始
继承就像一棵倒过来的树一样，不断的分叉，这些树叉最初都是从树的根部分出来的，OC中这个根就是NSObject类，所以我们以前定义类的形式是：

```
@interface Fraction : NSObject
  ...
@end
```

## 子类中只可以访问父类中interface中声明的变量和方法

我们定义一个父类CalssA，它在interface中有变量x和方法initVar。

``` objc
@inteface ClassA : NSObject
{
  int x;
}

- (void) initVar;
@end

@implementation ClassA
{
  int y;
}
- (void) initVar {
  x = 100;
  y = 101;
}
@end
```

我们再来定义一个子类ClassB，继承自ClassA，在ClassB中增加一个方法printVar来打印变量。

``` objc
@interface ClassB : ClassA 
- (void) printVar;
@end

@implementation ClassB
- (void) printVar {
  NSLog(@"x = %i", x);
  // NSLog(@"y = %i", y); // error
}
@end
```

子类只能访问父类中interface中声明的变量x，像implementation中的y变量在子类中是不能访问的。子类ClassB自动继承了ClassA中的initVar方法，是可以直接访问的，我们看main方法中的调用。

``` objc
int main (int argc, char *argv[]) {
  @autoreleasepool {
    ClassB *obj = [[ClassB alloc] init];
    [obj initVar];
    [obj printVar];

    return 0;
  }
}
```

## 如何找到正确的方法

这个很简单，当我们调用一个对象的方法时，先在这个对象的类中找，如果找不到，就到父类中找，找不到就再往父类的父类中找，直到找到为止。这里需要注意的一点是，OC也是单继承，每个类只有一个父类，所以在这个唯一的父类中找即可。这里还有另一个需要注意的点是，现在我们还没学“分类（category）”，在学完分类后，这个查找过程其实还有一个在分类中查找的过程。