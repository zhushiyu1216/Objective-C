# 选择结构
选择结构又叫条件语句，条件语句我们平时使用的比较多，大家应该也都会比较熟悉，我们这里只做一下汇总。

## if 语句
*if (条件) {*  
*&nbsp;&nbsp;执行语句*  
*}*  

``` objc
int number;
scanf("%i", &number);
if (number < 5) {
  NSLog(@"number is too less");
}
```

## if else语句
*if (条件) {*  
*&nbsp;&nbsp;执行语句*  
*} else {*  
*&nbsp;&nbsp;执行语句*  
*}*

``` objc
int number;
scanf("%i", &number);
if (number < 5) {
  NSLog(@"number is too less");
} else {
  NSLog(@"number is %i", number);
}
```

## 复合条件的逻辑运行符
``` objc
int number;
scanf("%i", &number);
if (5 < number && number < 15) {
  NSLog(@"number is too less");
}
```

## else if 语句
*if (条件) {*  
*&nbsp;&nbsp;执行语句*  
*} else if (条件) {*  
*&nbsp;&nbsp;执行语句*  
*} else {*  
*&nbsp;&nbsp;执行语句*  
*}*  

``` objc
int number;
scanf("%i", &number);
if (number < 5) {
  NSLog(@"number is too less");
} else if (number < 10) {
  NSLog(@"number is %i", number);
} else {
  NSLog(@"number is big, %i", number);
}
```

## switch语句
```
switch (表达式) {
  case value1:
    执行语句;
    break;
  
  case value2:
    执行语句;
    break;
  
  default:
    执行语句;
    break;
}
```

这里要注意case语句的执行顺序，在匹配到第一个等于`表达式`的case时开始执行，直到遇到break语句，或者到switch的结束大括号。

## 条件运算符

*条件 ? 语句1 : 语句2；*

这是一个快速的条件运算符，一般还有返回值；

``` objc
int number;
scanf("%i", number);
NSString *result = number < 10 ? @"little" : @"big";
NSLog(@"result is %@", result);
```