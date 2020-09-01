1. c源码设计
2. c源码编写
3. gcc预处理：cpp
4. gcc编译：cc1
5. gcc汇编：as
6. gcc链接：collect2:ld
7. elf装载
8. elf执行

ELF二进制文件load到内存并执行，内核源码：
linux-2.6.34/fs/binfmt_elf.c:elf_format.load_binary
linux-2.6.34/arch/ia64/kernel/process.c:sys_execve
