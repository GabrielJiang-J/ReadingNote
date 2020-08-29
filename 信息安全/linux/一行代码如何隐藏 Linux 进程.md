### �������ýű�
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

### Ҫ���صĽ���Դ��
�ļ�����test.c

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

### �ű�ʹ�÷���
```
��һ���նˣ�
gcc test.c -o test
./test

�ڶ����նˣ�
chmod 755 hide.stp
./hide.stp `pidof test`
```

### ��֤����
    1. /procĿ¼�¿��������ؽ��̵�Ŀ¼
    2. ps�����޷��������ؽ���
    3. pidof�����޷��������ؽ���
    4. top�����޷��������ؽ���
    5. htop�����޷��������ؽ���
    6. pstree�����޷��������ؽ���
    7. ���������޷��������ؽ�����Ϣ
```shell
    for pid in $(ls /proc|awk '/^[0-9]+/{print $1}'); do 
        ls -l /proc/$pid/exe; 
    done
```

### ����һ����ؽ��̣�
