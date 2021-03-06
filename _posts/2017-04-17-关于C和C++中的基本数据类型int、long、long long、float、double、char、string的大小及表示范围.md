---
title: 关于C和C++中的基本数据类型int、long、long long、float、double、char、string的大小及表示范围
date: 2019-06-04 10:26:38
tags: CSDN迁移
---
   一、基本类型的大小及范围的总结（以下所讲都是默认在32位操作系统下）：  
 【单位描述】

 字节：byte

 位：bit

 1. 短整型short：

 所占内存大小：2byte=16bit；

 所能表示范围：-32768~32767；(即-2^15~2^15-1)

 

 2. 整型int：

 所占内存大小：4byte=32bit；

 所能表示范围：-2147483648~2147483647；(即-2^31~2^31-1)

 unsigned: 

 所占内存大小：4byte=32bit；

 所能表示范围：0~4294967295；(即0~2^32-1)

 

 3. 长整型long：

 所占内存大小：4byte=32bit；

 所能表示范围：-2147483648~2147483647；(即-2^31~2^31-1)

 unsigned long: 

 所占内存大小：4byte=32bit；

 所能表示范围：0~4294967295；(即0~2^32-1)

 注：上面所说的全部是有符号型的，short，int，long都默认为有符号型，其 中long和int都占4个字节的空间大小，他们有什么区别呢？

 16位操作系统：long：4字节，int：2字节

 32位操作系统：long：4字节，int：4字节

 64位操作系统：long：8字节，int：4字节 

 int型在不同位数操作系统中所占用的字节数不同，如果想编写可移植性好的程序，早年流行16位和32位操作系统时最好用long修饰int型，现在流行32位和64位操作系统，用int就挺多了。当然这些都看你怎么去理解它了，毕竟它 们在不同操作系统所占字节数不固定，所以各自都有其适用之处，不可定论其好坏。

 下面是对它 们的有科学依据的规定：

 C语言规定：无论什么平台都要保证long型占用字节数不小于int型, int型不小于short型。

 

 4. 字符型char：

 所占内存大小：1byte=8bit；

 所能表示范围：不确定！！！！；

 unsigned char：

 所占内存大小：1byte=8bit；

 所能表示范围：0~255；(0~2^8-1)

 singned char: 

 所占内存大小：1byte=8bit；

 所能表示范围：-128~127；(-2^7~2^7-1)

 char的默认类型不确定有可能是unsigned，也有可能是signed，主要更具编译器而定，可以自己测试一下编译器的默认char的符号类型。

 

 5. 布尔类型bool：

 所占内存大小：1byte=8bit；

 所能表示的范围：只能取两个值false或者true；所以最小值就是：0， 最大值：1.

 

 6. 单精度float： 

 所占内存大小：4byte=32bit；

 所能表示的范围：(1.17549e-038)~(3.40282e+038);

 注意：浮点数在 内存中都是按科学计数法来存储的，浮点数的精度是由尾数的位数决定的，大家记住即可不必深究；

 

 7. 双精度double：

 所占内存大小：8byte=64bit；

 所能表示的范围：(2.22507e-308)~(1.79769e+308);

 注：如何区分和使用这两个浮点类型呢，首先float和double的精度不同， float保留到小数点后面7位，而double保留到小数点后面16位，float能保证6 位有效数字，而double能保证15位有效数字，如果在不追求精度的的情况下当然用 float比较好，节省内存，如果需要很高的精度的情况下，最好还是用 double，平时我们定义浮点型变量一般都用double，毕竟精度高，一般精度 的损失是不能忽略的。

 

 8. 字符串string：由于string在c++中属于类类型，不是基本数据类型，类不能计算其在内 存中所占大小，非要用sizeof(string)来算的话，一般算出来的结果是 sizeof(string)=4byte，如果string字符串内容很多，很明显就不是其 真实大小，string类里面有计算其字节大小的函数如：size(),length()。

 感谢原作者的分享！  
 原文：https://blog.csdn.net/love_x_you/article/details/42846993   
 

   
 