### 系统环境
**CPU**
```
lscpu:
Architecture:          x86_64
CPU op-mode(s):        32-bit, 64-bit
Byte Order:            Little Endian
CPU(s):                6
On-line CPU(s) list:   0-5
Thread(s) per core:    1
Core(s) per socket:    6
Socket(s):             1
NUMA node(s):          1
Vendor ID:             GenuineIntel
CPU family:            6
Model:                 158
Model name:            Intel(R) Core(TM) i7-8700 CPU @ 3.20GHz
Stepping:              10
CPU MHz:               3191.998
BogoMIPS:              6383.99
Hypervisor vendor:     KVM
Virtualization type:   full
L1d cache:             32K
L1i cache:             32K
L2 cache:              256K
L3 cache:              12288K
NUMA node0 CPU(s):     0-5
Flags:                 fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx rdtscp lm constant_tsc rep_good nopl xtopology nonstop_tsc eagerfpu pni pclmulqdq ssse3 cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt aes xsave avx rdrand hypervisor lahf_lm abm 3dnowprefetch invpcid_single fsgsbase avx2 invpcid rdseed clflushopt flush_l1d
```
**内核版本**
```
uname -a:
Linux localhost.localdomain 3.10.0-1062.4.1.el7.x86_64 #1 SMP Fri Oct 18 17:15:30 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
```

**GCC**
```
gcc -v:
COLLECT_GCC=cc
COLLECT_LTO_WRAPPER=/usr/local/gcc/9.3.0/libexec/gcc/x86_64-redhat-linux/9.3.0/lto-wrapper
Target: x86_64-redhat-linux
Configured with: ../configure --prefix=/usr/local/gcc/9.3.0 --enable-bootstrap --enable-shared --enable-threads=posix --enable-checking=release --with-system-zlib --enable-__cxa_atexit --disable-libunwind-exceptions --enable-gnu-unique-object --enable-linker-build-id --with-linker-hash-style=gnu --enable-languages=c,c++,objc,obj-c++ --enable-plugin --enable-initfini-array --disable-libgcj --enable-gnu-indirect-function --with-tune=generic --with-arch_32=x86-64 --build=x86_64-redhat-linux
Thread model: posix
gcc version 9.3.0 (GCC) 
```
---

**c代码**
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 100;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 64 00 00 00    movl   $0x64,-0x4(%rbp)
  4004dd:   b8 00 00 00 00          mov    $0x0,%eax
  4004e2:   5d                      pop    %rbp
  4004e3:   c3                      retq   
  4004e4:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  4004eb:   00 00 00  
  4004ee:   66 90                   xchg   %ax,%ax

```
**汇编指令学习**
>xchg: Exchanges the contents of the destination (first) and source (second) operands. (XCHG (E)AX, (E)AX (encoded instruction byte is 90H) is an alias for NOP regardless of data size
prefixes, including REX.W.)
---

**c代码**
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = -100;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 9c ff ff ff    movl   $0xffffff9c,-0x4(%rbp)
  4004dd:   b8 00 00 00 00          mov    $0x0,%eax
  4004e2:   5d                      pop    %rbp
  4004e3:   c3                      retq   
  4004e4:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  4004eb:   00 00 00  
  4004ee:   66 90                   xchg   %ax,%ax

```

---
**c代码**
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    unsigned int a = 100;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 9c ff ff ff    movl   $0xffffff9c,-0x4(%rbp)
  4004dd:   b8 00 00 00 00          mov    $0x0,%eax
  4004e2:   5d                      pop    %rbp
  4004e3:   c3                      retq   
  4004e4:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  4004eb:   00 00 00  
  4004ee:   66 90                   xchg   %ax,%ax

```

---
**c代码**
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    short int a = 100;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   66 c7 45 fe 64 00       movw   $0x64,-0x2(%rbp)
  4004dc:   b8 00 00 00 00          mov    $0x0,%eax
  4004e1:   5d                      pop    %rbp
  4004e2:   c3                      retq   
  4004e3:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  4004ea:   00 00 00  
  4004ed:   0f 1f 00                nopl   (%rax)
```

---
**c代码**
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    unsigned short int a = 100;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   66 c7 45 fe 64 00       movw   $0x64,-0x2(%rbp)
  4004dc:   b8 00 00 00 00          mov    $0x0,%eax
  4004e1:   5d                      pop    %rbp
  4004e2:   c3                      retq   
  4004e3:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  4004ea:   00 00 00  
  4004ed:   0f 1f 00                nopl   (%rax)
```

---
**c代码**
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    long a = 100;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   48 c7 45 f8 64 00 00    movq   $0x64,-0x8(%rbp)
  4004dd:   00  
  4004de:   b8 00 00 00 00          mov    $0x0,%eax
  4004e3:   5d                      pop    %rbp
  4004e4:   c3                      retq   
  4004e5:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  4004ec:   00 00 00  
  4004ef:   90                      nop 

```

---
**c代码**
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    unsigned long a = 100;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   48 c7 45 f8 64 00 00    movq   $0x64,-0x8(%rbp)
  4004dd:   00  
  4004de:   b8 00 00 00 00          mov    $0x0,%eax
  4004e3:   5d                      pop    %rbp
  4004e4:   c3                      retq   
  4004e5:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  4004ec:   00 00 00  
  4004ef:   90                      nop 
```

---
**c代码**
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    long a = -100;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   48 c7 45 f8 9c ff ff    movq   $0xffffffffffffff9c,-0x8(%rbp)
  4004dd:   ff  
  4004de:   b8 00 00 00 00          mov    $0x0,%eax
  4004e3:   5d                      pop    %rbp
  4004e4:   c3                      retq   
  4004e5:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  4004ec:   00 00 00  
  4004ef:   90 
```

---
**c代码**
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    long long a = 100;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   48 c7 45 f8 64 00 00    movq   $0x64,-0x8(%rbp)
  4004dd:   00  
  4004de:   b8 00 00 00 00          mov    $0x0,%eax
  4004e3:   5d                      pop    %rbp
  4004e4:   c3                      retq   
  4004e5:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  4004ec:   00 00 00  
  4004ef:   90                      nop 
```

---
**c代码**
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    unsigined long long a = 100;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   48 c7 45 f8 64 00 00    movq   $0x64,-0x8(%rbp)
  4004dd:   00  
  4004de:   b8 00 00 00 00          mov    $0x0,%eax
  4004e3:   5d                      pop    %rbp
  4004e4:   c3                      retq   
  4004e5:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  4004ec:   00 00 00  
  4004ef:   90                      nop 
```

---
**c代码**
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    long long a = -100;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   48 c7 45 f8 9c ff ff    movq   $0xffffffffffffff9c,-0x8(%rbp)
  4004dd:   ff  
  4004de:   b8 00 00 00 00          mov    $0x0,%eax
  4004e3:   5d                      pop    %rbp
  4004e4:   c3                      retq   
  4004e5:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  4004ec:   00 00 00  
  4004ef:   90 
```

---
**c代码**
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    char a = 100;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c6 45 ff 64             movb   $0x64,-0x1(%rbp)
  4004da:   b8 00 00 00 00          mov    $0x0,%eax
  4004df:   5d                      pop    %rbp
  4004e0:   c3                      retq   
  4004e1:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  4004e8:   00 00 00  
  4004eb:   0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)
```

---
**c代码**
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    unsigned char a = 100;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c6 45 ff 64             movb   $0x64,-0x1(%rbp)
  4004da:   b8 00 00 00 00          mov    $0x0,%eax
  4004df:   5d                      pop    %rbp
  4004e0:   c3                      retq   
  4004e1:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  4004e8:   00 00 00  
  4004eb:   0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)
```

---
**c代码**
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    char a = -100;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c6 45 ff 9c             movb   $0x9c,-0x1(%rbp)
  4004da:   b8 00 00 00 00          mov    $0x0,%eax
  4004df:   5d                      pop    %rbp
  4004e0:   c3                      retq   
  4004e1:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  4004e8:   00 00 00  
  4004eb:   0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)
```

