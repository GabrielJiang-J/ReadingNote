### ϵͳ����
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
**�ں˰汾**
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

**c����**
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 100;

    return 0;
}
```
**��Ӧ���**
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
**���ָ��ѧϰ**
>xchg: Exchanges the contents of the destination (first) and source (second) operands. (XCHG (E)AX, (E)AX (encoded instruction byte is 90H) is an alias for NOP regardless of data size prefixes, including REX.W.)
---

**c����**
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = -100;

    return 0;
}
```
**��Ӧ���**
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
**c����**
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    unsigned int a = 100;

    return 0;
}
```
**��Ӧ���**
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
**c����**
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    short int a = 100;

    return 0;
}
```
**��Ӧ���**
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
**c����**
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    unsigned short int a = 100;

    return 0;
}
```
**��Ӧ���**
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
**c����**
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    long a = 100;

    return 0;
}
```
**��Ӧ���**
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
**c����**
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    unsigned long a = 100;

    return 0;
}
```
**��Ӧ���**
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
**c����**
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    long a = -100;

    return 0;
}
```
**��Ӧ���**
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
**c����**
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    long long a = 100;

    return 0;
}
```
**��Ӧ���**
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
**c����**
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    unsigined long long a = 100;

    return 0;
}
```
**��Ӧ���**
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
**c����**
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    long long a = -100;

    return 0;
}
```
**��Ӧ���**
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
**c����**
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    char a = 100;

    return 0;
}
```
**��Ӧ���**
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
**c����**
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    unsigned char a = 100;

    return 0;
}
```
**��Ӧ���**
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
**c����**
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    char a = -100;

    return 0;
}
```
**��Ӧ���**
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
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    float a = 100.1;

    return 0;
}
```
**��Ӧ���**
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
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    float a = -100.1;

    return 0;
}
```
**��Ӧ���**
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
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    double a = 100.1;

    return 0;
}
```
**��Ӧ���**
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
**64λ��ֹ�������Ż�����ָ��**
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
**��Ӧ���**
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
**64λ��ֹ�������Ż�����ָ��**
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
**��Ӧ���**
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
**64λ��ֹ�������Ż�����ָ��**
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
**��Ӧ���**
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
**64λ��ֹ�������Ż�����ָ��**
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
**��Ӧ���**
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
**64λ��ֹ�������Ż�����ָ��**
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
**��Ӧ���**
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
**64λ��ֹ�������Ż�����ָ��**
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
**��Ӧ���**
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
**64λ��ֹ�������Ż�����ָ��**
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
**��Ӧ���**
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
**64λ��ֹ�������Ż�����ָ��**
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
**��Ӧ���**
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
**64λ��ֹ�������Ż�����ָ��**
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
**��Ӧ���**
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
**64λ��ֹ�������Ż�����ָ��**
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
**��Ӧ���**
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
**64λ��ֹ�������Ż�����ָ��**
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
**��Ӧ���**
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
**64λ��ֹ�������Ż�����ָ��**
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
**��Ӧ���**
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
**64λ��ֹ�������Ż�����ָ��**
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
**��Ӧ���**
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
**��ʾͼƬ**
![��ʾͼƬ](D:\�ĵ�\������Դ\����ʼ�\ReadingNote\REѧϰ�ʼ�\linux\X86_64\c\1.png)

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int i = 0;

    for (i = 0; i < 10; i++) {
    
    }

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004e4:   eb 04                   jmp    4004ea <main+0x18>
  4004e6:   83 45 fc 01             addl   $0x1,-0x4(%rbp)
  4004ea:   83 7d fc 09             cmpl   $0x9,-0x4(%rbp)
  4004ee:   7e f6                   jle    4004e6 <main+0x14>
  4004f0:   b8 00 00 00 00          mov    $0x0,%eax
  4004f5:   5d                      pop    %rbp
  4004f6:   c3                      retq
  4004f7:   66 0f 1f 84 00 00 00    nopw   0x0(%rax,%rax,1)
  4004fe:   00 00
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    for (;;) {
    
    }

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   eb fe                   jmp    4004d6 <main+0x4>
  4004d8:   0f 1f 84 00 00 00 00    nopl   0x0(%rax,%rax,1)
  4004df:   00
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int i = 0;

    for (;;) {
        i++; 
    }

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   83 45 fc 01             addl   $0x1,-0x4(%rbp)
  4004e1:   eb fa                   jmp    4004dd <main+0xb>
  4004e3:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  4004ea:   00 00 00
  4004ed:   0f 1f 00                nopl   (%rax)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int i = 0;
    int a = 0;

    for (i = 0; i < 10; i++) {
        a++; 
    }

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 00 00 00 00    movl   $0x0,-0x8(%rbp)
  4004e4:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004eb:   eb 08                   jmp    4004f5 <main+0x23>
  4004ed:   83 45 f8 01             addl   $0x1,-0x8(%rbp)
  4004f1:   83 45 fc 01             addl   $0x1,-0x4(%rbp)
  4004f5:   83 7d fc 09             cmpl   $0x9,-0x4(%rbp)
  4004f9:   7e f2                   jle    4004ed <main+0x1b>
  4004fb:   b8 00 00 00 00          mov    $0x0,%eax
  400500:   5d                      pop    %rbp
  400501:   c3                      retq
  400502:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  400509:   00 00 00
  40050c:   0f 1f 40 00             nopl   0x0(%rax)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    while (1) {}

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   eb fe                   jmp    4004d6 <main+0x4>
  4004d8:   0f 1f 84 00 00 00 00    nopl   0x0(%rax,%rax,1)
  4004df:   00
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;

    while (1) {
        a = 1; 
    }

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 fc 01 00 00 00    movl   $0x1,-0x4(%rbp)
  4004e4:   eb f7                   jmp    4004dd <main+0xb>
  4004e6:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  4004ed:   00 00 00
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int num = 10;
    int i = 0;
    int a = 0;

    while (i < num) {
        a = i;
        i++;
    }

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 f8 0a 00 00 00    movl   $0xa,-0x8(%rbp)
  4004dd:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004e4:   c7 45 f4 00 00 00 00    movl   $0x0,-0xc(%rbp)
  4004eb:   eb 0a                   jmp    4004f7 <main+0x25>
  4004ed:   8b 45 fc                mov    -0x4(%rbp),%eax
  4004f0:   89 45 f4                mov    %eax,-0xc(%rbp)
  4004f3:   83 45 fc 01             addl   $0x1,-0x4(%rbp)
  4004f7:   8b 45 fc                mov    -0x4(%rbp),%eax
  4004fa:   3b 45 f8                cmp    -0x8(%rbp),%eax
  4004fd:   7c ee                   jl     4004ed <main+0x1b>
  4004ff:   b8 00 00 00 00          mov    $0x0,%eax
  400504:   5d                      pop    %rbp
  400505:   c3                      retq
  400506:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  40050d:   00 00 00
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int num = 10;
    int i = 0;
    int a = 0;

    do {
        a = i;
        i++;
    } while (i < num);

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 f8 0a 00 00 00    movl   $0xa,-0x8(%rbp)
  4004dd:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004e4:   c7 45 f4 00 00 00 00    movl   $0x0,-0xc(%rbp)
  4004eb:   8b 45 fc                mov    -0x4(%rbp),%eax
  4004ee:   89 45 f4                mov    %eax,-0xc(%rbp)
  4004f1:   83 45 fc 01             addl   $0x1,-0x4(%rbp)
  4004f5:   8b 45 fc                mov    -0x4(%rbp),%eax
  4004f8:   3b 45 f8                cmp    -0x8(%rbp),%eax
  4004fb:   7c ee                   jl     4004eb <main+0x19>
  4004fd:   b8 00 00 00 00          mov    $0x0,%eax
  400502:   5d                      pop    %rbp
  400503:   c3                      retq
  400504:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  40050b:   00 00 00
  40050e:   66 90                   xchg   %ax,%ax
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 100;
    int b = 0;

    switch (a) {
    case 1:
       b = 1;
       break;
    case 2:
       b = 2;
    case 100:
       b = 3;
       break;
    default:
       b = 4;
    }

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 64 00 00 00    movl   $0x64,-0x4(%rbp)
  4004dd:   c7 45 f8 00 00 00 00    movl   $0x0,-0x8(%rbp)
  4004e4:   83 7d fc 64             cmpl   $0x64,-0x4(%rbp)
  4004e8:   74 24                   je     40050e <main+0x3c>
  4004ea:   83 7d fc 64             cmpl   $0x64,-0x4(%rbp)
  4004ee:   7f 27                   jg     400517 <main+0x45>
  4004f0:   83 7d fc 01             cmpl   $0x1,-0x4(%rbp)
  4004f4:   74 08                   je     4004fe <main+0x2c>
  4004f6:   83 7d fc 02             cmpl   $0x2,-0x4(%rbp)
  4004fa:   74 0b                   je     400507 <main+0x35>
  4004fc:   eb 19                   jmp    400517 <main+0x45>
  4004fe:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  400505:   eb 17                   jmp    40051e <main+0x4c>
  400507:   c7 45 f8 02 00 00 00    movl   $0x2,-0x8(%rbp)
  40050e:   c7 45 f8 03 00 00 00    movl   $0x3,-0x8(%rbp)
  400515:   eb 07                   jmp    40051e <main+0x4c>
  400517:   c7 45 f8 04 00 00 00    movl   $0x4,-0x8(%rbp)
  40051e:   b8 00 00 00 00          mov    $0x0,%eax
  400523:   5d                      pop    %rbp
  400524:   c3                      retq
  400525:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  40052c:   00 00 00
  40052f:   90                      nop
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a = b + c;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   8b 55 f8                mov    -0x8(%rbp),%edx
  4004ee:   8b 45 f4                mov    -0xc(%rbp),%eax
  4004f1:   01 d0                   add    %edx,%eax
  4004f3:   89 45 fc                mov    %eax,-0x4(%rbp)
  4004f6:   b8 00 00 00 00          mov    $0x0,%eax
  4004fb:   5d                      pop    %rbp
  4004fc:   c3                      retq
  4004fd:   0f 1f 00                nopl   (%rax)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = -1;
    int c = -2;

    a = b + c;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 ff ff ff ff    movl   $0xffffffff,-0x8(%rbp)
  4004e4:   c7 45 f4 fe ff ff ff    movl   $0xfffffffe,-0xc(%rbp)
  4004eb:   8b 55 f8                mov    -0x8(%rbp),%edx
  4004ee:   8b 45 f4                mov    -0xc(%rbp),%eax
  4004f1:   01 d0                   add    %edx,%eax
  4004f3:   89 45 fc                mov    %eax,-0x4(%rbp)
  4004f6:   b8 00 00 00 00          mov    $0x0,%eax
  4004fb:   5d                      pop    %rbp
  4004fc:   c3                      retq
  4004fd:   0f 1f 00                nopl   (%rax)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a = b - c;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   8b 45 f8                mov    -0x8(%rbp),%eax
  4004ee:   2b 45 f4                sub    -0xc(%rbp),%eax
  4004f1:   89 45 fc                mov    %eax,-0x4(%rbp)
  4004f4:   b8 00 00 00 00          mov    $0x0,%eax
  4004f9:   5d                      pop    %rbp
  4004fa:   c3                      retq
  4004fb:   0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = -1;
    int c = -2;

    a = b - c;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 ff ff ff ff    movl   $0xffffffff,-0x8(%rbp)
  4004e4:   c7 45 f4 fe ff ff ff    movl   $0xfffffffe,-0xc(%rbp)
  4004eb:   8b 45 f8                mov    -0x8(%rbp),%eax
  4004ee:   2b 45 f4                sub    -0xc(%rbp),%eax
  4004f1:   89 45 fc                mov    %eax,-0x4(%rbp)
  4004f4:   b8 00 00 00 00          mov    $0x0,%eax
  4004f9:   5d                      pop    %rbp
  4004fa:   c3                      retq
  4004fb:   0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a = b * c;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   8b 45 f8                mov    -0x8(%rbp),%eax
  4004ee:   0f af 45 f4             imul   -0xc(%rbp),%eax
  4004f2:   89 45 fc                mov    %eax,-0x4(%rbp)
  4004f5:   b8 00 00 00 00          mov    $0x0,%eax
  4004fa:   5d                      pop    %rbp
  4004fb:   c3                      retq
  4004fc:   0f 1f 40 00             nopl   0x0(%rax)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a = b / c;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   8b 45 f8                mov    -0x8(%rbp),%eax
  4004ee:   99                      cltd
  4004ef:   f7 7d f4                idivl  -0xc(%rbp)
  4004f2:   89 45 fc                mov    %eax,-0x4(%rbp)
  4004f5:   b8 00 00 00 00          mov    $0x0,%eax
  4004fa:   5d                      pop    %rbp
  4004fb:   c3                      retq
  4004fc:   0f 1f 40 00             nopl   0x0(%rax)
```
**���ָ��ѧϰ**
> cltd converts the signed long in EAX to a signed double long in EDX:EAX by extending the most-significant bit (sign bit) of EAX into all bits of EDX.

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a = b % c;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   8b 45 f8                mov    -0x8(%rbp),%eax
  4004ee:   99                      cltd
  4004ef:   f7 7d f4                idivl  -0xc(%rbp)
  4004f2:   89 55 fc                mov    %edx,-0x4(%rbp)
  4004f5:   b8 00 00 00 00          mov    $0x0,%eax
  4004fa:   5d                      pop    %rbp
  4004fb:   c3                      retq
  4004fc:   0f 1f 40 00             nopl   0x0(%rax)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a = sizeof(b);

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   c7 45 fc 04 00 00 00    movl   $0x4,-0x4(%rbp)
  4004f2:   b8 00 00 00 00          mov    $0x0,%eax
  4004f7:   5d                      pop    %rbp
  4004f8:   c3                      retq
  4004f9:   0f 1f 80 00 00 00 00    nopl   0x0(%rax)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a = b << 2;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   8b 45 f8                mov    -0x8(%rbp),%eax
  4004ee:   c1 e0 02                shl    $0x2,%eax
  4004f1:   89 45 fc                mov    %eax,-0x4(%rbp)
  4004f4:   b8 00 00 00 00          mov    $0x0,%eax
  4004f9:   5d                      pop    %rbp
  4004fa:   c3                      retq
  4004fb:   0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a = b >> 2;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   8b 45 f8                mov    -0x8(%rbp),%eax
  4004ee:   c1 f8 02                sar    $0x2,%eax
  4004f1:   89 45 fc                mov    %eax,-0x4(%rbp)
  4004f4:   b8 00 00 00 00          mov    $0x0,%eax
  4004f9:   5d                      pop    %rbp
  4004fa:   c3                      retq
  4004fb:   0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a = b & c;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   8b 45 f8                mov    -0x8(%rbp),%eax
  4004ee:   23 45 f4                and    -0xc(%rbp),%eax
  4004f1:   89 45 fc                mov    %eax,-0x4(%rbp)
  4004f4:   b8 00 00 00 00          mov    $0x0,%eax
  4004f9:   5d                      pop    %rbp
  4004fa:   c3                      retq
  4004fb:   0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a = b | c;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   8b 45 f8                mov    -0x8(%rbp),%eax
  4004ee:   0b 45 f4                or     -0xc(%rbp),%eax
  4004f1:   89 45 fc                mov    %eax,-0x4(%rbp)
  4004f4:   b8 00 00 00 00          mov    $0x0,%eax
  4004f9:   5d                      pop    %rbp
  4004fa:   c3                      retq
  4004fb:   0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a = b ^ c;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   8b 45 f8                mov    -0x8(%rbp),%eax
  4004ee:   33 45 f4                xor    -0xc(%rbp),%eax
  4004f1:   89 45 fc                mov    %eax,-0x4(%rbp)
  4004f4:   b8 00 00 00 00          mov    $0x0,%eax
  4004f9:   5d                      pop    %rbp
  4004fa:   c3                      retq
  4004fb:   0f 1f 44 00 00          nopl   0x0(%rax,%rax,1)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a = b && c;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   83 7d f8 00             cmpl   $0x0,-0x8(%rbp)
  4004ef:   74 0d                   je     4004fe <main+0x2c>
  4004f1:   83 7d f4 00             cmpl   $0x0,-0xc(%rbp)
  4004f5:   74 07                   je     4004fe <main+0x2c>
  4004f7:   b8 01 00 00 00          mov    $0x1,%eax
  4004fc:   eb 05                   jmp    400503 <main+0x31>
  4004fe:   b8 00 00 00 00          mov    $0x0,%eax
  400503:   89 45 fc                mov    %eax,-0x4(%rbp)
  400506:   b8 00 00 00 00          mov    $0x0,%eax
  40050b:   5d                      pop    %rbp
  40050c:   c3                      retq
  40050d:   0f 1f 00                nopl   (%rax)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a = b || c;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   83 7d f8 00             cmpl   $0x0,-0x8(%rbp)
  4004ef:   75 06                   jne    4004f7 <main+0x25>
  4004f1:   83 7d f4 00             cmpl   $0x0,-0xc(%rbp)
  4004f5:   74 07                   je     4004fe <main+0x2c>
  4004f7:   b8 01 00 00 00          mov    $0x1,%eax
  4004fc:   eb 05                   jmp    400503 <main+0x31>
  4004fe:   b8 00 00 00 00          mov    $0x0,%eax
  400503:   89 45 fc                mov    %eax,-0x4(%rbp)
  400506:   b8 00 00 00 00          mov    $0x0,%eax
  40050b:   5d                      pop    %rbp
  40050c:   c3                      retq
  40050d:   0f 1f 00                nopl   (%rax)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a = b ? b : c;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   83 7d f8 00             cmpl   $0x0,-0x8(%rbp)
  4004ef:   74 05                   je     4004f6 <main+0x24>
  4004f1:   8b 45 f8                mov    -0x8(%rbp),%eax
  4004f4:   eb 03                   jmp    4004f9 <main+0x27>
  4004f6:   8b 45 f4                mov    -0xc(%rbp),%eax
  4004f9:   89 45 fc                mov    %eax,-0x4(%rbp)
  4004fc:   b8 00 00 00 00          mov    $0x0,%eax
  400501:   5d                      pop    %rbp
  400502:   c3                      retq
  400503:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  40050a:   00 00 00
  40050d:   0f 1f 00                nopl   (%rax)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a == b ? b : c;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   8b 45 fc                mov    -0x4(%rbp),%eax
  4004ee:   3b 45 f8                cmp    -0x8(%rbp),%eax
  4004f1:   b8 00 00 00 00          mov    $0x0,%eax
  4004f6:   5d                      pop    %rbp
  4004f7:   c3                      retq
  4004f8:   0f 1f 84 00 00 00 00    nopl   0x0(%rax,%rax,1)
  4004ff:   00
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a = (a == b ? b : c);

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   8b 45 fc                mov    -0x4(%rbp),%eax
  4004ee:   3b 45 f8                cmp    -0x8(%rbp),%eax
  4004f1:   75 05                   jne    4004f8 <main+0x26>
  4004f3:   8b 45 f8                mov    -0x8(%rbp),%eax
  4004f6:   eb 03                   jmp    4004fb <main+0x29>
  4004f8:   8b 45 f4                mov    -0xc(%rbp),%eax
  4004fb:   89 45 fc                mov    %eax,-0x4(%rbp)
  4004fe:   b8 00 00 00 00          mov    $0x0,%eax
  400503:   5d                      pop    %rbp
  400504:   c3                      retq
  400505:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  40050c:   00 00 00
  40050f:   90                      nop
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a = (0, c);

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   8b 45 f4                mov    -0xc(%rbp),%eax
  4004ee:   89 45 fc                mov    %eax,-0x4(%rbp)
  4004f1:   b8 00 00 00 00          mov    $0x0,%eax
  4004f6:   5d                      pop    %rbp
  4004f7:   c3                      retq
  4004f8:   0f 1f 84 00 00 00 00    nopl   0x0(%rax,%rax,1)
  4004ff:   00
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a = 0, c;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004f2:   b8 00 00 00 00          mov    $0x0,%eax
  4004f7:   5d                      pop    %rbp
  4004f8:   c3                      retq
  4004f9:   0f 1f 80 00 00 00 00    nopl   0x0(%rax)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a, c;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   b8 00 00 00 00          mov    $0x0,%eax
  4004f0:   5d                      pop    %rbp
  4004f1:   c3                      retq
  4004f2:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  4004f9:   00 00 00
  4004fc:   0f 1f 40 00             nopl   0x0(%rax)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a += c;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   8b 45 f4                mov    -0xc(%rbp),%eax
  4004ee:   01 45 fc                add    %eax,-0x4(%rbp)
  4004f1:   b8 00 00 00 00          mov    $0x0,%eax
  4004f6:   5d                      pop    %rbp
  4004f7:   c3                      retq
  4004f8:   0f 1f 84 00 00 00 00    nopl   0x0(%rax,%rax,1)
  4004ff:   00
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a -= c;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   8b 45 f4                mov    -0xc(%rbp),%eax
  4004ee:   29 45 fc                sub    %eax,-0x4(%rbp)
  4004f1:   b8 00 00 00 00          mov    $0x0,%eax
  4004f6:   5d                      pop    %rbp
  4004f7:   c3                      retq
  4004f8:   0f 1f 84 00 00 00 00    nopl   0x0(%rax,%rax,1)
  4004ff:   00
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a *= c;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   8b 45 fc                mov    -0x4(%rbp),%eax
  4004ee:   0f af 45 f4             imul   -0xc(%rbp),%eax
  4004f2:   89 45 fc                mov    %eax,-0x4(%rbp)
  4004f5:   b8 00 00 00 00          mov    $0x0,%eax
  4004fa:   5d                      pop    %rbp
  4004fb:   c3                      retq
  4004fc:   0f 1f 40 00             nopl   0x0(%rax)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a /= c;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   8b 45 fc                mov    -0x4(%rbp),%eax
  4004ee:   99                      cltd
  4004ef:   f7 7d f4                idivl  -0xc(%rbp)
  4004f2:   89 45 fc                mov    %eax,-0x4(%rbp)
  4004f5:   b8 00 00 00 00          mov    $0x0,%eax
  4004fa:   5d                      pop    %rbp
  4004fb:   c3                      retq
  4004fc:   0f 1f 40 00             nopl   0x0(%rax)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int main() {
    int a = 0;
    int b = 1;
    int c = 2;

    a %= c;

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <main>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   c7 45 fc 00 00 00 00    movl   $0x0,-0x4(%rbp)
  4004dd:   c7 45 f8 01 00 00 00    movl   $0x1,-0x8(%rbp)
  4004e4:   c7 45 f4 02 00 00 00    movl   $0x2,-0xc(%rbp)
  4004eb:   8b 45 fc                mov    -0x4(%rbp),%eax
  4004ee:   99                      cltd
  4004ef:   f7 7d f4                idivl  -0xc(%rbp)
  4004f2:   89 55 fc                mov    %edx,-0x4(%rbp)
  4004f5:   b8 00 00 00 00          mov    $0x0,%eax
  4004fa:   5d                      pop    %rbp
  4004fb:   c3                      retq
  4004fc:   0f 1f 40 00             nopl   0x0(%rax)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int func() {
    return 0;
}

int main() {

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <func>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   b8 00 00 00 00          mov    $0x0,%eax
  4004db:   5d                      pop    %rbp
  4004dc:   c3                      retq

00000000004004dd <main>:
  4004dd:   55                      push   %rbp
  4004de:   48 89 e5                mov    %rsp,%rbp
  4004e1:   b8 00 00 00 00          mov    $0x0,%eax
  4004e6:   5d                      pop    %rbp
  4004e7:   c3                      retq
  4004e8:   0f 1f 84 00 00 00 00    nopl   0x0(%rax,%rax,1)
  4004ef:   00
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int func() {
    return 0;
}

int main() {
    func(); 

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <func>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   b8 00 00 00 00          mov    $0x0,%eax
  4004db:   5d                      pop    %rbp
  4004dc:   c3                      retq

00000000004004dd <main>:
  4004dd:   55                      push   %rbp
  4004de:   48 89 e5                mov    %rsp,%rbp
  4004e1:   b8 00 00 00 00          mov    $0x0,%eax
  4004e6:   e8 e7 ff ff ff          callq  4004d2 <func>
  4004eb:   b8 00 00 00 00          mov    $0x0,%eax
  4004f0:   5d                      pop    %rbp
  4004f1:   c3                      retq
  4004f2:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  4004f9:   00 00 00
  4004fc:   0f 1f 40 00             nopl   0x0(%rax)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int func(int a) {
    return 0;
}

int main() {
    int a = 1;

    func(a); 

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <func>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   89 7d fc                mov    %edi,-0x4(%rbp)
  4004d9:   b8 00 00 00 00          mov    $0x0,%eax
  4004de:   5d                      pop    %rbp
  4004df:   c3                      retq

00000000004004e0 <main>:
  4004e0:   55                      push   %rbp
  4004e1:   48 89 e5                mov    %rsp,%rbp
  4004e4:   48 83 ec 10             sub    $0x10,%rsp
  4004e8:   c7 45 fc 01 00 00 00    movl   $0x1,-0x4(%rbp)
  4004ef:   8b 45 fc                mov    -0x4(%rbp),%eax
  4004f2:   89 c7                   mov    %eax,%edi
  4004f4:   e8 d9 ff ff ff          callq  4004d2 <func>
  4004f9:   b8 00 00 00 00          mov    $0x0,%eax
  4004fe:   c9                      leaveq
  4004ff:   c3                      retq
```
**64λ�������ù�Լ**
![calling convention](D:\�ĵ�\������Դ\����ʼ�\ReadingNote\REѧϰ�ʼ�\linux\X86_64\c\2.png)
[calling convention wiki](https://en.wikipedia.org/wiki/X86_calling_conventions)


---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int func(int a, int b, int c) {
    return 0;
}

int main() {
    int a = 1;
    int b = 2;
    int c = 3;

    func(a, b, c); 

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <func>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   89 7d fc                mov    %edi,-0x4(%rbp)
  4004d9:   89 75 f8                mov    %esi,-0x8(%rbp)
  4004dc:   89 55 f4                mov    %edx,-0xc(%rbp)
  4004df:   b8 00 00 00 00          mov    $0x0,%eax
  4004e4:   5d                      pop    %rbp
  4004e5:   c3                      retq

00000000004004e6 <main>:
  4004e6:   55                      push   %rbp
  4004e7:   48 89 e5                mov    %rsp,%rbp
  4004ea:   48 83 ec 10             sub    $0x10,%rsp
  4004ee:   c7 45 fc 01 00 00 00    movl   $0x1,-0x4(%rbp)
  4004f5:   c7 45 f8 02 00 00 00    movl   $0x2,-0x8(%rbp)
  4004fc:   c7 45 f4 03 00 00 00    movl   $0x3,-0xc(%rbp)
  400503:   8b 55 f4                mov    -0xc(%rbp),%edx
  400506:   8b 4d f8                mov    -0x8(%rbp),%ecx
  400509:   8b 45 fc                mov    -0x4(%rbp),%eax
  40050c:   89 ce                   mov    %ecx,%esi
  40050e:   89 c7                   mov    %eax,%edi
  400510:   e8 bd ff ff ff          callq  4004d2 <func>
  400515:   b8 00 00 00 00          mov    $0x0,%eax
  40051a:   c9                      leaveq
  40051b:   c3                      retq
  40051c:   0f 1f 40 00             nopl   0x0(%rax)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int func(int a, int b, int c, int d, int e, int f, int g, int h, int i, int j, int k) {
  
    return 0;
}

int main() {
    int a = 1;
    int b = 2;
    int c = 3;
    int d = 4;
    int e = 5;
    int f = 6;
    int g = 7;
    int h = 8;
    int i = 9;
    int j = 10;
    int k = 11;

    func(a, b, c, d, e, f, g, h, i, j, k);

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <func>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   89 7d fc                mov    %edi,-0x4(%rbp)
  4004d9:   89 75 f8                mov    %esi,-0x8(%rbp)
  4004dc:   89 55 f4                mov    %edx,-0xc(%rbp)
  4004df:   89 4d f0                mov    %ecx,-0x10(%rbp)
  4004e2:   44 89 45 ec             mov    %r8d,-0x14(%rbp)
  4004e6:   44 89 4d e8             mov    %r9d,-0x18(%rbp)
  4004ea:   b8 00 00 00 00          mov    $0x0,%eax
  4004ef:   5d                      pop    %rbp
  4004f0:   c3                      retq

00000000004004f1 <main>:
  4004f1:   55                      push   %rbp
  4004f2:   48 89 e5                mov    %rsp,%rbp
  4004f5:   48 83 ec 30             sub    $0x30,%rsp
  4004f9:   c7 45 fc 01 00 00 00    movl   $0x1,-0x4(%rbp)
  400500:   c7 45 f8 02 00 00 00    movl   $0x2,-0x8(%rbp)
  400507:   c7 45 f4 03 00 00 00    movl   $0x3,-0xc(%rbp)
  40050e:   c7 45 f0 04 00 00 00    movl   $0x4,-0x10(%rbp)
  400515:   c7 45 ec 05 00 00 00    movl   $0x5,-0x14(%rbp)
  40051c:   c7 45 e8 06 00 00 00    movl   $0x6,-0x18(%rbp)
  400523:   c7 45 e4 07 00 00 00    movl   $0x7,-0x1c(%rbp)
  40052a:   c7 45 e0 08 00 00 00    movl   $0x8,-0x20(%rbp)
  400531:   c7 45 dc 09 00 00 00    movl   $0x9,-0x24(%rbp)
  400538:   c7 45 d8 0a 00 00 00    movl   $0xa,-0x28(%rbp)
  40053f:   c7 45 d4 0b 00 00 00    movl   $0xb,-0x2c(%rbp)
  400546:   44 8b 4d e8             mov    -0x18(%rbp),%r9d
  40054a:   44 8b 45 ec             mov    -0x14(%rbp),%r8d
  40054e:   8b 4d f0                mov    -0x10(%rbp),%ecx
  400551:   8b 55 f4                mov    -0xc(%rbp),%edx
  400554:   8b 75 f8                mov    -0x8(%rbp),%esi
  400557:   8b 45 fc                mov    -0x4(%rbp),%eax
  40055a:   8b 7d d4                mov    -0x2c(%rbp),%edi
  40055d:   57                      push   %rdi
  40055e:   8b 7d d8                mov    -0x28(%rbp),%edi
  400561:   57                      push   %rdi
  400562:   8b 7d dc                mov    -0x24(%rbp),%edi
  400565:   57                      push   %rdi
  400566:   8b 7d e0                mov    -0x20(%rbp),%edi
  400569:   57                      push   %rdi
  40056a:   8b 7d e4                mov    -0x1c(%rbp),%edi
  40056d:   57                      push   %rdi
  40056e:   89 c7                   mov    %eax,%edi
  400570:   e8 5d ff ff ff          callq  4004d2 <func>
  400575:   48 83 c4 28             add    $0x28,%rsp
  400579:   b8 00 00 00 00          mov    $0x0,%eax
  40057e:   c9                      leaveq
  40057f:   c3                      retq
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int func(int a, int b, int c, int d, int e, int f, int g, int h, int i, int j, int k) {
    a++;
    b++;
    c++;
    d++;
    e++;
    f++;
    g++;
    h++;
    i++;
    j++;
    k++;
  
    return 0;
}

int main() {
    int a = 1;
    int b = 2;
    int c = 3;
    int d = 4;
    int e = 5;
    int f = 6;
    int g = 7;
    int h = 8;
    int i = 9;
    int j = 10;
    int k = 11;

    func(a, b, c, d, e, f, g, h, i, j, k);

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <func>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   89 7d fc                mov    %edi,-0x4(%rbp)
  4004d9:   89 75 f8                mov    %esi,-0x8(%rbp)
  4004dc:   89 55 f4                mov    %edx,-0xc(%rbp)
  4004df:   89 4d f0                mov    %ecx,-0x10(%rbp)
  4004e2:   44 89 45 ec             mov    %r8d,-0x14(%rbp)
  4004e6:   44 89 4d e8             mov    %r9d,-0x18(%rbp)
  4004ea:   83 45 fc 01             addl   $0x1,-0x4(%rbp)
  4004ee:   83 45 f8 01             addl   $0x1,-0x8(%rbp)
  4004f2:   83 45 f4 01             addl   $0x1,-0xc(%rbp)
  4004f6:   83 45 f0 01             addl   $0x1,-0x10(%rbp)
  4004fa:   83 45 ec 01             addl   $0x1,-0x14(%rbp)
  4004fe:   83 45 e8 01             addl   $0x1,-0x18(%rbp)
  400502:   83 45 10 01             addl   $0x1,0x10(%rbp)
  400506:   83 45 18 01             addl   $0x1,0x18(%rbp)
  40050a:   83 45 20 01             addl   $0x1,0x20(%rbp)
  40050e:   83 45 28 01             addl   $0x1,0x28(%rbp)
  400512:   83 45 30 01             addl   $0x1,0x30(%rbp)
  400516:   b8 00 00 00 00          mov    $0x0,%eax
  40051b:   5d                      pop    %rbp
  40051c:   c3                      retq

000000000040051d <main>:
  40051d:   55                      push   %rbp
  40051e:   48 89 e5                mov    %rsp,%rbp
  400521:   48 83 ec 30             sub    $0x30,%rsp
  400525:   c7 45 fc 01 00 00 00    movl   $0x1,-0x4(%rbp)
  40052c:   c7 45 f8 02 00 00 00    movl   $0x2,-0x8(%rbp)
  400533:   c7 45 f4 03 00 00 00    movl   $0x3,-0xc(%rbp)
  40053a:   c7 45 f0 04 00 00 00    movl   $0x4,-0x10(%rbp)
  400541:   c7 45 ec 05 00 00 00    movl   $0x5,-0x14(%rbp)
  400548:   c7 45 e8 06 00 00 00    movl   $0x6,-0x18(%rbp)
  40054f:   c7 45 e4 07 00 00 00    movl   $0x7,-0x1c(%rbp)
  400556:   c7 45 e0 08 00 00 00    movl   $0x8,-0x20(%rbp)
  40055d:   c7 45 dc 09 00 00 00    movl   $0x9,-0x24(%rbp)
  400564:   c7 45 d8 0a 00 00 00    movl   $0xa,-0x28(%rbp)
  40056b:   c7 45 d4 0b 00 00 00    movl   $0xb,-0x2c(%rbp)
  400572:   44 8b 4d e8             mov    -0x18(%rbp),%r9d
  400576:   44 8b 45 ec             mov    -0x14(%rbp),%r8d
  40057a:   8b 4d f0                mov    -0x10(%rbp),%ecx
  40057d:   8b 55 f4                mov    -0xc(%rbp),%edx
  400580:   8b 75 f8                mov    -0x8(%rbp),%esi
  400583:   8b 45 fc                mov    -0x4(%rbp),%eax
  400586:   8b 7d d4                mov    -0x2c(%rbp),%edi
  400589:   57                      push   %rdi
  40058a:   8b 7d d8                mov    -0x28(%rbp),%edi
  40058d:   57                      push   %rdi
  40058e:   8b 7d dc                mov    -0x24(%rbp),%edi
  400591:   57                      push   %rdi
  400592:   8b 7d e0                mov    -0x20(%rbp),%edi
  400595:   57                      push   %rdi
  400596:   8b 7d e4                mov    -0x1c(%rbp),%edi
  400599:   57                      push   %rdi
  40059a:   89 c7                   mov    %eax,%edi
  40059c:   e8 31 ff ff ff          callq  4004d2 <func>
  4005a1:   48 83 c4 28             add    $0x28,%rsp
  4005a5:   b8 00 00 00 00          mov    $0x0,%eax
  4005aa:   c9                      leaveq
  4005ab:   c3                      retq
  4005ac:   0f 1f 40 00             nopl   0x0(%rax)
```
**��ʾͼƬ**
![�������ù�Լ](D:\�ĵ�\������Դ\����ʼ�\ReadingNote\REѧϰ�ʼ�\linux\X86_64\c\3.png)

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
int func(int a, int b, int c, int d, int e, int f, int g, int h, int i, int j, int k) {
    return func(a, b, c, d, e, f, g, h, i, j, k);
}

int main() {
    int a = 1;
    int b = 2;
    int c = 3;
    int d = 4;
    int e = 5;
    int f = 6;
    int g = 7;
    int h = 8;
    int i = 9;
    int j = 10;
    int k = 11;

    func(a, b, c, d, e, f, g, h, i, j, k);

    return 0;
}
```
**��Ӧ���**
```asm
00000000004004d2 <func>:
  4004d2:   55                      push   %rbp
  4004d3:   48 89 e5                mov    %rsp,%rbp
  4004d6:   48 83 ec 20             sub    $0x20,%rsp
  4004da:   89 7d fc                mov    %edi,-0x4(%rbp)
  4004dd:   89 75 f8                mov    %esi,-0x8(%rbp)
  4004e0:   89 55 f4                mov    %edx,-0xc(%rbp)
  4004e3:   89 4d f0                mov    %ecx,-0x10(%rbp)
  4004e6:   44 89 45 ec             mov    %r8d,-0x14(%rbp)
  4004ea:   44 89 4d e8             mov    %r9d,-0x18(%rbp)
  4004ee:   44 8b 4d e8             mov    -0x18(%rbp),%r9d
  4004f2:   44 8b 45 ec             mov    -0x14(%rbp),%r8d
  4004f6:   8b 4d f0                mov    -0x10(%rbp),%ecx
  4004f9:   8b 55 f4                mov    -0xc(%rbp),%edx
  4004fc:   8b 75 f8                mov    -0x8(%rbp),%esi
  4004ff:   8b 45 fc                mov    -0x4(%rbp),%eax
  400502:   48 83 ec 08             sub    $0x8,%rsp
  400506:   8b 7d 30                mov    0x30(%rbp),%edi
  400509:   57                      push   %rdi
  40050a:   8b 7d 28                mov    0x28(%rbp),%edi
  40050d:   57                      push   %rdi
  40050e:   8b 7d 20                mov    0x20(%rbp),%edi
  400511:   57                      push   %rdi
  400512:   8b 7d 18                mov    0x18(%rbp),%edi
  400515:   57                      push   %rdi
  400516:   8b 7d 10                mov    0x10(%rbp),%edi
  400519:   57                      push   %rdi
  40051a:   89 c7                   mov    %eax,%edi
  40051c:   e8 b1 ff ff ff          callq  4004d2 <func>
  400521:   48 83 c4 30             add    $0x30,%rsp
  400525:   c9                      leaveq
  400526:   c3                      retq

0000000000400527 <main>:
  400527:   55                      push   %rbp
  400528:   48 89 e5                mov    %rsp,%rbp
  40052b:   48 83 ec 30             sub    $0x30,%rsp
  40052f:   c7 45 fc 01 00 00 00    movl   $0x1,-0x4(%rbp)
  400536:   c7 45 f8 02 00 00 00    movl   $0x2,-0x8(%rbp)
  40053d:   c7 45 f4 03 00 00 00    movl   $0x3,-0xc(%rbp)
  400544:   c7 45 f0 04 00 00 00    movl   $0x4,-0x10(%rbp)
  40054b:   c7 45 ec 05 00 00 00    movl   $0x5,-0x14(%rbp)
  400552:   c7 45 e8 06 00 00 00    movl   $0x6,-0x18(%rbp)
  400559:   c7 45 e4 07 00 00 00    movl   $0x7,-0x1c(%rbp)
  400560:   c7 45 e0 08 00 00 00    movl   $0x8,-0x20(%rbp)
  400567:   c7 45 dc 09 00 00 00    movl   $0x9,-0x24(%rbp)
  40056e:   c7 45 d8 0a 00 00 00    movl   $0xa,-0x28(%rbp)
  400575:   c7 45 d4 0b 00 00 00    movl   $0xb,-0x2c(%rbp)
  40057c:   44 8b 4d e8             mov    -0x18(%rbp),%r9d
  400580:   44 8b 45 ec             mov    -0x14(%rbp),%r8d
  400584:   8b 4d f0                mov    -0x10(%rbp),%ecx
  400587:   8b 55 f4                mov    -0xc(%rbp),%edx
  40058a:   8b 75 f8                mov    -0x8(%rbp),%esi
  40058d:   8b 45 fc                mov    -0x4(%rbp),%eax
  400590:   48 83 ec 08             sub    $0x8,%rsp
  400594:   8b 7d d4                mov    -0x2c(%rbp),%edi
  400597:   57                      push   %rdi
  400598:   8b 7d d8                mov    -0x28(%rbp),%edi
  40059b:   57                      push   %rdi
  40059c:   8b 7d dc                mov    -0x24(%rbp),%edi
  40059f:   57                      push   %rdi
  4005a0:   8b 7d e0                mov    -0x20(%rbp),%edi
  4005a3:   57                      push   %rdi
  4005a4:   8b 7d e4                mov    -0x1c(%rbp),%edi
  4005a7:   57                      push   %rdi
  4005a8:   89 c7                   mov    %eax,%edi
  4005aa:   e8 23 ff ff ff          callq  4004d2 <func>
  4005af:   48 83 c4 30             add    $0x30,%rsp
  4005b3:   b8 00 00 00 00          mov    $0x0,%eax
  4005b8:   c9                      leaveq
  4005b9:   c3                      retq
  4005ba:   66 0f 1f 44 00 00       nopw   0x0(%rax,%rax,1)
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
#include <stdio.h>
  
void func(int a) {
    printf("%d\n", a);
}

int main() {
    int a = 1;

    func(a);

    return 0;
}
```
**��Ӧ���**
```asm
0000000000400512 <func>:
  400512:   55                      push   %rbp
  400513:   48 89 e5                mov    %rsp,%rbp
  400516:   48 83 ec 10             sub    $0x10,%rsp
  40051a:   89 7d fc                mov    %edi,-0x4(%rbp)
  40051d:   8b 45 fc                mov    -0x4(%rbp),%eax
  400520:   89 c6                   mov    %eax,%esi
  400522:   bf e4 05 40 00          mov    $0x4005e4,%edi
  400527:   b8 00 00 00 00          mov    $0x0,%eax
  40052c:   e8 df fe ff ff          callq  400410 <printf@plt>
  400531:   90                      nop
  400532:   c9                      leaveq
  400533:   c3                      retq

0000000000400534 <main>:
  400534:   55                      push   %rbp
  400535:   48 89 e5                mov    %rsp,%rbp
  400538:   48 83 ec 10             sub    $0x10,%rsp
  40053c:   c7 45 fc 01 00 00 00    movl   $0x1,-0x4(%rbp)
  400543:   8b 45 fc                mov    -0x4(%rbp),%eax
  400546:   89 c7                   mov    %eax,%edi
  400548:   e8 c5 ff ff ff          callq  400512 <func>
  40054d:   b8 00 00 00 00          mov    $0x0,%eax
  400552:   c9                      leaveq
  400553:   c3                      retq
  400554:   66 2e 0f 1f 84 00 00    nopw   %cs:0x0(%rax,%rax,1)
  40055b:   00 00 00
  40055e:   66 90                   xchg   %ax,%ax

Contents of section .rodata:
 4005e0 01000200 25640a00                    ....%d..
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
#include <stdio.h>
  
void func(char *name) {
    printf("%s\n", name);
}

int main() {
    char *name = "jiangziqi";

    func(name);

    return 0;
}
```
**��Ӧ���**
```asm
0000000000400512 <func>:
  400512:   55                      push   %rbp
  400513:   48 89 e5                mov    %rsp,%rbp
  400516:   48 83 ec 10             sub    $0x10,%rsp
  40051a:   48 89 7d f8             mov    %rdi,-0x8(%rbp)
  40051e:   48 8b 45 f8             mov    -0x8(%rbp),%rax
  400522:   48 89 c7                mov    %rax,%rdi
  400525:   e8 e6 fe ff ff          callq  400410 <puts@plt>
  40052a:   90                      nop
  40052b:   c9                      leaveq
  40052c:   c3                      retq

000000000040052d <main>:
  40052d:   55                      push   %rbp
  40052e:   48 89 e5                mov    %rsp,%rbp
  400531:   48 83 ec 10             sub    $0x10,%rsp
  400535:   48 c7 45 f8 d4 05 40    movq   $0x4005d4,-0x8(%rbp)
  40053c:   00
  40053d:   48 8b 45 f8             mov    -0x8(%rbp),%rax
  400541:   48 89 c7                mov    %rax,%rdi
  400544:   e8 c9 ff ff ff          callq  400512 <func>
  400549:   b8 00 00 00 00          mov    $0x0,%eax
  40054e:   c9                      leaveq
  40054f:   c3                      retq

Contents of section .rodata:
  4005d0 01000200 6a69616e 677a6971 6900      ....jiangziqi.
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
#include <stdio.h>
  
int main(void) {
    FILE *fp = NULL;
    fp = fopen("/tmp/iii", "rw");

    return 0;
}
```
**��Ӧ���**
```asm
0000000000400512 <main>:
  400512:   55                      push   %rbp
  400513:   48 89 e5                mov    %rsp,%rbp
  400516:   48 83 ec 10             sub    $0x10,%rsp
  40051a:   48 c7 45 f8 00 00 00    movq   $0x0,-0x8(%rbp)
  400521:   00
  400522:   be c4 05 40 00          mov    $0x4005c4,%esi
  400527:   bf c7 05 40 00          mov    $0x4005c7,%edi
  40052c:   e8 ff fe ff ff          callq  400430 <fopen@plt>
  400531:   48 89 45 f8             mov    %rax,-0x8(%rbp)
  400535:   b8 00 00 00 00          mov    $0x0,%eax
  40053a:   c9                      leaveq
  40053b:   c3                      retq
  40053c:   0f 1f 40 00             nopl   0x0(%rax)

Contents of section .rodata:
  4005c0 01000200 7277002f 746d702f 69696900  ....rw./tmp/iii.
```

---
**64λ��ֹ�������Ż�����ָ��**
```
gcc 1.c -o 1 -O0
```
```c
#include <stdio.h>
#include <string.h>

int main(void) {
    FILE *fp = NULL;
    char buff[4096] = { '\0' };

    fp = fopen("/dev/random", "r");

    while ((fread(buff, 1, sizeof(buff) - 1, fp)) < (sizeof(buff) - 1)) {
        printf("%s\n", buff);
        memset(buff, 0, sizeof(buff));
    }

    return 0;
}
```
**��Ӧ���**
```asm
00000000004005f2 <main>:
  4005f2:   55                      push   %rbp
  4005f3:   48 89 e5                mov    %rsp,%rbp
  4005f6:   48 81 ec 10 10 00 00    sub    $0x1010,%rsp
  4005fd:   48 c7 45 f8 00 00 00    movq   $0x0,-0x8(%rbp)
  400604:   00
  400605:   48 c7 85 f0 ef ff ff    movq   $0x0,-0x1010(%rbp)
  40060c:   00 00 00 00
  400610:   48 c7 85 f8 ef ff ff    movq   $0x0,-0x1008(%rbp)
  400617:   00 00 00 00
  40061b:   48 8d 95 00 f0 ff ff    lea    -0x1000(%rbp),%rdx
  400622:   b8 00 00 00 00          mov    $0x0,%eax
  400627:   b9 fe 01 00 00          mov    $0x1fe,%ecx
  40062c:   48 89 d7                mov    %rdx,%rdi
  40062f:   f3 48 ab                rep stos %rax,%es:(%rdi)
  400632:   be 24 07 40 00          mov    $0x400724,%esi
  400637:   bf 26 07 40 00          mov    $0x400726,%edi
  40063c:   e8 cf fe ff ff          callq  400510 <fopen@plt>
  400641:   48 89 45 f8             mov    %rax,-0x8(%rbp)
  400645:   eb 28                   jmp    40066f <main+0x7d>
  400647:   48 8d 85 f0 ef ff ff    lea    -0x1010(%rbp),%rax
  40064e:   48 89 c7                mov    %rax,%rdi
  400651:   e8 6a fe ff ff          callq  4004c0 <puts@plt>
  400656:   48 8d 85 f0 ef ff ff    lea    -0x1010(%rbp),%rax
  40065d:   ba 00 10 00 00          mov    $0x1000,%edx
  400662:   be 00 00 00 00          mov    $0x0,%esi
  400667:   48 89 c7                mov    %rax,%rdi
  40066a:   e8 71 fe ff ff          callq  4004e0 <memset@plt>
  40066f:   48 8b 55 f8             mov    -0x8(%rbp),%rdx
  400673:   48 8d 85 f0 ef ff ff    lea    -0x1010(%rbp),%rax
  40067a:   48 89 d1                mov    %rdx,%rcx
  40067d:   ba ff 0f 00 00          mov    $0xfff,%edx
  400682:   be 01 00 00 00          mov    $0x1,%esi
  400687:   48 89 c7                mov    %rax,%rdi
  40068a:   e8 41 fe ff ff          callq  4004d0 <fread@plt>
  40068f:   48 3d fe 0f 00 00       cmp    $0xffe,%rax
  400695:   76 b0                   jbe    400647 <main+0x55>
  400697:   b8 00 00 00 00          mov    $0x0,%eax
  40069c:   c9                      leaveq
  40069d:   c3                      retq
  40069e:   66 90                   xchg   %ax,%ax

Contents of section .rodata:
  400720 01000200 72002f64 65762f72 616e646f  ....r./dev/rando
  400730 6d00                                 m.

0000000000400510 <fopen@plt>:
  400510:   ff 25 2a 0b 20 00       jmpq   *0x200b2a(%rip)        # 601040 <fopen@GLIBC_2.2.5>
  400516:   68 05 00 00 00          pushq  $0x5
  40051b:   e9 90 ff ff ff          jmpq   4004b0 <.plt>

00000000004004c0 <puts@plt>:
  4004c0:   ff 25 52 0b 20 00       jmpq   *0x200b52(%rip)        # 601018 <puts@GLIBC_2.2.5>
  4004c6:   68 00 00 00 00          pushq  $0x0
  4004cb:   e9 e0 ff ff ff          jmpq   4004b0 <.plt>

00000000004004e0 <memset@plt>:
  4004e0:   ff 25 42 0b 20 00       jmpq   *0x200b42(%rip)        # 601028 <memset@GLIBC_2.2.5>
  4004e6:   68 02 00 00 00          pushq  $0x2
  4004eb:   e9 c0 ff ff ff          jmpq   4004b0 <.plt>

00000000004004d0 <fread@plt>:
  4004d0:   ff 25 4a 0b 20 00       jmpq   *0x200b4a(%rip)        # 601020 <fread@GLIBC_2.2.5>
  4004d6:   68 01 00 00 00          pushq  $0x1
  4004db:   e9 d0 ff ff ff          jmpq   4004b0 <.plt>
```
**���ָ��ѧϰ**
> mov    $0x0,%eax
> mov    $0x1fe,%ecx
> mov    %rdx,%rdi
> rep stos %rax,%es:(%rdi)
> repָ���Ŀ�����ظ��������ָ��ECX��ֵ���ظ��Ĵ����� 
> STOSָ��������ǽ�eax�е�ֵ������ES:EDIָ��ĵ�ַ��
