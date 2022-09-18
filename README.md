# 3.1  C51编程语言简介

**概念**<br>
`C51语言`是在`标准C语言`的基础上，针对8051单片机的硬件特点进行扩展而形成的用于8051单片机编程的C语言。

 - `标准C语言`针对的是通用微型计算机。 `C51语言`面向的是MCS-51单片机。
 - 由于单片机的硬件资源与存储器结构，相较于通用微型计算机要贫乏的多。 <br>`C51语言`与`标准C语言`在总体上相同的同时,也有一些差别。
## 3.1.1 C51语言与8051汇编语言比较  
相同功能的两段程序。一段用C编写，一段用汇编语言编写。

```c
#inluce<reg51.h> //C语言
unsigned char a=0x00;
void main(void)
{
	IE=0X81;
	IT0=1;
	P2=0;
	while(1);
}
void int0(void) interrupt 0
{
	a+=1;
	P2=a;
}
```

```c
		ORG 	0000H   //汇编语言
		LJMP 	MAIN
		ORG 	0003H
		LJMP 	INT_0
		ORG 	0100H
MAIN:	SETB 	EA
		SETB 	EX0
		SETB 	IT0
		MOV 	R3,#0
		MOV 	P2,R3
HERE:	SJMP 	HERE
 		ORG 	0200H
INT_0:	CLR 	EA
 		PUSH 	PSW
 		PUSH 	ACC
 		INC 	R3
 		MOV 	P2,R3
 		POP 	ACC
 		POP 	PSW
 		SET 	EA
 		RETI
 		END
```
### 与8051汇编语言相比， C51有如下优点

- 可读性好。便于修改、维护。
 
    容易看懂，自然便于修改。
    
- 模块化开发与资源共享。减少重复劳动。
		
     标准C语言有丰富的库函数[^1]。其他程序员编写的优秀程序段。都可以拿来利用。
     
- 可移植性好。
 
  	C51编写的程序通过改写头文件以及少量的程序行，就可方便地移植到PIC单片机上。
  
- 生成的代码效率高。
 
 	较好的C51语言编译系统编译出来的代码，效率只比直接使用汇编语言低20%左右 
 
==较好的C51语言编译系统编译出来的代码，效率只比直接使用汇编语言低20%左右==  <br>
 ==标记文本==
[^1]:



