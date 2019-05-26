# Scanners

## 2.2 Recognizing Words

**Review Questions**<br>
Construct an FA to accept each of the following languages:<br>

1. A six-character identifier consisting of an alphabetic character followed by zero to five alphanumeric characters.<br>

2. A string of one or more oairs, where each pair consists of an open parenthesis followed by a close parenthsis.<br>

3. A Pascal comment, which consists of an open brace, {, followed by zero or more characters drawn from an alphabet, $\Sigma$,  followed by a close brace, }.

## 2.3 Regular Expressions

**Review Questions**<br>

1. Recall the RE for six-character identifier, written using a finite closure.

 $$ ([A...Z]|[a...z])([A..Z]|[a..z]|[0...9])^5 $$

   rewrite it in terms of the three basic RE operations: Alternation, concatenation, and closure.
2. In PL/I, the programmer can insert a quotation mark into a string by writing two quotation marks in a row. Thus, the string

   _The quotation mark, ", should be tyoeset in italics_
   would be  weitten in a PL/I program as 
   _"The quotation mark, "", should be tyoeset in italics"_
   Design a _RE_ ad a _FA_ to recognize PL/I strings. Assume that strings begin and end with quotation marks and contain only symbols drawn from an alphabet, sesignated as $\Sigma$. Quotation marks are the only special case.

**Review Questions**<br>
1. Consider the RE _who|what|where_. Use Thompon’s construction to build an NFA from RE. Use the subset construction to build a DFA from the NFA. Minimize the DFA.
2. Minimize the following DFA:<br>


  ![DFA](DFA.jpg)


