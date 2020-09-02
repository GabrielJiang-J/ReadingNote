    hw�ڼ䣬�ڹ�˾����Ƚ��٣��Ͱ�֮ǰû��ϵͳ�о����Ķ����Ƹ�ʽ��linux c����Ĵ�Դ�뵽�������ļ���ת���Լ��������ļ���װ�غ�ִ�У��ٴ�ͷ��β��һ�飬�ѵײ��ԭ��Ū���������ǰ�����������е��������ɵ�֪ʶ��һ��һ����ֳ�����Ҳ�����Լ��Ļ�������ʵЩ��

### 1. cԴ�����
    �����Ը�������ࡢ�ܹ����鼮��ϴ��Ӧ�ÿ��ԡ���ơ����Ƚ�ţ�Ƶ�����ܹ��ˣ�Ȼ������Ÿ��ֱ༭������ide����ʼһ��д���롣
    ������������ݣ���Ҫ����c�Ļ�����c�ĸ߼�������linuxϵͳ��̡�linux�����̡����б�̡�IPC�������ں˱�̵ȵȣ������ı�̼�����ѧϰ�����в���ϵͳ������ԭ������ԭ���������ϵ�ṹ���㷨���ܹ���ơ��ع���ϵͳ���������ģʽ�ȵȼ�����ѧϰ��Ȼ�����ҹ�Լ�������ֹ��ߣ���룬�򸱱�������

### 2. cԴ���д
    Ȼ���ھ���������ҹ�İٶȡ�����֮�����ڰ���ţ�Ƶļܹ�ʵ���ˣ���Ȼ��д��ʲô����һ���±ƣ�������������쵼���õ�������֭��֭����

---
    ������꣬���ڰѴ���д���ˣ�Ȼ����Ǳ��롢ִ�С��������Ȼ�Ĳ����������������������׸���ɶ������ȫ��֪������ȫ��ɵ��һ�������ż�������Ҵ���á����ԣ�������뵽linux c����ı���׶Ρ�

### 3. gccԤ����cpp
### 4. gcc���룺cc1
### 5. gcc��ࣺas
#### elf�ļ���ʽ
    ���֮������relocatable file��relocatable file��c�������������е�һ����elf��ʽ���ڵ��ļ������滹��executable file��shared object file������elf��ʽ���ڣ�������elf�����У�������object file������������¼elf�ļ���ʽ��
    elf������ǰΪֹ����Ϊ�����֡�һ����32λ��׼���壬һ����64λ���䶨�塣
> [elf 32λ��׼����](https://github.com/GabrielJiang-J/study_information/blob/master/%E4%BA%8C%E8%BF%9B%E5%88%B6%E5%88%86%E6%9E%90/linux/elf.pdf)
> [elf 64λ���䶨��](https://github.com/GabrielJiang-J/study_information/blob/master/%E4%BA%8C%E8%BF%9B%E5%88%B6%E5%88%86%E6%9E%90/linux/elf-64-gen.pdf)

    ����Ŀǰ64λ�ѱȽ��ձ飬�����ڼ�¼ʱ��ֱ�Ӻϲ�32λ��64λ�����е�������ݽṹ���塣

---
    
   object file����뵽��������Ӻ�ִ�й����У����elf�ļ����ֳ�������ͼ��ִ����ͼ��������ͼ���������Ӻ�ִ�й����еĲ�ͬҪ�ء�
![Object File Format](D:\�ĵ�\������Դ\����ʼ�\ReadingNote\linux�����������\1.png) 
> **ELF header**������������elf�Ľṹ����֯��
> **Sections**���������С�������ͼ���������Ϣ��
> **Segments**���������С�ִ����ͼ���������Ϣ��
> **program header table**��������δ���process image��
> **section header table**����������section��ȫ����Ϣ��

![ELF-64 Data Types](D:\�ĵ�\������Դ\����ʼ�\ReadingNote\linux�����������\2.png)
    
![ELF-64 Header](D:\�ĵ�\������Դ\����ʼ�\ReadingNote\linux�����������\3.png)

![ELF Identification, e_ident](D:\�ĵ�\������Դ\����ʼ�\ReadingNote\linux�����������\4.png)

![Object File Classes, e_ident[EI_CLASS]](D:\�ĵ�\������Դ\����ʼ�\ReadingNote\linux�����������\5.png)

![Data Encodings, e_ident[EI_DATA]](D:\�ĵ�\������Դ\����ʼ�\ReadingNote\linux�����������\6.png)

![Operating System and ABI Identifiers, e_ident[EI_OSABI]](D:\�ĵ�\������Դ\����ʼ�\ReadingNote\linux�����������\7.png)

![Object File Types, e_type](D:\�ĵ�\������Դ\����ʼ�\ReadingNote\linux�����������\8.png)

![e_machine](D:\�ĵ�\������Դ\����ʼ�\ReadingNote\linux�����������\9.png)

ʵ����
```shell
[root@localhost tmp]# readelf -h /bin/ls
ELF Header:
  Magic:   7f 45 4c 46 02 01 01 00 00 00 00 00 00 00 00 00 
  Class:                             ELF64
  Data:                              2's complement, little endian
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  ABI Version:                       0
  Type:                              EXEC (Executable file)
  Machine:                           Advanced Micro Devices X86-64
  Version:                           0x1
  Entry point address:               0x404324
  Start of program headers:          64 (bytes into file)
  Start of section headers:          115688 (bytes into file)
  Flags:                             0x0
  Size of this header:               64 (bytes)
  Size of program headers:           56 (bytes)
  Number of program headers:         9
  Size of section headers:           64 (bytes)
  Number of section headers:         30
  Section header string table index: 29
```
```shell
[root@localhost tmp]# xxd -s 0x0 -l 0x40 /bin/ls
0000000: 7f45 4c46 0201 0100 0000 0000 0000 0000  .ELF............
0000010: 0200 3e00 0100 0000 2443 4000 0000 0000  ..>.....$C@.....
0000020: 4000 0000 0000 0000 e8c3 0100 0000 0000  @...............
0000030: 0000 0000 4000 3800 0900 4000 1e00 1d00  ....@.8...@.....
```

    
### 6. gcc���ӣ�collect2:ld//lib64/ld-linux-x86-64.so.2
#### ��̬����
ʵ�飺
`[root@localhost 3]# cat Program1.c`
```c
#include "Lib.h"

int main(void) {
   foobar(1); 
   return 0;
}
```

`[root@localhost 3]# cat Program2.c`
```c
#include "Lib.h"

int main(void) {
   foobar(2); 
   return 0;
}
```

`[root@localhost 3]# cat Lib.c`
```c
#include <stdio.h>

void foobar(int i) {
    printf("Printing from Lib.so %d\n", i);
}
```

`[root@localhost 3]# cat Lib.h`
```c
#ifndef LIB_H
#define LIB_H

void foobar(int i);

#endif
```

```shell
[root@localhost 3]# gcc -fPIC -shared -o Lib.so Lib.c 
[root@localhost 3]# gcc -o Program1 Program1.c ./Lib.so 
[root@localhost 3]# gcc -o Program2 Program2.c ./Lib.so
```

### 7. elfװ��

program headers
```c
int main(void) {
    int a = 0x12345678;

    return 0;
}
```
```
[root@localhost tmp]# readelf -l test

Elf file type is EXEC (Executable file)
Entry point 0x400400
There are 9 program headers, starting at offset 64

Program Headers:
  Type           Offset             VirtAddr           PhysAddr
                 FileSiz            MemSiz              Flags  Align
  PHDR           0x0000000000000040 0x0000000000400040 0x0000000000400040
                 0x00000000000001f8 0x00000000000001f8  R E    8
  INTERP         0x0000000000000238 0x0000000000400238 0x0000000000400238
                 0x000000000000001c 0x000000000000001c  R      1
      [Requesting program interpreter: /lib64/ld-linux-x86-64.so.2]
  LOAD           0x0000000000000000 0x0000000000400000 0x0000000000400000
                 0x000000000000069c 0x000000000000069c  R E    200000
  LOAD           0x0000000000000e18 0x0000000000600e18 0x0000000000600e18
                 0x0000000000000220 0x0000000000000228  RW     200000
  DYNAMIC        0x0000000000000e28 0x0000000000600e28 0x0000000000600e28
                 0x00000000000001d0 0x00000000000001d0  RW     8
  NOTE           0x0000000000000254 0x0000000000400254 0x0000000000400254
                 0x0000000000000044 0x0000000000000044  R      4
  GNU_EH_FRAME   0x0000000000000574 0x0000000000400574 0x0000000000400574
                 0x0000000000000034 0x0000000000000034  R      4
  GNU_STACK      0x0000000000000000 0x0000000000000000 0x0000000000000000
                 0x0000000000000000 0x0000000000000000  RW     10
  GNU_RELRO      0x0000000000000e18 0x0000000000600e18 0x0000000000600e18
                 0x00000000000001e8 0x00000000000001e8  R      1

 Section to Segment mapping:
  Segment Sections...
   00     
   01     .interp 
   02     .interp .note.ABI-tag .note.gnu.build-id .gnu.hash .dynsym .dynstr .gnu.version .gnu.version_r .rela.dyn .rela.plt .init .plt .text .fini .rodata .eh_frame_hdr .eh_frame 
   03     .init_array .fini_array .dynamic .got .got.plt .data .bss 
   04     .dynamic 
   05     .note.ABI-tag .note.gnu.build-id 
   06     .eh_frame_hdr 
   07     
   08     .init_array .fini_array .dynamic .got 
```
```
[root@localhost tmp]# xxd -s 0x40 -l 0x1f8 /tmp/test
0000040: 0600 0000 0500 0000 4000 0000 0000 0000  ........@.......
0000050: 4000 4000 0000 0000 4000 4000 0000 0000  @.@.....@.@.....
0000060: f801 0000 0000 0000 f801 0000 0000 0000  ................
0000070: 0800 0000 0000 0000 0300 0000 0400 0000  ................
0000080: 3802 0000 0000 0000 3802 4000 0000 0000  8.......8.@.....
0000090: 3802 4000 0000 0000 1c00 0000 0000 0000  8.@.............
00000a0: 1c00 0000 0000 0000 0100 0000 0000 0000  ................
00000b0: 0100 0000 0500 0000 0000 0000 0000 0000  ................
00000c0: 0000 4000 0000 0000 0000 4000 0000 0000  ..@.......@.....
00000d0: 9c06 0000 0000 0000 9c06 0000 0000 0000  ................
00000e0: 0000 2000 0000 0000 0100 0000 0600 0000  .. .............
00000f0: 180e 0000 0000 0000 180e 6000 0000 0000  ..........`.....
0000100: 180e 6000 0000 0000 2002 0000 0000 0000  ..`..... .......
0000110: 2802 0000 0000 0000 0000 2000 0000 0000  (......... .....
0000120: 0200 0000 0600 0000 280e 0000 0000 0000  ........(.......
0000130: 280e 6000 0000 0000 280e 6000 0000 0000  (.`.....(.`.....
0000140: d001 0000 0000 0000 d001 0000 0000 0000  ................
0000150: 0800 0000 0000 0000 0400 0000 0400 0000  ................
0000160: 5402 0000 0000 0000 5402 4000 0000 0000  T.......T.@.....
0000170: 5402 4000 0000 0000 4400 0000 0000 0000  T.@.....D.......
0000180: 4400 0000 0000 0000 0400 0000 0000 0000  D...............
0000190: 50e5 7464 0400 0000 7405 0000 0000 0000  P.td....t.......
00001a0: 7405 4000 0000 0000 7405 4000 0000 0000  t.@.....t.@.....
00001b0: 3400 0000 0000 0000 3400 0000 0000 0000  4.......4.......
00001c0: 0400 0000 0000 0000 51e5 7464 0600 0000  ........Q.td....
00001d0: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00001e0: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00001f0: 0000 0000 0000 0000 1000 0000 0000 0000  ................
0000200: 52e5 7464 0400 0000 180e 0000 0000 0000  R.td............
0000210: 180e 6000 0000 0000 180e 6000 0000 0000  ..`.......`.....
0000220: e801 0000 0000 0000 e801 0000 0000 0000  ................
0000230: 0100 0000 0000 0000                      ........
```
```
[root@localhost tmp]# xxd -s 0x40 -l 56 /tmp/test
0000040: 0600 0000 0500 0000 4000 0000 0000 0000  ........@.......
0000050: 4000 4000 0000 0000 4000 4000 0000 0000  @.@.....@.@.....
0000060: f801 0000 0000 0000 f801 0000 0000 0000  ................
0000070: 0800 0000 0000 0000                      ........
```
    > ELF�������ļ�load���ڴ沢ִ�У��ں�Դ�룺
    > https://github.com/GabrielJiang-J/study_information/blob/master/%E4%BA%8C%E8%BF%9B%E5%88%B6%E5%88%86%E6%9E%90/linux/elf-64-gen.pdf
    > linux-2.6.34/fs/binfmt_elf.c:elf_format.load_binary
    > linux-2.6.34/arch/ia64/kernel/process.c:sys_execve
### 8. elfִ��
