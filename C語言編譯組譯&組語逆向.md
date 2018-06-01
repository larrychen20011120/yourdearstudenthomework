# C語言編譯&組譯

# 程式: hello.c

#include<stdio.h>
 
int main()
{

    printf("dlrow olleH\n");
    
}

# 預處理:

```
 gcc -E hello.c -o hello.i
```
``` 
 file hello.i
```
 ==> C source, ASCII text
 
# 編譯階段:產生組語:

gcc –S XXX.i  –o XXX.s

![組語](picture/87.png)

產生的組合語言(assembly)

預設是AT&T組合語言格式

	.file	"hello.c"
	.section	.rodata
.LC0:

	.string	"Hello CTFer"
	.text
	.globl	main
	.type	main, @function
main:

.LFB0:

	.cfi_startproc
	pushq	%rbp
	.cfi_def_cfa_offset 16
	.cfi_offset 6, -16
	movq	%rsp, %rbp
	.cfi_def_cfa_register 6
	movl	$.LC0, %edi
	call	puts
	movl	$0, %eax
	popq	%rbp
	.cfi_def_cfa 7, 8
	ret
	.cfi_endproc
.LFE0:

	.size	main, .-main
	.ident	"GCC: (Ubuntu 5.4.0-6ubuntu1~16.04.5) 5.4.0 20160609"
	.section	.note.GNU-stack,"",@progbits
  
 產生AT&T語法格式的組語(gcc預設使用的格式)

gcc -S -masm=att XXXXX.c -o XXXXX_att.s

產生Intel語法格式的組語(微軟預設使用的格式)

gcc -S -masm=intel XXXXX.c -o XXXXX_intel.s

要去掉一堆註解:請加上參數-fno-asynchronous-unwind-tables

gcc -S -masm=intel XXXXX.c -o XXXXX_intel_OK.s -fno-asynchronous-unwind-tables
