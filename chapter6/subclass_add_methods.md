# 子类扩展新方法

子类一般都会有自己新的属性和能力，所以一般也会扩展一些新的方法，这在我们上一节的例子中有所展示。在子类中扩展方法实际上和在一般的类上定义新方法没有什么区别，我们专门把这一节列出来，主要也是为了让大家更加清楚的明白继承常做的两件事情：扩展方法、覆盖方法。

这一节会讲一个继承的例子。我们在开始时接受一个任务，写一个矩形类，包含宽、高属性和获取面积及周长的方法。

``` objc
@interface Rectangle : NSObject

  @property int width, height;

  - (void) setWidth: (int) w andHeight: (int) h;
  - (int) area;
  - (int) perimeter;
@end

@implementation Rectangle
  @synthesize width, height;

  - (void) setWidth: (int) w andHeight: (int) h {
    width = w;
    height = h;
  }

  - (int) area {
    return width * height;
  }

  - (int) perimeter {
    return 2 * (width + height);
  }
@end
```

后来要实现一个正方形的类，它实际上就是一个特殊的矩形，面积和周长都可以重用，所以我们可以写一个子类，扩展出setSide和side方法。

``` objc
@interface Square : Rectangle {
  - (void) setSide: (int) side;
  - (int) side;
}

@implementation Square {
  - (void) setSide: (int) side {
    [self setWidth: side andHeight: side];
  }

  - (int) side {
    return self.width;
  }
}
```

在setSide方法中调用了父类的setWidth: andHeight方法实现边长的存储。

如果你对继承的特性比较了解，你会在感觉到有点别扭，似乎在这种情况下使用继承并不是一个最好的选择，因为在Square中可以访问到宽和高等属性，用组合的方式似乎更好。的确，使用继承可以让我们复用大量的代码，可以少写很多代码。但很多情况下使用组合反而让类的定义更加清晰，不过代码会增加不少，每个共有的方法都要重新定义，父类定义了新方法也不能直接使用。

从软件设计的角度看，能使用组合的情况下，建议优先使用组合。