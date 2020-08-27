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
