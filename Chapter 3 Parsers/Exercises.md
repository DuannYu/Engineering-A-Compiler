# Parsers
## 3.3 Top-Down Parsing
**Review Questions**
1. To build an efficient top-down parser, the compiler writer must express the sourse language in a somewhat constrained form. Explain the restrictions on the source-language grammer that are required to make it amenable to efficient top-down parsing.
_Left Recursive can not be existed._
2. Name two potential advantages of a hand-coded recursive-descent parser over a generated, table-driven LL(1) parser, and two advantages of LL(1) parser over the recursive descent implementation.
a.  Less codes of main function
b. More efficient
c. Easier to generate automatically

## 3.4 Bottom-Up Parsing
**Review Questions**
2. Build the LR(1)  tables for the _SheepNoise_ grammer, given in Section 3.2.2 on Page 86.

||**Item**|**Goal**|**S**|b|eof|
|-|-|-|-|-|-|
|0|CC0 |- | CC1|CC2|-|
|1|CC1 | -| -| -| -|
|2|CC2 |- |CC3 | CC2|- |
|3|CC3 |- | -|- |- |

