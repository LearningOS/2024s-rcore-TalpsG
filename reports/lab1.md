# 简答题
## 第一题

答：我的sbi是最新的版本，qemu8.2,三个程序的错误分别是
1. pagefault
2. 非法指令
3. 非法指令

## 第二题
### 2.1 
我猜问的应该是ch2的trap.S中的restore里的a0,a0代表的是内核栈的指针
### 2.2
三个csr寄存器被存放到栈中，实际上就是保护断点(or现场)，sstatus记录了特权等级开关中断相关信息，sscratch记录了用户栈，sepc记录了sret要返回的程序地址

### 2.3
x4 一般不会用到，x2是sp,正在使用所以不保存，由于sp是内核栈的指针，因此最后会被保存到sscratch当中。当下次进入trap后就会恢复
### 2.4
sscratch 保存了sp的值，sp恢复成原来的值。
### 2.5
sret 
### 2.6 
交换了sscratch和 sp的值，sp指向内核栈，sscratch保存了sp之前的值

### 2.7 
ecall


# chap3 练习 taskinfo
这个练习实现起来相对容易只需要实现以下几个点即可
1. 在进入下一个任务时，判断是否是第一次执行该任务，如果是需要记录下最开始被调度的时间。
2. 在syscall分派函数中增加对应task的syscall 次数
3. 在taskinfo函数中将taskmanager里的taskinfo数据写到taskinfo系统调用的参数指针中即可

