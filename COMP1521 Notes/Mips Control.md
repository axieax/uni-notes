# Mips Control

## goto (sometimes used in kernel and embedded programs, avoid for C programming)

```c
for (int i = 1; i <= 10; i++) printf("%d\n", i);
```

same as 

```c
	int i = 1;
loop:
	if (i > 10) goto end; // negate logic
	printf("%d", i);
	printf("\n");
  i++;
end:
	return 0;
```

MIPS:

```assembly
li $t0, 1 # i in $t0
loop:
	bgt $t0, 10, end # if i > 10, goto end
	# Print i
	move $a0, $t0
	li $v0, 1
	syscall
	# Print \n
	li $a0, '\n'
	li $v0, 11
	syscall
	addi $t0, $t0, 1
	j loop
end:
	li $v0, 0 # return 0
	jr $ra
```

## If else

```c
	int i = 0;
	int n = 0;
	if (i < 0 && n >= 42) n = n - i;
	else n = n + i;
	printf("%d", n);
```

```c
	int i = 1;
	int n = 0;
	if (i >= 0) goto main_else; // Negate logic
	if (n < 42) goto main_else; // 
	n = n - i;
	goto main_end;
main_else:
	n = n + i;
main_end:
	printf("%d", n);
```

```assembly
	li $t0, 1 # i in $t0
	li $t1, 0 # n in $t1
	bge $t0, 0, main_else # If i < 0, goto main_else
	blt $t1, 42, main_else # If n < 42, goto main_else
	sub $t1, $t1, $t0 # n = n - 1
	b main_end
main_else:
	add $t1, $t1, $t0 # n = n + 1
main_end:
	move $a0, $t1
  li $v0, 1
  syscall
```





















