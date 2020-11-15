# 循环结构

## for语句
*for ( 初始化表达式; 继续循环条件; 循环一次后的执行语句)*
*&nbsp;&nbsp;循环体语句;*
``` objc
int sum = 0;
for (int n = 1; n <= 100; n++) {
  sum += n;
}
NSLog(@"sum = %i", sum);
```

## while语句
*初始化语句*
*while ( 循环条件 ) {*
*&nbsp;&nbsp;循环体;*
*}*

``` objc
int n = 1;
int sum = 0;
while (n <= 100) {
  sum += n;
  n++;
}
```
我们举一个最大公约数的例子，这个例子后面的课程中也会用到。下面是百度百科上计算最大公约数的方法的介绍：

> 辗转相除法
辗转相除法：辗转相除法是求两个自然数的最大公约数的一种方法，也叫欧几里德算法。
例如，求（319，377）：
∵ 319÷377=0（余319）
∴（319，377）=（377，319）；
∵ 377÷319=1（余58）
∴（377，319）=（319，58）；
∵ 319÷58=5（余29）
∴ （319，58）=（58，29）；
∵ 58÷29=2（余0）
∴ （58，29）= 29；
∴ （319，377）=29。
可以写成右边的格式。
用辗转相除法求几个数的最大公约数，可以先求出其中任意两个数的最大公约数，再求这个最大公约数与第三个数的最大公约数，依次求下去，直到最后一个数为止。最后所得的那个最大公约数，就是所有这些数的最大公约数。

``` objc
int number1, number2;
NSLog(@"please input number1:");
scanf("%i", &number1);
NSLog(@"please input number2:");
scanf("%i", &number2);

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

NSLog(@"最大公约数是:%i", less);
```

## do 语句
*初始化语句*
*do {*
*&nbsp;&nbsp;循环体;*
*}*
*while ( 循环条件 )*

do语句先执行后判断条件，所以循环体至少会执行一次。

``` objc
int number = 0;
do {
  NSLog(@"number = %i", number);
  number++;
} while (number < 10)
```

## break语句
在执行过程中如果要跳出循环，直接执行break语句即可。

``` objc
int number = 0;
while (number++ < 10) {
  NSLog(@"number = %i", number);
  if (number > 5) {
    break;
  }
}
```

## continue语句
在执行循环体过程中，如果想跳出本轮循环，可以使用continue语句。

``` objc
int number = 0;
while (number++ < 10) {
  NSLog(@"number = %i", number);
  if (number > 5) {
    continue;
  }
  NSLog(@"本轮循环 complete");
}
```