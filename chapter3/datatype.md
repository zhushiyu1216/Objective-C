# OC数据类型
OC的数据类型分为基本数据类型和对象型的数据类型，基本类型是int，float, char, BOOL, double等，对象型的数据类型就是class了，但一般它都是指针，或者可以用id表示。同时，我们在打日志或者用format构造字符串对象时，要用%xx这种形式来占位，那各种类型要用哪些符占位呢？这一节我们都来讲解一下。

## int
这个是大家最熟悉的基本数据类型了，整数。需要注意的是，int占用的内容是几个字节，或者说占几位（0 1），是由计算机来决定的，32位的cpu机器，int占4字节，64位机器占8个字节。占用字节数不同，可以表示的数据范围也不同。

NSLog中，int使用“%i”来占位。

## float和double
float和double都是表示小数，只是两都的精度和可表示的数据范围不一样，double占用字节数是float的两位，可以表达的数范围也是float的两倍。

NSLog中，float用“%f”占位，double使用“%g”占位。

```
float f = 331.79;
NSLog(@"f = %f", f);
```

上边的这个代码打印的结果是`f = 331.790009`，我们看，打印出来的结果并不是331.79，这就是因为float有精度，要使用宽度限制一下，你可以试一下`%.2f`来占位试试。

## char
char表示一个字符，使用单引号表示，如：`char c = 'a';`，正常情况下字符只有一个，但一些特殊字符需要使用转义符，即反斜杠，来表示，如：`char c = '\n'；`。

这里要了解到，字符、字符串、字符串对象的区别，字符就是单引号引起来表示；字符串实际上是字符串数组，或者字符串指针，用双引号表示，如：`char *str = "abcdef";`；字符串对象实际上NSString，它是一个OC对象，属于对象数据类型，要用“@”号修饰，如：`NSString *str = @"abcdef";`。

在NSLog中，char使用“%c”占位，字符串使用“%s”占位，字符串对象使用“%@”占位。


## 限定词long short unsigned
对于int，可以使用一些限定词的指定int的长度或者是否有符号（即正负数）。  
long int / long long int：加长int长度；  
short int：减少长度；  
unsigned int: 无符号，即只有正数，无符号int可以让变量表示的整数增加一倍；

NSLog中，如果有long修饰，则占位符也需要添加“l”；如果有unsigned修饰，则占位符需要添加“u”；

## 对象类型
对象类型指的就是类了，在OC中，class类型的变量必须使用指针，表示方式为： 

ClassName *var;

```
NSString *str;
```

这种表达方式我们应该也很熟悉了。

NSLog中，对象型变量使用“%@”来占位，不过需要注意的是，要想使用“%@”占位，在类的implementation中需要重写NSObject（所有类的最终父类）description属性的get方法，如：

```
@implementation Fraction

- (NSString *) description {
  return [NSString stringWithFromat: @"I am fraction"];
}
@end
```

## id类型
id类型也是非常重要的，它也是表示class的数据类型，当你不知道某个class的具体类名是什么时，就可以使用id来声明class类型的变量，需要注意的是，id默认就是指针，不用再使用“*”号声明变量了，如：

```
id graphicObject;
```

这是OC不同于C的地方，需要多注意。id也是OC实现多态和动态类型、动态绑定的基础。

## 基本数据类型的NSLog占位符
我们最扣使用一个表格来列举一下各种类型的占位坐，如果忘了的时可以来快速查询。

| 类型 | 占位符 |
| ---  | --- |
| char | %c |
| short int | %hi、%hx（十六进制）、%ho（八进制）|
| unsigned short int | %hu |
| int | %i、%x、%o |
| unsigned int | %u |
| long int | %li、%lx、%lo |
| unsigned long int | %lu |
| long long int | %lli、%llx、%llo |
| float | %f、%e、%g |
| double | %f、%e、%g |
| long double | %Lf、%Le、%Lg |
| id | %p |