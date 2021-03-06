# 专题：c语言如何建立一个自己的库

[^参考]: 《脑洞大开C语言另类攻略》刘隽良编著，西安电子科技大学出版社

[TOC]



### 首先，回忆起自己写程序的时候，要添加头文件

#### 了解#include的作用：使你可以引用其中声明的函数

举个例子，用scanf和printf需要添加<stdio.h>这个头文件，编译器会自动在编译时将这个库编译进去，也就是我们所说的**预处理**阶段。

### 其次，从#include<stdio.h>和#include“stdio.h”的区别认识到系统自带的库和自己建的库

因为#include<stdio.h>直接去系统默认库里面去找，#include“stdio.h”优先在程序的本地目录搜索这个文件，找不到再搜索系统目录。所以前者更适合自带库，后者更适合编程者自己写的库。

### 然后，总结一下头文件，接口还有库之间的关系

一句话解释：要写**库**的话，就要有.h这种头文件作为**接口**；而.h这种**头文件**另外一个作用就是防止重复引入。

啥？怎么重复引用了？引用了啥？   嘻嘻，就是自己写库的时候，打个比方，要用scanf这样的函数，就要加上一句#include<stdio.h>。也就是说，自己写的库函数文件可以引用其他的库。

那，如何实现头文件防止重复引入这个机制的呢？

用#ifndef这个宏定义进行判断

```c
#ifndef _STDIO_H_//先判断当前文件中是否已经宏定义过_STDIO_H_，若没有则执行下面的语句
#define _STDIO_H_
.
.
.
#endif//若有，则直接跳到这里来
//和if关键字很像
```

#### .h头文件的一般格式

```c
#ifndef<标识>//<标识>是当前头文件名的全大写形式，并将‘.’换成‘_’,且在文件名前后各加'_'
#define<标识>
	(这里写头文件的内容)
#endif
	(这里写如果引入过头文件的操作，一般是没操作)
```

### 最后，动手操作写一个库试试（一个例子）

#### 1.编写一个.c文件

```c
#include<stdio.h>
void More(int num){
    int i;
    for(i=0;i<50;i++){
        num++;
        printf("%d",num);
    }
}
//存为.c文件
```

#### 2.编写.h头文件

```c
#ifndef _MORE_H_
#define _MORE_H_
 void More(int num);
#endif
```

#### 3.将编写好的.h文件包含到.c文件里面去

```c
#include<stdio.h>
#include "More.h"
void More(int num){
    int i;
    for(i=0;i<50;i++){
        num++;
        printf("%d",num);
    }
}
```

#### 特别注意，将这个库的文件和库函数文件放在同一个工程目录下

至于怎么写.c文件和.h文件，又在哪里写.c文件和.h文件，不晓得

这里有一个手把手教的例子：

http://blog.csdn.net/bbs375/article/details/52668322