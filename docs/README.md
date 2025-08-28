### Data Type 	### Details
Boolean 	    Single bit, enough for True/False flags (also was called yes/no)
Integers 	    Unsigned integers made up of bit arrays
Floats 	        Floating point numbers encoded in bit arrays
Complex 	    Complex numbers built from float arrays
Arrays 	        Index able arrays of above primitives types
Records 	    Group multiple arrays as records
Strings 	    Abbreviation for char arrays representing text

### Program Structure
In Plankalkul, a program is composed of one or several blocks, called plans. 
Modern analogue would be functions.

### Variables
Language can only assign particular names to variables.
V0, R0 and Z0 depending on their usage.

The **V** variables are used only for input values, and are readonly.
The **Z** variables are for intermediary storage within a plan.
The **R** variables store the results of each plan.

Every plan is preceded by a ’Randauszug’, which defines the number
of parameters and results as well as their corresponding type.
```
R(V0, V1) => (R0, R1)
```
Code takes two input value and returns it.
To use the result of plan 1.2 as a parametr for plan 1, 
this can be made: 
```
R0>1.2(V0)=> R0
```
In original there was **Ro1.2**

This Randauszug ensures that the result of R0 of plan 1.2 is used
as a parametr for this plan, which returns a single variable.

### Strange aspects
+ The index of an array is not written after the variable name, 
but immediatly below the variable name
+ The type of a variable must also be written below that, and given explicitly.
+ Variables don't have to be declared

**Original way of variables**
|    |  Z   | Z  |
| :- | :--: | -: |
| V  |  4   | 2  |
| K  |  2.3 |    |
| S  |  0   | 0  |

V here is a part of the variable name. So, here we have got Z4 and Z2.
K is a variable index. Calls Z4[2.3] and Z2[].
S is the type of a variable. In this case a signle bit. 

## Indexing a variable from another
|    |  Z   | Z  |
| :- | :--: | -: |
| V  |  1   ||2  |
| K  |  --- ||   |
| S  |  0   | 4.0|
The value of the variable Z2 is used as the index for the variable Z1, thus we get Z1[Z2]

In Plankalkul 2000 another notation was choosen. And so, the compiler uses it.
V0[1:5.0]       V0 is a component 1, of type 5.0
Z1[5.3 :9.0]    Z1 is a component 3 of component 5, of type 9.0
Z2[:12.3.0]     Z2 is of type 12.3.0

Example of the declared values:
```
V0[2]
Z1[6.4]
Z2
```

### Datatypes
The only primitive datatype in the language is a bit. 
You can construct more advanced datatypes from it.

An array of bits is constructed as:
```
n x 0
```
An array of arrays of bits this way:
```
m x n x 0
```

Tuples are created in such way.
> (0, 0) is a tuple of two bits.
> (0, 0, 0) is a tuple of three bits.

This tuples can be applied to any existent datatype. 
For example for datatypes д and є, we would write:
```
(д,Є)
```
and an array like:
```
m x д
```
A tupple can be written:
```
(д, m x Є)
```
and so on.

> Finish later this section

### Operators
**Basic assigning**
```
10=>Z0
```
Here value 10 had been assigned to the variable Z0.

**Conditional executing / if**
```
Z0=>Statement
```

If Z0 evaluates as true the Statement is executed, otherwise it is ignored.

**if else**
```
Z0=>Statement1
|Z0=>Statement2
```
>                          _
>Originally was written as Z0

The |Z0 is true if Z0 is not. And so, it equals to if-else:
```
  if (k < 5) {
    // do something
  } else if (k => 5) {
    // do something
  }
```

**Loops**
The first and the most general loop is called 'W'. 
```
W[
  Z0=>Statement1
  Z0=>Statement2
]
```
There are six looping constructs, W0..W5 which have
variants on the same operation.

They are given one (in the case of W0 to W3) or two 
(in the case of W4 and W5) integer variables which are constant.

Every loop emloyes a local variable for checking against the constant value.
```
W0(V0)[Statement1]
```
The W0 operator simply executes all statements in the following block for a number of times, 
speciﬁed in the variable V0.
Also, when the initial value is zero, the loop will not run.

The W1 and W2 operators are used to loop through the components of an array.
```
W1(n)[
  V0[i] => R0[i]
]
```
In the snippet above first variable from V0 is coppied to R0,
amount of times to loop is from 0 - n. So, until loop reaches n's value.

In W2 they count from n - 0. All the difference.

-------

Constructs W3 and W4 take two integers (k,l) at the start.
And then count while (W3) k=>l, and (W4) while k<=l.

W5 counts up or down while k=l, depending on whether k<l or k>l.

### Syntax
Variables x0, x1, x2
Boolean Expressions b0, b1, b2
Arithmatic Expressions a0, a1, a2
List Expressions l0, l1, l2
Statements S0, S1, S2
Numerical Expressions n0, n1, n2


