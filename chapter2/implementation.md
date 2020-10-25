# @implementation
implementation是对interface声明的方法进行定义，如果你写的是一个SDK或类库，这部分是不是公开给使用方的。implementation部分的定义如下：

``` objc
#import "NewClassName.h"

@implementation NewClassName
{
  memberDeclarations;
}

methodDefinitions;
@end
```

1、@implementation部分一般会写在一个独立文件中，所以开头部分要引用一下头文件`#import xxx.h`；  
2、@implementation后间隔一个空格，跟着要实现的类名，这里不用再写父类的名称了；  
3、memberDeclarations部分用于声明我们要使用的变量，注意，这里跟interface中声明的属性不是一回事儿，这里声明的变量只供类实现部分使用，不对外公开；  
4、methodDefinitions部分用于定义方法，它可以有两类方法，一类是interface头文件中声明的方法，这些方法是必须实现的，且对外公开，另一类是供implementation类定义使用的，这些方法是不公开的；  
5、实现部分在`@implementation`开头，以`@end`结束；  

如果Fraction类中我们没有使用属性，则分子和分母就需要在implementation中自己定义成员变量了，如： 

``` objc
@implementation Fraction
{
  int _numerator, _denominator;
}

- (void) setNumerator: (int) numerator andDenominator: (int) denominator {
  _numerator = numerator;
  _denominator = denominator;
}
@end
```

注意，方法内，OC不能区分出成员变量与参数变量，为了便于区分，成员变量尽量以下划线开头；

