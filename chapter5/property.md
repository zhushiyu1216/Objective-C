# 类的属性及访问
## @property属性定义
作为一个类，它可以定义一些自己的成员变量来存取自己的属性，如Person这个类，你可以定义这个类的“性别、年龄、身高”等属性。在面向对象编程中，我们还有一个封装的编程原则，就是说我们不能直接访问这些变量，而要通过这些变量的get和set方法来访问及赋值，这也是为什么我们在类的头文件内只能定义方法。

通常，对于成员变量的get和set方法的命名形式为，get方法即成员变量名，set方法命名为`set+变量名`。如：

``` objc
@interface Person : NSObject
  - int age;
  - void setAge: (int) a;
  - void print;
@end
```

在头文件定义完成后，在实现文件中还要对这些方法进行实现，而要想实现这些方法，我们又要定义一个成员变量，如下：

``` objc
@implementation Persion
{
  int age;
}
  - int age {
    return age;
  }
  - void setAge: (int) a {
    age = a;
  }

  - void print {
    NSLog(@"person's age = %i", age);
  }
@end
```

这样定义我们需要写很多代码，而这些代码也是有一定的规则，所以OC将属性的写法进行了简化，它给了一个`@property`命令来帮我们实现上面所有的代码，如：

``` objc
@interface Person : NSObject

@property int age;

- void print;

@end
```

我们再看看类的实现文件中怎么写的：

``` objc
@implementation Persion

- void print {
  NSLog(@"person's age = %i", _age);
}
@end
```

注意这里使用的变量是`_age`，这是因为使用@property后，编译器会自动帮我们生成一个带下划线的同名变量。如果想使用和property内声明的名字一样的变量怎么办呢？OC也提供了方法的，可以在implementation中使用@synthesize命令进行合成，如下：

``` objc
@implementation Persion

@synthesize age;

- void print {
  NSLog(@"person's age = %i", age);
}
@end
```

这时就可以直接使用同名变量的。

这里一定要注意，此时编译器帮我们已经实现了get set方法，如果要重写覆盖这些方法，我们只需手工定义即可。

## 类属性的访问
OC的属性访问有两种形式，一种是`.`的形式，一种是用方法的访问形式，我们先看看如何使用。

先看使用`.`的形式：

``` objc
Person *person = [[Person alloc] init];
// 获取，即get
NSLog(@"age = %i", person.age);
// 赋值，即set
person.age = 15;
```

再看看使用方法的访问形式：

``` objc
Person *person = [[Person alloc] init];
// 获取，即get
NSLog(@"age = %i", [person age]);
// 赋值，即set
[person setAge: 15];
```

从上边两个使用形式可以看出，使用`.`的访问形式明显更加简便，所以，我们在写代码的过程中也推荐使用`.`的形式来访问属性。

## 在类内访问属性
我们在类内部如何访问属性呢？这里大家记住几个原则：

+ 当使用了@synthesize合成后，直接使用属性名字，如：age = 15;
+ 当没有使用@synthesize合成，则使用带下划线的的变量名，如：_age = 15;
+ 如果没有使用@synthesize合成，也可以使用self.age这种形式来访问，实际上表示调用了get方法，调用方法的成本是高于直接访问变量的，如果没有特殊需要，一般不建议使用这种形式。