---
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    float a = 100.1;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   f3 0f 10 05 96 00 00    movss  0x96(%rip),%xmm0        # 400574 <_IO_stdin_used+0x4>
  4004dd:   00  
  4004de:   f3 0f 11 45 fc          movss  %xmm0,-0x4(%rbp)
  4004e3:   b8 00 00 00 00          mov    $0x0,%eax
  4004e8:   5d                      pop    %rbp
  4004e9:   c3                      retq   
  4004ea:   66 0f 1f 44 00 00       nopw   0x0(%rax,%rax,1)
```

---
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    float a = -100.1;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   f3 0f 10 05 96 00 00    movss  0x96(%rip),%xmm0        # 400574 <_IO_stdin_used+0x4>
  4004dd:   00  
  4004de:   f3 0f 11 45 fc          movss  %xmm0,-0x4(%rbp)
  4004e3:   b8 00 00 00 00          mov    $0x0,%eax
  4004e8:   5d                      pop    %rbp
  4004e9:   c3                      retq   
  4004ea:   66 0f 1f 44 00 00       nopw   0x0(%rax,%rax,1)
```

---
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    double a = 100.1;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   f2 0f 10 05 9a 00 00    movsd  0x9a(%rip),%xmm0        # 400578 <_IO_stdin_used+0x8>
  4004dd:   00  
  4004de:   f2 0f 11 45 f8          movsd  %xmm0,-0x8(%rbp)
  4004e3:   b8 00 00 00 00          mov    $0x0,%eax
  4004e8:   5d                      pop    %rbp
  4004e9:   c3                      retq   
  4004ea:   66 0f 1f 44 00 00       nopw   0x0(%rax,%rax,1)
```

---
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
#include <stddef.h>
int main() {
    int *a = NULL;
    int *b;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   48 c7 45 f8 00 00 00    movq   $0x0,-0x8(%rbp)
  4004dd:   00  
  4004de:   b8 00 00 00 00          mov    $0x0,%eax
  4004e3:   5d                      pop    %rbp
  4004e4:   c3                      retq   
  4004e5:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  4004ec:   00 00 00  
  4004ef:   90                      nop 
```

