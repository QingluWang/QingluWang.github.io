---
layout	:	post
title	:	C++浅复制与深复制
---
*在谈C++浅复制与深复制之前，先谈谈复制构造函数。*

## 复制构造函数

与类中的构造函数、析构函数类型差不多，在你未显式地调用复制构造函数时，并执行一些与复制构造函数相关的操作时，编译器会隐式地生成一个复制构造函数，该函数简单地关联了所有类成员。

一般以下3种情况会用到类的复制构造函数:
<blockquote>
1.对象作为参数，以按值传递的方式传入一个函数；<br>

class a{……};<br>

void test(a temp){……}<br>

2.对象作为返回值，以按值传递的方式从一个函数返回；<br>

class a{……};<br>

a test(){a temp;……return temp;}<br>

3一个对象给另一个对象赋值初始化;<br>

class a{……};<br>

a temp;<br>

a temp2 = temp;<br>
</blockquote>
## 浅复制与深复制

简单来说，在类中存在指针时，浅复制仅仅是将该指针变量的值，即一个地址复制了，并没有将该地址指向的内存缓冲区的内容复制；深复制则是都复制了

下面举个例子：

类a定义

类b定义

类外两个函数

主函数中调用

`a mystringA(“Hello”);`

`usingStringA(mystringA);`

出现错误，而执行以下代码没有问题

`b mystringB(“World”);`

`usingStringB(mystringB);`


原因：
<blockquote>
编译器对于整型、字符和原始指针等POD数据，执行二进制复制，并不深复制指向的内存单元。<br><br>
a中由于按值传递后执行析构函数释放buffer指向的内存单元，所以usingStringA函数里使用的浅复制来的对象temp的buffer指针指向了无效的内存单元，无法输出”Hello”,导致错误；<br><br>
b中是重载了复制构造函数，使它按值传递时，usingStringB函数里复制来的对象temp的buffer指向了一片新的内存空间，例子里，这片存储空间存的就是”World”。
</blockquote>