# 方法中分配对象

在写程序时，我们有很多原则需要遵守，像单一职责原则、依赖倒置原则等，这其中有一个重要的原则叫“开放-封闭原则”，它的意思是说软件实体(类，模块，函数等等)应该可以扩展，但是不可修改。

这句话是什么意思呢，我们还拿Fraction这个类来举例，我们执行加法运算时，运算后返回一个分数，如果我们把当前的Fraction返回，则被调用者持有后可能会对我们当前的Fraction进行修改，这就违反了封装的原则，需要我们创建一个新的Fraction返回，如：

``` objc
- (Fraction *) add: (Fraction *f) {
  Fraction *result = [[Fraction alloc] init];
  result.numerator = numerator * f.denominator + denominator * f.numerator;
  result.denominator = denominator * f.denominator;

  return result;
}
```

我们在方法内创建了一个对象，那由谁来释放呢？放心，只要你使用ARC进行编译，编译器会自动为你添加计数，在不使用时自动回收。