---
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
#include <stddef.h>
int main() {
    int b = 100;
    int *a = &b;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 f4 64 00 00 00    movl   $0x64,-0xc(%rbp)
  4004dd:   48 8d 45 f4             lea    -0xc(%rbp),%rax
  4004e1:   48 89 45 f8             mov    %rax,-0x8(%rbp)
  4004e5:   b8 00 00 00 00          mov    $0x0,%eax
  4004ea:   5d                      pop    %rbp
  4004eb:   c3                      retq   
  4004ec:   0f 1f 40 00             nopl   0x0(%rax)
```

---
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
#include <stddef.h>
int main() {
    unsigned int b = 100;
    unsigned int *a = &b;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 f4 64 00 00 00    movl   $0x64,-0xc(%rbp)
  4004dd:   48 8d 45 f4             lea    -0xc(%rbp),%rax
  4004e1:   48 89 45 f8             mov    %rax,-0x8(%rbp)
  4004e5:   b8 00 00 00 00          mov    $0x0,%eax
  4004ea:   5d                      pop    %rbp
  4004eb:   c3                      retq   
  4004ec:   0f 1f 40 00             nopl   0x0(%rax)
```

---
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
#include <stddef.h>
int main() {
    int b = -100;
    int *a = &b;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 f4 9c ff ff ff    movl   $0xffffff9c,-0xc(%rbp)
  4004dd:   48 8d 45 f4             lea    -0xc(%rbp),%rax
  4004e1:   48 89 45 f8             mov    %rax,-0x8(%rbp)
  4004e5:   b8 00 00 00 00          mov    $0x0,%eax
  4004ea:   5d                      pop    %rbp
  4004eb:   c3                      retq   
  4004ec:   0f 1f 40 00             nopl   0x0(%rax)
```

---
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
#include <stddef.h>
int main() {
    long b = 100;
    long *a = &b;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   48 c7 45 f0 64 00 00    movq   $0x64,-0x10(%rbp)
  4004dd:   00
  4004de:   48 8d 45 f0             lea    -0x10(%rbp),%rax
  4004e2:   48 89 45 f8             mov    %rax,-0x8(%rbp)
  4004e6:   b8 00 00 00 00          mov    $0x0,%eax
  4004eb:   5d                      pop    %rbp
  4004ec:   c3                      retq
  4004ed:   0f 1f 00                nopl   (%rax)

```

---
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
#include <stddef.h>
int main() {
    long long b = 100;
    long long *a = &b;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   48 c7 45 f0 64 00 00    movq   $0x64,-0x10(%rbp)
  4004dd:   00
  4004de:   48 8d 45 f0             lea    -0x10(%rbp),%rax
  4004e2:   48 89 45 f8             mov    %rax,-0x8(%rbp)
  4004e6:   b8 00 00 00 00          mov    $0x0,%eax
  4004eb:   5d                      pop    %rbp
  4004ec:   c3                      retq
  4004ed:   0f 1f 00                nopl   (%rax)
```

---
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
#include <stddef.h>
int main() {
    short b = 100;
    short *a = &b;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   66 c7 45 f6 64 00       movw   $0x64,-0xa(%rbp)
  4004dc:   48 8d 45 f6             lea    -0xa(%rbp),%rax
  4004e0:   48 89 45 f8             mov    %rax,-0x8(%rbp)
  4004e4:   b8 00 00 00 00          mov    $0x0,%eax
  4004e9:   5d                      pop    %rbp
  4004ea:   c3                      retq
  4004eb:   0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)
```

---
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
#include <stddef.h>
int main() {
    char b = 100;
    char *a = &b;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c6 45 f7 64             movb   $0x64,-0x9(%rbp)
  4004da:   48 8d 45 f7             lea    -0x9(%rbp),%rax
  4004de:   48 89 45 f8             mov    %rax,-0x8(%rbp)
  4004e2:   b8 00 00 00 00          mov    $0x0,%eax
  4004e7:   5d                      pop    %rbp
  4004e8:   c3                      retq
  4004e9:   0f 1f 80 00 00 00 00    nopl   0x0(%rax)
```

---
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
#include <stddef.h>
int main() {
    float b = 100.1;
    float *a = &b;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   f3 0f 10 05 a6 00 00    movss  0xa6(%rip),%xmm0        # 400584 <_IO_stdin_used+0x4>
  4004dd:   00
  4004de:   f3 0f 11 45 f4          movss  %xmm0,-0xc(%rbp)
  4004e3:   48 8d 45 f4             lea    -0xc(%rbp),%rax
  4004e7:   48 89 45 f8             mov    %rax,-0x8(%rbp)
  4004eb:   b8 00 00 00 00          mov    $0x0,%eax
  4004f0:   5d                      pop    %rbp
  4004f1:   c3                      retq
  4004f2:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  4004f9:   00 00 00
  4004fc:   0f 1f 40 00             nopl   0x0(%rax)
```

---
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
#include <stddef.h>
int main() {
    double b = 100.1;
    double *a = &b;

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   f2 0f 10 05 aa 00 00    movsd  0xaa(%rip),%xmm0        # 400588 <_IO_stdin_used+0x8>
  4004dd:   00
  4004de:   f2 0f 11 45 f0          movsd  %xmm0,-0x10(%rbp)
  4004e3:   48 8d 45 f0             lea    -0x10(%rbp),%rax
  4004e7:   48 89 45 f8             mov    %rax,-0x8(%rbp)
  4004eb:   b8 00 00 00 00          mov    $0x0,%eax
  4004f0:   5d                      pop    %rbp
  4004f1:   c3                      retq
  4004f2:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  4004f9:   00 00 00
  4004fc:   0f 1f 40 00             nopl   0x0(%rax)
```

---
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 1;
    int b;

    if (a == 1) {
        b = 1; 
    } else {
        b = 0; 
    }

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 01 00 00 00    movl   $0x1,-0x4(%rbp)
  4004dd:   83 7d fc 01             cmpl   $0x1,-0x4(%rbp)
  4004e1:   75 09                   jne    4004ec <main+0x1a>
  4004e3:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004ea:   eb 07                   jmp    4004f3 <main+0x21>
  4004ec:   c7 45 f8 00 00 00 00    movl   $0x0,-0x8(%rbp)
  4004f3:   b8 00 00 00 00          mov    $0x0,%eax
  4004f8:   5d                      pop    %rbp
  4004f9:   c3                      retq
  4004fa:   66 0f 1f 44 00 00       nopw   0x0(%rax,%rax,1)
```

---
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
#include <stddef.h>
  
int main() {
    int a = 1;
    int *b = &a;
    int *c = NULL;
    int d = 0;

    if (c == b) {
        d = 1;
    } else {
        d = 0;
    }

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 e8 01 00 00 00    movl   $0x1,-0x18(%rbp)
  4004dd:   48 8d 45 e8             lea    -0x18(%rbp),%rax
  4004e1:   48 89 45 f8             mov    %rax,-0x8(%rbp)
  4004e5:   48 c7 45 f0 00 00 00    movq   $0x0,-0x10(%rbp)
  4004ec:   00
  4004ed:   c7 45 ec 00 00 00 00    movl   $0x0,-0x14(%rbp)
  4004f4:   48 8b 45 f0             mov    -0x10(%rbp),%rax
  4004f8:   48 3b 45 f8             cmp    -0x8(%rbp),%rax
  4004fc:   75 09                   jne    400507 <main+0x35>
  4004fe:   c7 45 ec 01 00 00 00    movl   $0x1,-0x14(%rbp)
  400505:   eb 07                   jmp    40050e <main+0x3c>
  400507:   c7 45 ec 00 00 00 00    movl   $0x0,-0x14(%rbp)
  40050e:   b8 00 00 00 00          mov    $0x0,%eax
  400513:   5d                      pop    %rbp
  400514:   c3                      retq
  400515:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  40051c:   00 00 00
  40051f:   90                      nop
```

---
**64位禁止编译器优化编译指令**
```
gcc 1.c -o 1 -O0
```
```c
#include <stddef.h>
  
int main() {
    int a = 1;
    int *b = &a;
    int *c = NULL;
    int d = 0;

    if (c == b) {
        d = 1;
    } else if (c == NULL) {
        d = 0;
    } else {
        d = 2; 
    }

    return 0;
}
```
**对应汇编**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 e8 01 00 00 00    movl   $0x1,-0x18(%rbp)
  4004dd:   48 8d 45 e8             lea    -0x18(%rbp),%rax
  4004e1:   48 89 45 f8             mov    %rax,-0x8(%rbp)
  4004e5:   48 c7 45 f0 00 00 00    movq   $0x0,-0x10(%rbp)
  4004ec:   00
  4004ed:   c7 45 ec 00 00 00 00    movl   $0x0,-0x14(%rbp)
  4004f4:   48 8b 45 f0             mov    -0x10(%rbp),%rax
  4004f8:   48 3b 45 f8             cmp    -0x8(%rbp),%rax
  4004fc:   75 09                   jne    400507 <main+0x35>
  4004fe:   c7 45 ec 01 00 00 00    movl   $0x1,-0x14(%rbp)
  400505:   eb 17                   jmp    40051e <main+0x4c>
  400507:   48 83 7d f0 00          cmpq   $0x0,-0x10(%rbp)
  40050c:   75 09                   jne    400517 <main+0x45>
  40050e:   c7 45 ec 00 00 00 00    movl   $0x0,-0x14(%rbp)
  400515:   eb 07                   jmp    40051e <main+0x4c>
  400517:   c7 45 ec 02 00 00 00    movl   $0x2,-0x14(%rbp)
  40051e:   b8 00 00 00 00          mov    $0x0,%eax
  400523:   5d                      pop    %rbp
  400524:   c3                      retq
  400525:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  40052c:   00 00 00
  40052f:   90                      nop
```
**演示图片**
![演示图片](D:\文档\技术资源\读书笔记\ReadingNote\RE学习笔记\linux\X86_64\c\1.png)

---
