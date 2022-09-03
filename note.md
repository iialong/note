# 课程笔记

## 《计算机系统基础》

### 1.1--为什么要学习计算机系统？

![image-20220828110250180](https://raw.githubusercontent.com/iialong/note/main/images/image-20220828110250180.png?token=A2XHUZHZBCARMBINPO4Q563DBLNR4)

**程序执行结果**不仅取决于**算法、程序编写**，而且取决于**语言处理系统、操作系统、ISA、微体系结构**。

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

指令执行过程中，指令和数据被从存储器取到CPU，存放在CPU内的寄存器中，指令在IR中，数据在GPR中。

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