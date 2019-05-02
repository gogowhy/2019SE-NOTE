# Linker 
## .symtab 分类
如下图，符号类型包括三种：local、global、external。它们分别对应的变量类型和作用域也如图中所示，在函数体内声明的变量叫做局部变量，函数体外声明的变量叫做全局变量。不加static修饰的局部变量运行时由栈管理是不被包含在.symtab表中的，static修饰的局部变量和static全局变量作用域都是单个文件，是作为local符号包含在.symtab中的。而不加static修饰的全局变量的作用域为全体文件，如果在本文件中是作为global符号，如果在别的文件中就是external符号。

![.symtab作用图](https://github.com/gogowhy/2019SE-NOTE/blob/master/IMAGES/ICS/symtab_effect.jpg)

## .bss .data COMMON
COMMON：未初始化的全局变量

.bss：未初始化的静态变量，以及初始化为0的全局或静态变量

.data：初始化的全局变量

## .rel.data .rel.text
参考：[ELF重定位 - kernweak的博客 - CSDN博客](https://blog.csdn.net/youyou519/article/details/82699670)
对代码和变量的重定位入口
````c
typedef struct
{
	Elf64_Addr r_offset;
	Uint64_t r_info;//（里面有sumbol和type）
	int64_t r_addend;
}Elf64_Rel;
````
Offset: 需要被修改的引用的节偏移

Symbol：被修改引用应该指向的符号

Type：如何修改新的引用

addend：偏移调整

### R_X86_64_PC32相对重定位
他的计算方式是“S+A-P”的方式重定位目标。

S是所以位于重定位条目中0符号的值（比如真正函数定义的地址）。
A是重定位条目中的加数。（比如补齐4字节）。

P是要进行重定位（使用r_offset进行计算）的存储单元的地址（节偏移或者地址）。（比如就是call之后的函数地址）

所以要将一个偏移量计算成虚拟地址，可以利用下面公式：
address_of_call（这个就是call这条指令的地址了，不是call后的地址）+offset+5(5是调用指令的长度)

用下面的计算也可以将一个地址转换成偏移量：
address-address_of_call-4(4是调用指令立即操作数的长度，为32位）



r.offset：0xf 偏移量

r.symblo= sum

r.type=R_X86_64_PC32

r.addend=-4 修正量

假设ADDR(s)=ADDR(.text)=0x4004d0 就是这段程序最开始的地址

ADDR(r.symbol) =ADDR(sum)=0x4004e8     就是我们想要调用的函数sum的地址（又叫sum重定位到的地址）

运行时地址：refaddr=ADDR(s)+r.offset     就是这段程序执行到这条指令的地址（又叫重定位引用地址）

更新这个指向，让它运行时指向程序sum：*refptr=(unsigned)(ADDR(r.symbol)+r.addend-refaddr)    就是我们想要调用的函数sum的地址+偏移量-程序执行到这条指令的地址（又叫重定位引用值）



 
### R_X86_64_32绝对引用

r.offset：0xa 偏移量

r.symbol= array

r.type=R_X86_64_32

r.addend=0

假设ADDR(r.symbol)=ADDR(array)=0x601018 我们要调用的array的地址
那么*refptr=(unsigned)(ADDR(r.symbol)+r.addend)  调用的这个地址+偏移量 就是绝对引用