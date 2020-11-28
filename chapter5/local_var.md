# 局部变量
本节继续结合Fraction类，给大家讲解一下什么是局部变量？方法参数的值是如何传递的？static关键字修饰局部变量时它的作用是什么？

## 什么是局部变量
局部变量就是在方法内声明的变量，我们还以上一章讲循环语句讲的求最大公约数的方法来看一下：

``` objc
- (int) findMaxDivisor: (int) number1 andNumber2: (int number2) {
  int bigger = MAX(number1, number2);
  int less = MIN(number1, number2);
    
  while (true) {
    int mod = bigger % less;
    if (mod == 0) {
        break;
    } else {
        bigger = less;
        less = mod;
    }
  }

  return less;
}
```

+ 这里的bigger和less都是在方法内定义的变量，这两个变量都是局部变量，它们只在方法内有效，出了方法后就无法访问了；
+ 这里的mod也是局部变量，它定义在while循环内，所以它只在while后的大括号内生效；所以这里有一个原则，局部变量只在它上边最近的一个大括号内有效；
+ 方法的入参number1和number2也是局部变量，它的生命周期和bigger一样，只在方法内有效。

## 方法参数的值是如何传递的

OC中方法的参数在传递时都使用的是值传递，即copy传递。这是什么意思呢？就是说方法内对入参进行修改，都不会影响传递进来的变量。我们先看一下基本数据类型的传递：

``` objc
int a = 10;
- (void) handleA: (int) b {
  b = 15;
}


[self handleA: a];
NSLog(@"a = %i", a);
```

这里a的值仍然是10，为什么呢？因为a在传参方法handleA时，会复制一份后赋值给b，此时b怎么改变都不会影响到a。

再看看对象类型的参数，我们以Fraction的add为实例看看：

``` objc
- (void) add: (Fraction *) a {
  a.numerator = 15;
}

// 我们调用一下看看
Fraction *f = [[Fraction alloc] init];
f.numerator = 10;

Fraction *f2 = [[Fraction alloc] init];
[f2 add: f];

NSLog(@"f.numerator = %i", f.numerator);
```

我们会发现，f.numerator打印出来的值已经变成了15，跟上面的基础类型不一样了，这又是为什么呢？大家注意add方法的参数为指针，此时在调用add方法时`[f2 add: f]`,将f这个指针的指向的地址复制后赋值给了方法的入参a，所以此时两个指针变量指向了同一个实际的对象，此时修改a，实际上修改的对象跟f指向的是同一个，这也是为什么修改一个，另一个也会变了。

那基本数据类型的参数也想在方法内修改，要怎么实现呢？此时要将参数也定义为指针类型，同时，在传递时使用变量引用，如：

``` objc
- (void) handle: (int *) a {
  *a = 15;
}

int i = 10;
[obj handle:&i];

NSLog(@"i = %i", i);
```

## static关键字修饰局部变量时它的作用是什么
static在修饰变量时，跟C是一样的，这个变量只被初始化一次，且在方法执行完后不会释放，下次进入后还可以继续使用。static修饰局部变量时，常用来计数，如我们想统计一下一个页面共展示了多少次:

``` objc
- (int) showPage {
  static int pageCount = 0;
  pageCount++;
  return pageCount;
}
```