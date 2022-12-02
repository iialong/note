# 课程笔记

## 《计算机系统基础》

### 1.1--为什么要学习计算机系统？

![image-20220828110250180](https://raw.githubusercontent.com/iialong/note/main/images/image-20220828110250180.png?token=A2XHUZHZBCARMBINPO4Q563DBLNR4)

**程序执行结果**不仅取决于**算法、程序编写**，而且取决于**语言处理系统、操作系统、ISA、微体系结构**。

语言处理系统包括：各种语言处理程序（如编译、汇编、链接）、运行时系统（如库函数，调试、优化等功能）

课程目标： 清楚理解计算机是如何**生成和运行可执行文件**的！

重点在高级语言以下各抽象层：

- C语言程序设计层
  - 数据的机器级表示、运算
  - 语句和过程调用的机器级表示
- 操作系统、编译和链接的部分内容
- **指令集体系结构（ISA）和汇编层**
  - 指令系统、机器代码、汇编语言
- 微体系结构及硬件层

  - CPU的通用结构
  - 层次结构存储系统

### 1.2--计算机系统基本组成与基本功能

![image-20220828180415357](https://raw.githubusercontent.com/iialong/note/main/images/202208281804346.png)

- 程序由指令组成

- 程序在执行前，数据和指令事先存放在存储器中，每条指令和每个数据都有地址，指令按序存放，程序起始地址置PC

- 开始执行程序

  1. 根据PC取指令

  2. 指令译码

  3. 取操作数

  4. 指令执行

  5. 回写结果

  6. 修改PC的值

​		继续执行下一条指令



指令执行过程中，指令和数据被从存储器取到CPU，存放在CPU内的寄存器中，指令在IR中，数据在GPR中。

### 1.3--程序开发和执行过程简介

- 机器语言与汇编语言

![image-20220904111153452](https://raw.githubusercontent.com/iialong/note/main/images/202209041111525.png)

汇编语言(源)程序由汇编指令构成

汇编指令是用助记符和标号来表示的指令（与机器指令一一对应）

指令包含操作码和操作数或其地址码

- 高级语言

有两种转换方式：“编译”和“解释”

**编译程序**(Complier)：将高级语言源程序转换为机器级目标程序，执行时只要启动目标程序即可

**解释程序**(Interpreter )：将高级语言语句逐条翻译成机器指令并立即执行，不生成目标文件



经典hello.c源程序

```c
#include <stdio.h>

int main()
{
	printf("hello, world\n");
}
```

![image-20220904110954966](https://raw.githubusercontent.com/iialong/note/main/images/202209041109091.png)

**任何高级语言程序最终通过执行若干条指令来完成！**

### 1.4--计算机系统层次结构

**指令集体系结构（ISA）**

ISA是一种规约（Specification），它规定了**如何使用硬件**

  - 可执行的指令的集合，包括**指令格式、操作种类**以及每种操作对应的操作数的相应规定；

  - 指令可以接受的**操作数的类型**；

  -  操作数所能存放的寄存器组的结构，包括每个长度和用途；**寄存器的名称、编号、长度和用途**；

  - 操作数所能存放的**存储空间的大小和编址方式**； 

  - 操作数在存储空间存放时按照**大端还是小端**方式存放； 

  -  指令获取操作数的方式，即**寻址方式**；

  - 指令执行过程的控制方式，包括**程序计数器（PC）、条件码定义**等。

**ISA和计算机组成（微结构）之间的关系**

不同ISA规定的指令集不同，如IA-32、MIPS、ARM、X86等

计算机组成必须能够实现ISA规定的功能，如提供GPR、标志、运算电路等

同一种ISA可以有不同的计算机组成，如乘法指令可用ALU或乘法器实现

**ISA是计算机组成的抽象**

### 2.1--数制和编码

![image-20220904225130709](https://raw.githubusercontent.com/iialong/note/main/images/202209042251904.png)

**数值数据表示的三要素**

1. 进位计数制

​	十进制、二进制、十六进制、八进制数及其相互转换

2. 定/浮点表示（解决小数点问题）

- 定点整数、定点小数

- 浮点数（可用一个定点小数和一个定点整数来表示）

3. 定点数的编码（解决正负号问题）

​	原码、补码、移码、反码（很少用）

**定点数和浮点数**

![image-20220904230242970](https://raw.githubusercontent.com/iialong/note/main/images/202209042302063.png)

要解决数值数据的表示问题，只要解决**定点数**的编码问题！

### 2.2--定点数的编码表示

- **原码**

![image-20220904231548380](https://raw.githubusercontent.com/iialong/note/main/images/202209042315443.png)   

原码容易理解，但是不容易使用

从 50年代开始，**整数都采用补码来表示，但浮点数的尾数用原码定点小数表示**

- **补码**

  正数的补码为本身

  负数的补码等于将对应正数补码**各位取反、末位加一**

  简便方法：从右向左遇到第一个1的前面各位取反

- **移码**

![image-20220904231918995](https://raw.githubusercontent.com/iialong/note/main/images/202209042319070.png)

### 2.3--C语言中的整数

- **无符号整数(Unsigned integer)**

  一般在全部是正数运算且不出现负值结果的场合下，可使用无符号整数数表示；

  无符号整数的编码中**没有符号位**。

- **带符号整数(Signed integer)**

  带符号整数用**补码**表示，补码运算系统是模运算系统，加、减运算统一。

- **编译器处理常量时默认的类型**

  C99标准下：

![image-20220925162749964](https://raw.githubusercontent.com/iialong/note/main/images/202209251627080.png)

### 2.4--浮点数的编码表示

**IEEE 754 标准**

![image-20221004194130645](https://raw.githubusercontent.com/iialong/note/main/images/202210041941909.png)

下面以单精度浮点数为例：

- Sign符号位：**1表示负数，0表示正数**
- Exponent指数：
  - **用移码表示，偏置常数为127**（双精度为1023，n位指数为2^(n-1)-1）
    - 用移码是为了保证连续性，连续性是指把除符号位之外的数看成一个无符号整数，它表示的浮点数随这个无符号数的增大而增大。
  - 全0和全1用来表示特殊值
  - 范围为-126~127
  
- Significand有效数（尾数）：
  - **规格化浮点数的整数部分固定是1，不用表示，有效数只表示小数部分**
- 特殊情况
  - 指数全0时，整数部分不再是1而是0，这样有效数全0便表示0（符号位不同可以表示+0和-0）；同时还可以表示非规格化的浮点数，但此时指数不再是e-偏移值（此时e=0），而是1-偏移值，这是为了抵消整数部分变为0的效果，保证连续性；
  - 指数为全1时，如有效数为0，则表示无穷∞（有正负），若有效数不为0，则表示非数（NaN）,即not an number。无穷表示溢出或被0除的结果，非数表示诸如无穷间的运算结果。

通过一个两位指数、两位有效数的例子看一下连续性：（只看正数）

偏置常数为2^(3-1)-1=3

| IEEE编码 | 指数 | 有效数 | 十进制 |
| :------: | :--: | :----: | :----: |
| 0 000 00 |  -2  |   0    |   0    |
| 0 000 01 |  -2  |  1/4   |  1/16  |
| 0 000 10 |  -2  |  2/4   |  2/16  |
| 0 000 11 |  -2  |  3/4   |  3/16  |
| 0 001 00 |  -2  |  4/4   |  4/16  |
| 0 001 01 |  -2  |  5/4   |  5/16  |
| 0 001 10 |  -2  |  6/4   |  6/16  |
| 0 001 11 |  -2  |  7/4   |  7/16  |
| 0 010 00 |  -1  |  4/4   |  8/16  |
| 0 010 01 |  -1  |  5/4   | 10/16  |
| 0 010 10 |  -1  |  6/4   | 12/16  |
| 0 010 11 |  -1  |  7/4   | 14/16  |
| 0 011 00 |  0   |  4/4   | 16/16  |
| 0 011 01 |  0   |  5/4   | 20/16  |
| 0 011 10 |  0   |  6/4   | 24/16  |
| 0 011 11 |  0   |  7/4   | 28/16  |
|   ...    | ...  |  ....  |  ...   |
| 0 111 00 |      |        |   ∞    |
| 0 111 01 |      |        |  NaN   |
| 0 111 10 |      |        |  NaN   |
| 0 111 11 |      |        |  NaN   |

C语言浮点数的舍入采用“四舍六入五向偶”的原则

### 2.5--非数值数据的编码表示

- 西文字符

  ASCII码

- 汉字及国际字符

  **GB2312-80字符集**

  - 汉字的区位码

    码表由94行、94列组成，行号为区号，列号为位号，各占7位，指出汉字在码表中的位置，共14位，区号在左、位号在右

  - 汉字的国标码

    每个汉字的区号和位号各自加上32（20H），得到其国标码

    国标码中区号和位号各占7位。在计算机内部，为方便处理与存储，前面添一个0，构成一个字节

  - 汉字内码

    可在GB2312国标码的基础上产生汉字内码

    为与ASCII码区别，将国标码的两个字节的第一位置“1”后得到一种汉字内码（可以有不同的编码方案）

### 2.6--数据宽度和存储容量的单位

数据的基本宽度

- 比特（bit，位）是计算机中处理、存储、传输信息的最小单位
- 二进制信息最基本的计量单位是“字节”(Byte) 
  - 现代计算机中，存储器按字节编址
  - 字节是最小可寻址单位 (addressable unit) 
  - 如果以字节为一个排列单位，则LSB表示最低有效字节，MSB表示最高有效字节

C语言中数据类型的宽度 (单位：字节)

|  C声明   | 32位机器 | 64位机器 |
| :------: | :------: | :------: |
|   char   |    1     |    1     |
|  short   |    2     |    2     |
|   int    |    4     |    4     |
| **long** |    4     |    8     |
|  float   |    4     |    4     |
|  double  |    8     |    8     |
| **指针** |    4     |    8     |

### 2.7--数据存储时的字节排列

80年代开始，几乎所有通用计算机都采用**字节编址**。

一个基本数据可能会占用多个存储单元，**变量的地址是其最小地址**。

![image-20220925173117670](https://raw.githubusercontent.com/iialong/note/main/images/202209251731757.png)

LSB表示最低有效字节，MSB表示最高有效字节

**通俗的讲，大端表示数的高位在最小地址，小端表示数的低位在最小地址。**



union的所有成员**占用同一段内存**，占用的内存等于最长的成员占用的内存，修改一个成员会影响其余所有成员。

union的存放顺序是**所有成员从低地址开始**，利用该特性可测试CPU的大/小端方式。

```c
#include <stdio.h>
int main()
{
    union NUM
    {
        int a;
        char b;
    } num;
    num.a = 0x12345678;
    if(num.b == 0x12)
        printf("big endian\n");
    else
        printf("little endian\n");
}
```

### 3.1--数字逻辑电路基础

![image-20221003220544722](https://raw.githubusercontent.com/iialong/note/main/images/202210032205871.png)

- 根据电路是否具有存储功能，将逻辑电路划分为两种类型：
  - **组合逻辑电路**：没有存储功能，其输出仅依赖于当前输入；
  - **时序逻辑电路** ：具有存储功能，其输出不仅依赖于当前输入，还依赖于存储单元的当前状态。
- 可以利用基本逻辑门电路构成一些具有特定功能的组合逻辑部件（功能部件），如**译码器**、**编码器**、**多路选择器**、**加法器**等。
- 实现一个功能部件的过程
  1. 用一个真值表描述功能部件的输入和输出之间的关系；
  2. 根据真值表确定逻辑表达式；
  3. 根据逻辑表达式实现逻辑电路。

![image-20221003221145190](https://raw.githubusercontent.com/iialong/note/main/images/202210032211298.png)

![image-20221003221232858](https://raw.githubusercontent.com/iialong/note/main/images/202210032212986.png)

![image-20221003221310260](https://raw.githubusercontent.com/iialong/note/main/images/202210032213366.png)

![image-20221003221344697](https://raw.githubusercontent.com/iialong/note/main/images/202210032213823.png)



# C

### kill函数

函数原型如下:

`int kill(pid_t pid, int sig);`

pid > 0 向pid指定的进程发送sig指定的信号.

pid = 0 向调用kill函数所在进程组中的所有进程发送sig指定的信号.

pid = -1 向调用kill函数所在进程拥有权限的所有进程发送sig信号,除了进程1(init).

pid < -1 向进程组id 为-pid 内的所有进程发送sig 信号.

返回值:成功返回0; 错误返回-1,并且errno会被设置相应的值.

**如果sig = 0, 没有信号发送,但是错误检查还是会执行。sig = 0，可以被用于检查pid指定的进程或进程组是否存在。**

如下:

```c
#include <errno.h>
if(kill(mClientPid, 0) == -1 && errno == ESRCH){

	printf("client process is dead!\n");

}
```

<errno.h>头文件

errno.h 提供了一个整数全局变量errno，代码是一个int型的值，extern int errno来声明定义该错误值，errno 记录系统的最后一次错误代码。

### errno

Linux中系统调用的错误都存储于 `errno`中，`errno`由操作系统维护，存储就近发生的错误，即下一次的错误码会覆盖掉上一次的错误。

只有当系统调用或者调用lib函数时出错，才会置位`errno`！

```c
/* Function: obtain the errno string
*   char *strerror(int errno)
*/
 
#include <stdio.h>
#include <string.h>     //for strerror()
int main()
{
    int tmp = 0;
    for(tmp = 0; tmp <=256; tmp++)
    {
        printf("errno: %2d\t%s\n",tmp,strerror(tmp));
    }
    return 0;
}
```

Linux中，在头文件 `/usr/include/asm-generic/errno-base.h` 对基础常用errno进行了宏定义，在 `/usr/include/asm-asm-generic/errno.h` 中，对剩余的errno做了宏定义

https://www.cnblogs.com/Jimmy1988/p/7485133.html

### fork函数

在Linux下有两个基本的系统调用可以用于创建子进程：fork()和vfork()，当一个进程正在运行的时候，使用了fork()函数之后就会创建另一个进程。与一般函数不同的是，fork()函数会有两次返回值，一次返回给父进程（该返回值是子进程的PID（Process ID）），第二次返回是给子进程，其返回值为0。所以在调用该函数以后，我们需要通过返回值来判断当前的代码时父进程还是子进程在运行：

返回值大于0 -> 父进程在运行
返回值等于0 -> 子进程在运行
返回值小于0 -> 函数系统调用出错

通常系统调用出错的原因有两个：①已存在的系统进程已经太多；②该实际用户ID的进程总数已经超过了限制。

当fork()系统调用时，创建了一个新的子进程，这个子进程时父进程的一个副本，系统在创建了这个新的子进程了之后，会将父进程的文本段、数据段、堆栈都复制一份给子进程，子进程拥有自己独立的空间，对自己内存的修改并不会影响父进程相应的内存空间。

https://blog.csdn.net/geiii9/article/details/123814112

示例代码：先执行子进程，再执行父进程：

```c
#include <stdio.h>

int pid = fork();

if(pid < 0)
{
    //faile
    return;
}
else if(pid = 0)
{
    //子进程
    exit(0);
}
else
{
    while(1)
    {
        sleep(1);
        if(kill(pid, 0) < 0)
        {
            //父进程
        }
    }
}
```

### sigsetjmp函数

相关函数：longjmp, siglongjmp, setjmp 
表头文件：#include <setjmp.h> 
函数定义：int sigsetjmp(sigjmp_buf env, int savesigs) 

函数说明：

sigsetjmp()会保存目前堆栈环境，然后将目前的地址作一个记号，而在程序其他地方调用siglongjmp()时便会直接跳到这个记号位置，然后还原堆栈，继续程序的执行。 

参数env为用来保存目前堆栈环境，一般声明为全局变量 ；
参数savesigs若为非0则代表搁置的信号集合也会一块保存 。

返回：若直接调用则为0，若从siglongjmp调用返回则为非0。

https://blog.csdn.net/tujiaw/article/details/7230990

示例：

```c
#include <string.h>
#include <stdlib.h>
#include <signal.h>
#include <setjmp.h>
#include <unistd.h>
#include <stdio.h>

sigjmp_buf jmp_env;

static void connect_alarm()
{
    siglongjmp(jmp_env, 1);
}

int main()
{
    int sec_timeout = 3;//超时时间
    int run_time = 2;

    signal(SIGALRM, connect_alarm);
    if (sigsetjmp(jmp_env, 1))
    {
        //超时
        alarm(0);
        return 0;
    }

    alarm(sec_timeout);
    printf("set timeout\n");
    //to do something
    sleep(run_time);
    printf("running...\n");
	signal(SIGALRM, SIG_IGN);

    return 0;
}
```

### 一个传指针并修改的错误

要在函数内修改指针的值，参数需要传指针的地址

错误代码：

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct a{
    int i;
}A;

void init(A *p);

int main(void)
{
    A *ptr = NULL;

    init(ptr);
	//这里ptr认为NULL，并未修改
    printf("ptr[1] = %d\n", ptr[1].i);

    return 0;
}

void init(A *p)
{
    p = malloc(4 * sizeof(A));
    p[1].i = 555;
}
```

正确代码：

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct a{
	int i;
}A;

void init(A **p);

int main(void)
{
        A *ptr = NULL;

        init(&ptr);//要修改ptr，需传ptr的地址
        printf("ptr[1] = %d\n", ptr[1].i);

        return 0;
}

void init(A **p)
{
        *p = malloc(4 * sizeof(A));
        (*p)[1].i = 555;
}
```

### readlink与/proc/self/exe

头文件`#include <unistd.h>`

定义函数：`ssize_t readlink(const char *path, char *buf, size_t bufsiz);`

函数说明：readlink()会将参数path的 符号链接内容存储到参数buf所指的内存空间，返回的内容不是以\000作字符串结尾，但会将字符串的字符数返回，这使得添加\000变得简单。若参数bufsiz小于符号连接的内容长度，过长的内容会被截断，如果 readlink 第一个参数指向一个文件而不是 符号链接时，readlink 设 置errno 为 EINVAL 并返回 -1。 readlink()函数组合了open()、read()和close()的所有操作。

返回值 ：执行成功则返回字符串的字符数，失败返回-1， 错误代码存于errno

执行成功则返回ssize_t



linux系统中有个符号链接：/proc/self/exe 它代表当前程序，所以可以用readlink读取它的源路径就可以获取当前程序的绝对路径，如下：

```c
#include <unistd.h>
#include <stdio.h>
 
int main(int argc , char* argv[])
{
    char buf[1024] = { 0 };
    int n;
 
    n = readlink("/proc/self/exe" , buf , sizeof(buf));
    if( n > 0 && n < sizeof(buf))
    {
        printf("%s\n" , buf);
    }
}
```

https://blog.csdn.net/wteruiycbqqvwt/article/details/112664432

### getopt函数 -- 解析命令的可选项

【说明】

getopt只是一个简单的解析命令可选项的函数，只能进行简单的格式命令解析，格式如下：

1、形如：cmd [-a]\[-b\] //对短选项的解析；

2、形如：cmd [-a a_argument]\[-b b_argument\] //对短选项及短选项的参数解析；

3、形如：cmd [-a\[a_argument\]] //选项a的参数也是可选的情况解析。

【原型】

```c
#include <unistd.h>
 
extern char *optarg;
extern int optind, opterr, optopt;
int getopt(int argc, char * const argv[], const char *optstring);
```

关于optstring的格式规范简单总结如下：

(1) 单个字符，表示该选项Option不需要参数。

(2) 单个字符后接一个冒号":"，表示该选项Option需要一个选项参数Option argument。选项参数Option argument可以紧跟在选项Option之后，或者以空格隔开。选项参数Option argument的首地址赋给optarg。

(3) 单个字符后接两个冒号"::"，表示该选项Option的选项参数Option argument是可选的。当提供了Option argument时，必须紧跟Option之后，不能以空格隔开，否则getopt()会认为该选项Option没有选项参数Option argument，optarg赋值为NULL。相反，提供了选项参数Option argument，则optarg指向Option argument。

为了使用getopt()，我们需要在while循环中不断地调用直到其返回-1为止。每一次调用，当getopt()找到一个有效的Option的时候就会返回这个Option字符，并设置几个全局变量。

全局变量

char *optarg -- 当匹配一个选项后，如果该选项带选项参数，则optarg指向选项参数字符串；若该选项不带选项参数，则optarg为NULL；若该选项的选项参数为可选时，optarg为NULL表明无选项参数，optarg不为NULL时则指向选项参数字符串。

https://blog.csdn.net/c1523456/article/details/79173776

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <sys/types.h>

extern char *optarg;
extern int optind, opterr, optopt;

int main(int argc, char *argv[])
{
        int i;
        int opt;

        while ((opt = getopt(argc, argv, "a:b::c")) != -1)
        {
            switch (opt) {
                case 'a':
                    printf ("option: %c argv: %s\n", opt, optarg);
                    break;
                case 'b':
                    if (optarg)
                        printf ("option: %c argv: %s\n", opt, optarg);
                    else
                        printf ("option: %c no argument\n", opt);
                    break;
                case 'c':
                    printf ("option: %c\n", opt);
                    break;
                default:
                    printf ("unknow option: %c\n", opt);
                    break;
            }
        }

        return 0;
}
```

### 共享内存与二维数组

库函数说明

```c
#include <sys/shm.h>

int shmget(key_t key, size_t size, int shmflg);
void *shmat(int shmid, const void *shmaddr, int shmflg);
int shmdt(const void *shmaddr);
int shmctl(int shmid, int cmd, struct shmid_ds *buf);

#include <sys/ipc.h>
key_t ftok(const char *pathname, int proj_id);
```

shmget()：创建共享内存区

- key参数的产生

  方式一：通过传进一个pathname和project_id，使用ftok调用产生的。这种方式适用于同个项目中相互通信场景，不过需要提前约定好文件路径、名称以及项目id。

  方式二：自定义方式key，key_t 其实是一个int类型的重新声明，直接传自定义的key给shmget也是可以的。

- size指定需要创建的共享内存段的大小，读取时可以设为0。

- shmflag

  支持： IPC_CREAT、IPC_EXCL、SHM_HUGETLB、SHM_NORESERVE，及共享内存的权限。

  如果同时指定IPC_CREAT、IPC_EXCL，且指定key已存在，则报错。

  访问一个已经存在的共享内存，此时可以将shmflg置为0，不加任何标识打开。

- 返回值

  成功返回一个非负整数，即共享内存的标识符；失败返回-1

shmat()：把这块共享内存区挂接映射到两个进程的地址空间上。

shmdt()：撤销内存映射关系

https://www.jianshu.com/p/701a73809887

https://blog.csdn.net/m0_53311279/article/details/125160583

写共享内存

```c
#include <sys/shm.h>
#include <stdio.h>
#include <stdlib.h>

#deinfe ROW 64
#deinfe LENGTH 32

static char (*list)[LENGTH];
static const long key_id 0x42424141;//AABB
static int shm_id = -1;
static int shm_size = ROW*LENGTH;

int main()
{
    int i;
    shm_id = shmget(key_id, shm_size, IPC_CREAT | IPC_EXCL | 0666);
    if(shm_id == -1)
    {
        return 0;
	}
    
    list = (char (*)[LENGTH])shmat(shm_id, NULL, 0);
    if((void *)list == (void *)-1)
    {
        return 0;
    }
    
    for(i = 0; i < ROW; i++)
    {
        memcpy(list[i], "string", 7);
    }
    
    if(shm_id != -1)
    {
        shmdt(shm_id);
    }
}
```

读共享内存

```c
#include <sys/shm.h>
#include <stdio.h>
#include <stdlib.h>

#deinfe ROW 64
#deinfe LENGTH 32

static char (*list)[LENGTH];
static const long key_id 0x42424141;//AABB
static int shm_id = -1;
static int shm_size = ROW*LENGTH;

int main()
{
    int i;
    shm_id = shmget(key_id, 0, 0);
    if(shm_id == -1)
    {
        return 0;
	}
    
    list = (char (*)[LENGTH])shmat(shm_id, NULL, 0);
    if((void *)list == (void *)-1)
    {
        return 0;
    }
    
    for(i = 0; i < ROW; i++)
    {
        printf("%s\n", list[i]);
    }
    
    if(shm_id != -1)
    {
        shmdt(shm_id);
    }
}
```



# linux

### iptables参数

iptables -t nat -L

- -t table表名（指定要操作的表，默认filter）

- -L（列出链所有的规则）

iptables -t nat -F DMZ_nas0_0

- -F chain链名（清除该链下所有操作）

iptables -t nat -I DMZ_nas0_0 -p all -i nas0_0 -j DNAT --to 192.168.2.2

- -I chain链名 [rulenum第几条规则]（插入规则到该链第rulenum条规则之前，rulenum默认为1）
- -p protocol协议（指定协议，tcp udp all）
- -i interface接口名（指定输入的网络接口）
- -j target跳转目标（指定下一个处理规则，如ACCEPT,REJECT,DROP,DNAT,SNAT等）
- --to ip（DNAT目的地址）

iptables -t nat -A DMZ_nas0_0 -p tcp --dport 80 -i nas0_0 -j DNAT --to 192.168.2.159:8000

- -A chain链名（追加规则到该链最后）
- --dport port（指定tcp或udp后指定要匹配的目的端口号）

https://blog.csdn.net/wzj_110/article/details/108890766

### grep搜索跳过某个目录

grep -nr --exclude-dir="skipDir" sreachContent

### /dev/null

/dev/null在Linux中其实是一个空设备文件，它对于写入的东西通通扔掉。

由于它没有执行权限，不是一个可执行文件，所以不能使用管道符 **|** 来接 /dev/null ，只能使用文件重定向（**>**, **>>** 或 **<**, **<<**）。

https://baijiahao.baidu.com/s?id=1712518976709206113

# 网络

### MAC地址分类

一个制造商在生产制造网卡之前，必须先向 IEEE 注册，以获取到一个长度为 24bit 的厂商代码，也称为 OUI（Organizationally-Unique Identifier）。制造商在生产制造网卡的过程中，会往每一块网卡的 ROM 中烧入一个 48bit 的 BIA（Burned-In Address，固化地址）地址，BIA 地址的前 3 个字节就是该制造商的 OUI，后 3 个字节由该制造商自己确定，但不同的网卡，其 BIA 地址的后 3 个字节不相同。烧入进网卡的 BIA 地址是不能被更改的，只能被读取出来使用。

注意，BIA 地址只是 MAC 地址的一种，更准确的说，BIA 地址是一种单播 MAC 地址。MAC 地址共分为 3 种，分别为单播 MAC 地址、组播 MAC 地址、广播 MAC 地址。这 3 种 MAC 地址的定义分别如下：

1）单播 MAC 地址是指第一个字节的最低位是 0 的 MAC 地址。
2）组播 MAC 地址是指第一个字节的最低位是 1 的 MAC 地址。
3）广播 MAC 地址是指每个比特都是 1 的 MAC 地址。广播 MAC 地址是组播 MAC 地址的一个特例。

# 前端

### 在Vue中修改element UI组件的样式（deep 深度选择器）

直接使用\<style\>标签，没有scopd属性，会在全局生效，可能会造成其他组件样式的错乱，所以该方式不推荐。

```css
<style>

</style>
```

当 \<style\> 标签中有 scoped 属性时，它的 CSS 只作用于当前组件中的元素，父组件中如果有跟子组件相同的class名称或者使用选择器的时候，不会影响其子组件。也就是实现了组件的私有化，不对全局造成样式污染。

当想在父组件修改子组件的样式，就需要使用/deep/深度选择器。

修改el-input的后缀元素背景颜色：

```html
<el-input v-model.number="form.limit_down" class="input-with-select">
    <el-select v-model="unit_down" slot="append" style="width: 80px;">
        <el-option
            v-for="item in unitOption"
            :key="item.value"
            :label="item.label"
            :value="item.value"
        >
        </el-option>
    </el-select>
</el-input>
```

```css
<style scoped>
  .input-with-select /deep/ .el-input-group__append {
    background-color: #ffffff;
  }
</style>
```

### vue中的computed、watch(immediate、deep)区别

computed是vue实例中的计算属性，存在缓存机制，只有它所依赖的属性值发生变化才会重新计算，否则默认走缓存。

当一个属性依赖多个属性时一般可以采用computed方式，当该属性依赖的其他属性发生变化时，会立即调用该属性的get方法重新计算当前的属性值并重新渲染页面。

watch只能监听**data中现有的属性**，只要监听的属性发生变化就会触发监听函数执行。

computed和watch的区别：

- 1、computed默认走缓存，减少性能消耗；watch不走缓存
- 2、computed不支持异步；watch支持异步
- 3、当一个属性依赖多个属性时使用computed（多对一）；当一个属性变化会引起多个操作时使用watch（一对多）

watch监听函数在第一次绑定时不执行，只有在监听到的属性值发生变化才会执行对应的监听函数，利用watch中的immediate属性让watch中监听函数在第一次绑定时就执行。

可以通过设置watch中的deep属性值为true，实现通过设置一个对象的监听函数，就可以监听到该对象中的属性值发生的变化。

### setTimeout

运行机制：

setTimeout和setInterval的运行机制是，将指定的代码移出本次执行，等到下一轮Event Loop时，再检查是否到了指定时间。如果到了，就执行对应的代码；如果不到，就等到再下一轮Event Loop时重新判断。这意味着，setTimeout指定的代码，必须等到本次执行的所有代码都执行完，才会执行。

每一轮Event Loop时，都会将“任务队列”中需要执行的任务，一次执行完。setTimeout和setInterval都是把任务添加到“任务队列”的尾部。因此，它们实际上要等到当前脚本的所有同步任务执行完，然后再等到本次Event Loop的“任务队列”的所有任务执行完，才会开始执行。由于前面的任务到底需要多少时间执行完，是不确定的，所以没有办法保证，setTimeout和setInterval指定的任务，一定会按照预定时间执行。

`setTimeout(f,0)`将第二个参数设为0，作用是让f在现有的任务（脚本的同步任务和“任务队列”中已有的事件）一结束就立刻执行。也就是说，`setTimeout(f,0)`的作用是，尽可能早地执行指定的任务。

https://blog.csdn.net/lihchweb/article/details/94635720

# 工具

## 网站

linux工具快速教程：

https://linuxtools-rst.readthedocs.io/zh_CN/latest/index.html

# RC

## WEB



## 算号器

npm run dev

npm run build

## gitbook

环境安装

cnpm install -g gitbook-cli

生成文档

gitbook init

gitbook serve

## 插件

### IF5

#### IF5上线失败

错误代码查看：authn_constant.h

errorcode 101，202：需要保证SN和一机一密录入正确