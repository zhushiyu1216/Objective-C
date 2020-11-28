
# 子类覆盖父类的方法

如上一节所说，继承常做的两件事：扩展方法和覆盖。继承不能减少或都删除父类的方法，但可以覆盖重写父类在interface中声明的方法。之前我们也提到了OC查找要调用的方法的路径，先在本身的类中查找，找到后就直接调用了。这就为我们覆盖父类方法提供了可能。

同样看我们第一节中的ClassA和ClassB。

``` objc
@interface ClassA : NSObject 
{
  int x;
}

- (void) initVar;
@end

@implementation ClassA 

- (void) intVar {
  x = 100;
}
@end
```

我们在子类ClassB中重写initVar方法：

``` objc
@interface ClassB : ClassA 

- (void) printVar;
@end

@impelementation ClassB

- (void) initVar {
  x = 200;
}

- (void) printVar {
  NSLog(@"x = %i", x);
}
@end
```

在main中调用一下看看x的值：

``` objc
int main (int argc, char *argv[]) {
  @autoreleasepool {
    ClassB *obj = [[ClassB alloc] init];
    [obj initVar];
    [obj printVar];
  }
}
```

此时ClassB实际上有一个x变量，两个方法initVar和printVar可用。

## OC中的抽象类

如果你是一个Java程序员，你可能会有两个疑问：OC中有final这样的防止类或方法被继承关键字吗？OC中有abstract这样的专门用于抽象类的声明吗？

第一个问题的答案是没有，OC中是不能防止类被继承的。

第二个问题的答案也是没有，但这个问题倒是有一些讨巧的解决办法，对于必须要求子类中继承的方法抛出异常来强制要求子类覆盖重写。如：

``` objc
@interface Person : NSObject
- (void)home;
@end

#define MethodNotImplemented() \
    @throw \
    [NSException exceptionWithName:NSInternalInconsistencyException \
                            reason:[NSString stringWithFormat:@"You must override %@ in a subclass", NSStringFromSelector(_cmd)] \
                          userInfo:nil]

@implementation Person 
- (void) home {
  MethodNotImplemented();
}
@end
```