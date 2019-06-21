# Intermediate Representation
## Linear IRS
**Review Questions**
1. Consider the expression **_a\*2 + a\*2\*b_**. Translate it into stack machine code and into three address code. Compare and constrast the number of operations and the number of operands in each form. How do they coimpare against the trees in Figure 5.1?
**Answer:**

Stack Machine

```
PUSH a
PUSH 2
MULTIPLY 
PUSH a
PUSH 2
MULTIPLY
PUSH b
MULTIPLY
ADD
```

Three Address Code

```
t1 = a
t2 = 2
t3 = t1 * t2   // a*2
t4 = b
t5 = t3 * t5   // a*2*b
t6 = t3 + t5   // a*2 + a*2*b

```

## Mapping Values to Names
**Review Questions**
1. Consider the function fib shown in the margin. Write down the ILOC that a compiler’s front end might generate for this code under a register-to-register model and under a memory-to-memory model. How do the two compare? Under what circumstances might each memory be desirable.

```C
int fib(int n) {
  int x = 1;
  int y = 1;
  int z = 1;
  while(n > 1)
    z = x + y;
    x = y;
    y = z;
    n = n - 1;
  return z;
}
```
**Answer:**

register-to-register:

```C
main:
    loadI 1   to r1    # x = 1;
    loadI 1   to r2    # y = 1;
    loadI 1   to r3    # z = 1;
    loadI 100 to r4    # n = 100;
loop:
    add r1, r2 to r3   # z = x + y;
    i2i r2     to r1   # x = y;
    i2i r3     to r2   # y = z;
    sub r4, 1  to r2   # n = n - 1;
    cbr r4     to loop, next
next:
    ...
```

memory-to-memory:
_Assume int type has 4 bytes and  it is  8-bit machine._

```C
init:    
    loadI   1      to r2     
    store   r2     to r1     # x = 1
    storeAI r2     to r1, 4  # y = 1
    storeAI r2     to r1, 8  # z = 1
    loadI   100    to r2
    storeAI r2     to r1, 12 # n = 100
loop:
    load    r1     to r2     # read x
    load    r1, 4  to r3     # read y
    add     r2, r3 to r4     # z = x + y;
    storeAI r4     to r1, 12 # store z
    sotre   r3     to r1     # store x
    storeAI r4     to r1, 4  # store y
    load    r1, 12 to r2     # read n
    sub     r2, 1  to r2     # n = n - 1
    storeAI r2     to r1, 12 # store n
    cbr     r2     to loop, next
next:
    ...
    
```

memory-to-memory has more IO operations and uses less registers.
If we have enough registers and small amount of data we should use R2R.