---
layout: page
title: struct task_struct
description: ""
---
{% include JB/setup %}

{% highlight ruby %}
struct mm_struct
{
    /*list of VMA*/
    struct vm_area_struct *mmap;

    /*指向vma段红黑树的指针*/
    rb_root_t mm_rb;

    /*last find_vma result  存储上一次查询的操作的结果*/
    struct vm_area_struct *mmap_cache;

    /*进程页目录的起始地址*/
    pgd_t *pgd;

    /*how many users with user space*/
    atomic_t mm_users;

    /*how many reference to "struct mm_struct"*/
    atomic_t mm_count;

    /*Number of VMA*/
    int map_count;

    /*对mmap操作的互赤信号量*/
    struct rw_semaphore mmap_sem;

    /*Protects task page tables and mm->rss*/
    spinlock_t page_table_lock;

    /*list of all active mm's. These are globally together off init_mm.mmlist,and are protected by mmlist_lock*/
    struct list_head mmlist;

    unsigned long start_code,end_code;
    unsigned long start_data,end_data;
    unsigned long start_brk,brk;
    unsigned long start_stack;
    unsigned long arg_start,arg_end,env_start,env_end;
    unsigned long rss,total_vm,locked_vm;
    unsigned long def_flags;
    unsigned long cpu_vm_mask;
    unsigned long swap_address;

    unsigned dumpable:1;
    mm_context_t context;
};
{% endhighlight %}
