# Code Shape
## 7.2 Assigning Storage Locations
**Review Questions**
2. Consider the short fragment in the margin. It mentions three values: _a, b,_ and _*b_. Which are ambiguous? Which are unambiguous?
**Answer:**

||ambiguous|unambigious|
|-|-|-|
|**Values** |_a,b_|_*b_ |

## 7.5 Storing and Accessing Arrays
**Review Questions**
1. For a two-dimensional array _A_ stored in column-major order, write down the address polynomail for the reference _A[i, j]_. Assume that _A_ is declared with dimensions _(l1:h1)_ and _(l2:h2)_ and that elements of _A_ occupy _w_ bytes.
**Answer:**

```
@A + (j - i1)*len2*w + (i - i2)*w
```

2. Given an array of integers with dimensions _A[0:99, 0:89, 0:109]_, how many words of memory are used to represent _A_ as a compact row-major order array? How many words are needed to represent _A_ using indirection vectors? Assume that both pointers and integers require one word each.
**Answer:**


||Compact row-major order array|Indirection vectors|
|-:|-|-|
|**Memory** |100 x 90 x 110| 100 x 90 x 110 + 100 + 90 + 110|

## 7.6 Character Strings
1. Write the ILOC code for the string assignment _a = b_ using word-length loads and stores. (Use character-length loads and stores in a post loop to clean up the end cases.) Assume that _a_ and _b_ are word aligned and non-over-lapping.

**Answer:**

```C

  loadI  @b      to r@b
  loadAI r@b, -4 to r1        // get b's length
  loadI  @a      to r@a
  loadAI r@a, -4 to r2        // get a's length
  com_LT r2, r1  to r3        // will b fit in a?
  cbr    r3      to Lsov, L1
L1:
  loadI 0       to r4         // counter
  com_LT r4, r1 to r5         // more to copy
  cbr r5        to L2, L3
L2:
  loadA0  r@b, r4 to r6       // get char from b (1/4)
  storeA0 r6      to r@a, r4  // put it in a
  addI    r4, 1   to r4       // increment offset

  loadA0  r@b, r4 to r6       // get char from b (2/4)
  storeA0 r6      to r@a, r4  // put it in a
  addI    r4, 1   to r4       // increment offset

  loadA0  r@b, r4 to r6       // get char from b (3/4)
  storeA0 r6      to r@a, r4  // put it in a
  addI    r4, 1   to r4       // increment offset

  loadA0  r@b, r4 to r6       // get char from b (4/4)
  storeA0 r6      to r@a, r4  // put it in a
  addI    r4, 1   to r4       // increment offset
  
  /* Finish a whole word
  * The code block can be written to a new procedure and easy to read
  */
  

  cmp_LT r4, r1 to r7         // more to copy?
  cbr r7        to L2, L3
L3:
  storeAI r1    to r@a, -4    // set length
```
