# Chapter 1 Values, Types, and Operators
## Numbers
JavaScript uses a fixed number of bits, namely 64 of them to store a single number value. How to write?

>13

>9.81

>2.998e8

The important thing is to be aware of it and treat fractional digital numbers as approximations, not as precise values.
## Special Numbers
**Infinity** represents the positive infinity and **Infinity-1** is still **Infinity**

**-Infinity** represents the negative infinity.

**NaN** stands for "not a number", if you try to calculate

**0/0** (zero divided by zero), **Infinity - Infinity**, or any number of other numeric operations that don’t yield a precise, meaningful result, you will get this.

## Strings
Strings are used to represent text. They are written by enclosing their content in quotes.

>"Patch my boat with chewing gum"

>'Monkeys wave goodbye'

Both single and double quotes can be used to mark strings as long as the start and the end match.

*Newlines* (the characters you get when you press Enter) can not be put between quotes. The string has to stay on a single line.

But you can do this:

>"This is the first line\nAnd this is the second"

The actual text goes like this:

>This is the first line

>And this is the second

There are, of course, situations where you want a backslash in a string to be just a backslash, not a special code. If two backslashes follow each other, they will collapse together, and only one will be left in the resulting string value. This is how the string “A newline character is written like "\n".” can be expressed:

>"A newline character is written like \"\\\n\"."

Strings cannot be divided, multiplied, or subtracted, but the + operator can be used on them.

string "concatenate":

>"con" + "cat" + "e" + "nate"

## Unary Operators

>console.log(typeof 4.5)

>// → number

>console.log(typeof "x")

>// → string

The other operators we saw all operated on two values, but typeof takes only one. Operators that use two values are called binary operators, while those that take one are called unary operators. The minus operator can be used both as a binary operator and as a unary operator.

>console.log(- (10 - 2))

>// → -8
