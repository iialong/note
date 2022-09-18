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

**原码**

![image-20220904231548380](https://raw.githubusercontent.com/iialong/note/main/images/202209042315443.png)

原码容易理解，但是不容易使用

从 50年代开始，**整数都采用补码来表示，但浮点数的尾数用原码定点小数表示**

**补码**

正数的补码为本身

负数的补码等于将对应正数补码**各位取反、末位加一**

​		简便方法：从右向左遇到第一个1的前面各位取反

**移码**

![image-20220904231918995](https://raw.githubusercontent.com/iialong/note/main/images/202209042319070.png)

### 2.3--C语言中的整数

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