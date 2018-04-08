# 专题：C语言的关键字

[^参考]: 《脑洞大开C语言另类攻略》刘隽良编著，西安电子科技大学出版社

[TOC]



## 一 auto



## 二~九 基本数据类型以及signed和unsigned



## 十 sizeof

### sizeof()的两种应用

#### 1.主要功能：计算变量所占内存的长度

#### 2.常用方法：计算数组长度（计算字符串长度）



## 十一~十五 if和else；do,while,for

值得注意的是浮点数据的比较，只能直接比较'<'或者'>',对于‘!=’和'=='直接比较是不行的，得转成精度。

原因:浮点型变量的标准定义是，在与0相差一定精度内的浮点数均可视作零值

```c
double num=0;
if(num==0.0);//隐含错误的比较
//转化为
if((num>=-EPSINON)&&(num<=EPSINON));//EPSINON即为允许的误差
```

## 十六~十八（循环三剑客）break、continue、goto

goto的示例

```c
void function(){
    int flag=0;
	jump:
  	  flag++;
      if(flag<9)goto jump;
}
```



## 十九~二十一 switch和case、default

case只能是整型或者字符型的常量或常量表达式（作者说“这三者都存在于内存区的文字常量区，生存期很长，不会像其他东西那样容易被销毁，这样可能可以使得程序错误率降低”）

## 二十二“只进不出”const

const定义的变量从某种程度上已经不算是变量了，叫只读变量。

只读类型的变量是不能更新的，一旦被设定，就不能轻易改变

## 二十三 “外籍”extern

extern修饰的变量或函数来自同一工程的其他文件

全局变量是“本文件内可用，整个工程内可见”，如果需要全局变量在本工程其他文件内可用，则需要extern.

归根结底，extern是一种声明，它对于被声明的变量是一种引用关系

## 二十四 static（静态）

第一个作用，修饰变量，被修饰的变量又分为局部变量和全局变量，但他们都存在内存的静态区。（因为被保存在静态区，所以不会被销毁）

静态全局变量，作用域仅存限于变量被定义的文件中，其他文件即使用extern也不行。而对于本文件，作用域也只是从被定义处到文件的结尾；在定义处之前的同文件代码也不能使用，但是（鉴于是同文件，总得给点优惠嘛~）可以在静态全局变量之前加上extern.

综上，我们在定义静态全局变量时，直接在文件顶端定义。

第二个作用，修饰函数。函数加了静态，那么这个函数只能在本文件内使用（所以又称这种函数叫内部函数）.

## 二十五（集结关联）struct

*为每一个伙伴都配置了一个房间*

## 二十六（联合体）union

*所有的伙伴共用一个房间，每次只能有一个伙伴用（每次只有一个数据成员的数据是有效的）*

“大小是最胖的成员的那个尺寸”，即

大小足够容纳位宽最宽的成员；

大小能被其包含的所有的基本数据类型的大小整除

union相较于struct，主要是用来压缩空间，如果一些数据不肯呢过同时被用上，那么union很有用哦！

（先写到这里，反正还没用到）

## 二十七（枚举）enum

主要用法，替代宏定义。

只支持整数类型

## 二十八 typedef

给一个已经存在的数据类型取一个别名。如

```c
typedef int num1,num2;

//定义了两个新的数据类型num1，num2，在编译器眼里都是整型。

```

```c
typedef struct{
    char name[20];
    int id;
}student;
student st1;
//student就完全等价于上面那个结构体
struct student{
    char name[20];
    int id;
};
struct student st1;
//这里要多写一个struct
```

```c
//#define与typedef的第一个不同
#define IntPtr int*
typedef int* Iptr;
IntPtr p1,p2;//等价于 int* p1,p2;
Iptr p3,p4;//等价于 int *p3,*p4;
//#define只是简单地常量替换


//#define与typedef的第二个不同，修饰指针的作用域不同
#define IntPtr int*
typedef int* Iptr;
const IntPtr p1;//相当于const int*p1,或者 int const *p1, p1可以更改指向，但被p1指向的地址里面的内容不能更改
const Iptr p2;//相当于int *const p2, p2可以更改指向的地址里的内容，但p2的指向不能更改
//说了这么多还是不懂，到底怎么看const修饰的是谁啊？？？？把数据类型先去掉
//即，const *p1（内容不可修改）和*const p2(指向不可修改)
```

## 二十九~三十 volatile和register

## 三十一~三十二void和return

## 三十三~三十七（C99新定义了五个）

###  restrict, inline,_Complex, _Imaginary, _Bool



### 





