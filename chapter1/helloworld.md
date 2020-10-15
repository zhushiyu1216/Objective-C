# 第一个程序“helloworld”
正常创建一个项目后，项目会帮我们生成一个main.m文件，同时在里面有main函数，代码如下：

``` c
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // insert code here...
        NSLog(@"Hello, World!"); // 新增加的语句
    }
    return 0;
}
```
## 程序编写与解释
Hello world程序十分简单，只用一句代码输出“hello world!”即可，这句代码如下：

``` c
NSLog(@"Hello, World!"); // 新增加的语句
```

我们对hello world分析一下：  

``` c
#import <Foundation/Foundation.h>
```
引入OC的基础库，基本每个OC的程序都需要引入，引入后就可以使用OC提供的丰富多样的功能了。

``` c
int main(int argc, const char * argv[])
```
这句是不是很熟悉，对，就是C语言的入口函数。

```c
  @autoreleasepool {
  }
```
这一句也很必要，也是OC借鉴Java的JVM虚拟机垃圾自动收集机制，升级了内存管理，大大解放了程序员对指针的管理，编译器自动帮我们添加无用对象回收。当然，它的机制跟JVM不一样，JVM是运行时动态监测，OC是在编译时帮助我们添加对象回收代码。

``` c
NSLog(@"Hello, World!");
```
这一句是打印一个字符串，NSLog是Foundation库提供的打印方法，这也是我们学习OC过程中最常用到的方法，没有之一。再看字符串`@"Hello, World!"`，看看它和C的字符串有什么不一样，对，它多了个`@`，这个是OC的指定符，表示这是一个对象，从而后面的"Hello, World!"转化成NSString不可变对象。

## 如何打印变量

我们看一下如何将一个变量的值打全出来，比如我们计算一个加法，并打印出结果：

```
int sum;
sum = 50 + 25;
NSLog(@"sum = %i", sum);
```

跟C的printf类似，NSLog方法的第一个字符串参数中可使用%+标识，后面的参数传入变量，即可以打印出对应的值。

## 断点调试

在某个语句前面点击，即可添加上断点，点击运行，当代码运行到断点时，即可以XCode底部的Debug Area里看到对应的变量值，用法见视频。

[打赏](../include/donate.md ':include')