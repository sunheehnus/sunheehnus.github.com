---
layout: page
title: struct task_struct
description: ""
---
{% include JB/setup %}

{% highlight ruby %}
struct task_struct {

    /*进程的运行时状态，-1代表不可运行，0代表可运行，0代表已停止。*/
    volatile long state;

    /*
    进程当前的状态标志，具体的如：
    0x00000002表示进程正在被创建；
    0x00000004表示进程正准备退出；
    0x00000040 表示此进程被fork出，但是并没有执行exec；
    0x00000400表示此进程由于其他进程发送相关信号而被杀死 。
    */
    unsigned int flags;

    /*此进程的运行优先级*/
    unsigned int rt_priority;

    /*这里出现了list_head结构体，详情请参考*/
    struct list_head tasks;

    /*该结构体记录了进程内存使用的相关情况*/
    struct mm_struct *mm;

    /*进程的一些状态参数*/
    int exit_state;
    int exit_code, exit_signal;

    /*进程号*/
    pid_t pid;

    /*进程组号*/
    pid_t tgid;

    /*进程的"亲生父亲"，不管其是否被"寄养"。*/
    struct task_struct *real_parent;

    /*进程现在的父进程，有可能是"继父"*/
    struct task_struct *parent;

    /*该进程孩子的链表，可以得到所有孩子的进程描述符，但是需使用list_for_each和list_entry。*/
    struct list_head children;

    /*该进程兄弟的链表，也就是其父亲的所有孩子的链表。用法与children相似。*/
    struct list_head sibling;

    /*主线程的进程描述符*/
    struct task_struct *group_leader;

    /*进程所有线程的链表。*/
    struct list_head thread_group;

    /*进程使用cpu时间的信息，utime是在用户态下执行的时间，stime是在内核态下执行的时间。*/
    cputime_t utime, stime;

    /*启动的时间，时间基准不一样。*/
    struct timespec start_time;
    struct timespec real_start_time;

    /*comm是保存该进程名字的字符数组，长度最长为15*/
    char comm[TASK_COMM_LEN];

    /*文件系统信息计数*/
    int link_count, total_link_count;

    /*该进程在特定CPU下的状态*/
    struct thread_struct thread;

    /*文件系统相关信息结构体*/
    struct fs_struct *fs;

    /*打开的文件相关信息结构体*/
    struct files_struct *files;

    /*信号相关信息的句柄*/
    struct signal_struct *signal;
    struct sighand_struct *sighand;

    /*松弛时间值，用来规定select()和poll()的超时时间，单位是纳秒nanoseconds*/
    unsigned long timer_slack_ns;
    unsigned long default_timer_slack_ns;
}
{% endhighlight %}
