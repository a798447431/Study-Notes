# C语言笔记

## 19. 4 .16 

### 1.三种输出输出方式

1. **printf--->scanf**

2. **sprintf--->sscanf**　　

3. **fprintf--->fscanf**　

   



### 2.三种printf()简介

#### (1) printf

printf()是C语言标准库函数，用于将格式化输出输出到**标准输出**。
    
标准输出，即标准输出文件，对应着终端的屏幕。printf申名于头文件stdio.h。
    
**函数原型：**

```c
int printf ( const char * format, ... );
```

​    **format** -- 这是字符串，包含了要被写入到标准输出 stdout 的文本。

**返回值：**

​    如果成功，则返回写入的字符总数，否则返回一个负数。



#### (2) sprintf()

与printf()函数类似，用于将格式化输出输出到**所指向字符串**中。

**函数原型：**

```c
int sprintf(char *str, char *farmat [,argument,...]);
```

- **str** -- 这是指向一个字符数组的指针，该数组存储了 C 字符串。
- **format** -- 这是字符串，包含了要被写入到字符串 str 的文本。

**返回值：**

​    如果成功，则返回写入的字符总数，不包括字符串追加在字符串末尾的空字符。如果失败，则返回一个负数。



#### (3) fprintf()

与printf()函数类似，用于将格式化输出输出到**流/文件**中。

函数原型：

```c
int fprintf(FILE *stream, const char *format, ...)
```

- **stream** -- 这是指向 FILE 对象的指针，该 FILE 对象标识了流。
- **format** -- 这是 C 字符串，包含了要被写入到流 stream 中的文本。

**返回值：**

​    如果成功，则返回写入的字符总数；如果失败，则返回一个负数。





### 3.三种scanf()简介

#### (1) sacnf

scanf()是C语言标准库函数，用于**执行格式化输入** 。

**函数原型：**

```c
int scanf(const char *format, ...)
```

**format** -- 这是 C 字符串，包含了以下各项中的一个或多个：*空格字符、非空格字符* 等*。

**返回值：**

​    如果成功，该函数返回成功匹配和赋值的个数。如果到达文件末尾或发生读错误，则返回 EOF。



#### (2) sscanf()

从字符串**读取格式化输入**。

**函数原型：**

```c
int sscanf(const char *str, const char *format, ...)
```

- **str** -- 这是 C 字符串，是函数检索数据的源。
- **format** -- 这是 C 字符串，包含了以下各项中的一个或多个：*空格字符、非空格字符* 等。

**返回值：**

​    如果成功，该函数返回成功匹配和赋值的个数。如果到达文件末尾或发生读错误，则返回 EOF。



#### (3) fscanf()

用于将格式化输入输入到**流/文件**中。

函数原型：

```c
int fscanf(FILE *stream, const char *format, ...)
```

- **stream** -- 这是指向 FILE 对象的指针，该 FILE 对象标识了流。
- **format** -- 这是 C 字符串，包含了以下各项中的一个或多个：*空格字符、非空格字符* 等。

**返回值：**

​    如果成功，该函数返回成功匹配和赋值的个数。如果到达文件末尾或发生读错误，则返回 EOF。



---

**重点：**

``` 
while(scanf("%d", &n) != EOF) == while(~scanf("%d", &n)) //EOF = -1, ~取反
```

二进制负数等于整数各位取反，末位加一

二进制-1为0的二进制减1, 为11111111(八位)，因为每一位上前进位，符号位为１。

有的二进制只能表示负数，不能表示正数，如10000000(2)为-128,　正数只能表示到127。



##  19. 4 .18

 ### 位运算

### 非常重要！！！！ 位运算位与位之间相互独立，不互相影响！！！！！

位运算符号有**& , |  ,  ^ ,  ~ , <<,  >>**等。

#### 移位运算 >> , << 

**<<** 左移末位补0,  **乘2**

**>>** 右移开头补符号位,  **除2**

```c
1111 1111(-1)
1111 1110(-2) >> 1 = 1111 1111 (-2 / 2 == -1)
```

负数右移最大值为**-1**  (1111 1111)

#### 异或运算 ^ 

a ^ b = c  --> **异或运算是自己的逆运算**

**异或运算的三个数，已知任意两个数可以得到第三个数**

```c
#include<stdio.h>

int main() {
    int a = 2, b = 7, c;
    c = a ^ b;
    printf("c = %d\n", c);
    printf("a = %d\n", c ^ b);
    printf("b = %d\n", c ^ a);
    return 0;
} 

```

```c
结果：
c = 5
a = 2
b = 7
```

**异或运算本质：** **判断相关二进制位上“1”的奇偶性**

 a    ^   b  =    c

 奇      奇       偶
 奇      偶       奇
 偶      偶       偶

### 与运算 &
& 可简单看做二进制位间的乘法

### 或运算 |
| 可简单看做二进制位间的加法



### 数学函数
一般数学函数都存在math.h头文件中, 而abs(n)比较特殊, 存在stdlib.h头文件中, 作用为输出整型绝对值
acos(n)函数 输入的参数与返回值均为弧度制，acos(-1)的值为π
可以利用**换底公式和log10()函数**来求以任何数为底的对数，比如以2为底的对数函数：**logxN / logx2 = log2N**

C语言gcc编译时引入数学函数库：

```
gcc code.c -lm (lm即为数学函数库，加在文件名后面)
```

**int (32位) (4字节)    long long(64位) (8字节)   short int (16位) (2字节)   char (8位) (1字节)**

**1字节 = 8位二进制数(位bit)**

c99后引入了头文件 **inttypes.h**

int8_t	int16_t	int32_t	int64_t

这样定义可以防止不同编译环境下int等占用字节数不同，可移植性强。

输出方式：

```c
int16_t
scanf("%" PRId16 "\n", &a);
```

PRI可以看做"hhd, hd, d, ld, lld"等字符串。

```c
"%" "hd" ==> "%hd"
```

INT64_MAX(MIN) 查看最大(小)值。



### " = "

" = "  并不靠左右位置来区分为左值和右值。

左值：" = " 运算后依旧可以被我们获取到的值

右值：" = " 运算后不能被我们获取到的值，比如运算过程中的值，只是个临时变量，无法被输出。

```c
#include<stdio.h>
int main() {
    int a = 3, b = 7, c = 10, d = 4, e = 5;
    a = ++(4 + 3); //错误，4 + 3的计算结果是一个临时变量，没法自增，为右值
    b = ++(c + d); //同上，c + d的值也由临时变量存储，无法自增，为右值
    c = ++d; //可以输出，因为d是一个被定义的变量，可以被我们所得到，为左值
    printf("%d %d %d", a, b, c);
    return 0;
} 
```



```c
错误提示：lvalue需要作为递增操作数
test.c: In function ‘main’:
test.c:12:9: error: lvalue required as increment operand
     a = ++(4 + 3); 
         ^~
test.c:13:9: error: lvalue required as increment operand
     b = ++(c + d); 
         ^~
```

**运算符优先级：**

**a + b + c  等加减乘除运算均为左结合**

**++，--，* 等为右结合**

不一定要都记住，但要看的懂！
[百度百科：运算符优先级](https://baike.baidu.com/item/%E8%BF%90%E7%AE%97%E7%AC%A6%E4%BC%98%E5%85%88%E7%BA%A7/4752611?fr=aladdin)

