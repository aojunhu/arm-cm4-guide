# ARM GCC 汇编语法及连接脚本

# 1. ARM GCC 汇编语法


# 2. ARM GCC连接脚本

```
OUTPUT_FORMAT("elf32-littlearm", "elf32-bigarm")
OUTPUT_ARCH(arm)
ENTRY(reset_handler)

/* memory map */
MEMORY
{
    FLASH (rx) : ORIGIN = 0x08000000, LENGTH = 128K
    RAM (rwx) : ORIGIN = 0x20000000, LENGTH = 40K
}

/* The size of the stack used by application */
C_STACK_SIZE	= 512;
IRQ_STACK_SIZE	= 0;
FIQ_STACK_SIZE	= 0;
SVC_STACK_SIZE	= 0;
ABT_STACK_SIZE	= 0;
UND_STACK_SIZE	= 0;

SECTIONS
{
	.text :
	{
		KEEP(*(.isr_vector))
		*(.text)
		*(.text.*)
		*(.rodata)
		_sromdev = .;
		_eromdev = .;
		_sidata = .;
	} >FLASH
	
	.data : AT(_sidata)
	{
		_sdata = .;
		*(.data)
		*(.data*)
		_edata = .;
	} >RAM
	
	.bss :
	{
		_sbss = .;
		*(.bss)
		_ebss = .;
	} >RAM
	
	.stack :
	{
        __stack_start__ = .;
        . += IRQ_STACK_SIZE;
        . = ALIGN(4);
        __irq_stack_top__ = .;
        
        . += FIQ_STACK_SIZE;
        . = ALIGN(4);
        __fiq_stack_top__ = .;
        
        . += SVC_STACK_SIZE;
        . = ALIGN(4);
        __svc_stack_top__ = .;
        
        . += ABT_STACK_SIZE;
        . = ALIGN(4);
        __abt_stack_top__ = .;
        
        . += UND_STACK_SIZE;
        . = ALIGN(4);
        __und_stack_top__ = .;
        
        . += C_STACK_SIZE;
        . = ALIGN(4);
        __c_stack_top__ = .;
        __stack_end__ = .;
	} >RAM
}
```
+ **OUTPUT_FORMAT**
指定输出格式。
+ **OUTPUT_ARCH**
指定目标机器架构。
+ **ENTRY(reset_handler)**
function ENTRY在linker script中可以指定entry point，也就是程式执行时第一个执行的指令开始位置。这边设定reset_handler作为entry point。
+ **MEMORY**
command MEMORY可以用来设定记忆体区段的属性，起始位置以及长度。其syntax为：
```
MEMORY
{
	name [(attr)] : ORIGIN = origin, LENGTH = len
	...
}
```
+ **C_STACK_SIZE**
指定C程序堆栈大小。
+ **KEEP**
当有开启link-time garbage collection的时候，有时候我们希望某个区段不要被回收掉，这时候就可以使用KEEP，使用方式为将input section wildcard entry放入KEEP中。
+ **\>FLASH \>RAM** 
把output section置入该memory region