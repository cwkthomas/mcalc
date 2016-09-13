# mcalc

mcalc is a command line tool for calculating mathematical expressions.

### Usage
To use mcalc, run mcalc.py using python3. The first command line argument
should be an expression that you want solved. For example, to solve the 
expression 1+1, run:

`$ python3 mcalc.py 1+1`

If your expression contains spaces you must put it in double quotes:

`$ python3 mcalc.py "3 * (2 + 1)"`

mcalc does not follow the order of operations fully, for example in the
expression `1 + 1 / 2` the addition will be performed before the division,
resulting in 1, not 1.5. You must use parentheses to give order to your expressions. 
For example: `1 + (1 / 2)` will calculate the division of 1 / 2 first.

##### Expressions that should work:
* 1
* 1 + 1
* 1 + 1 + 1
* 1 / ( 2 + 3 )
* (3 + 2 + 1)

##### Expressions that shouldn't work:
* *Nothing*
* 2 / 0


### *IMPORTANT NOTES*
This utility hasn't been tested. I don't even really know if it works! Maybe
you can test it for me.

There are **3 main functions**:
##### tokenize ( expr )
Tokenize takes a string (a mathematical expression) and breaks it into
individual elements called "tokens". It then returns a list of tokens. For 
example: 

`tokenize("(3 * 2) / (12 - (2 * 2))")`

should return:

`['(', '3', '*', '2', ')', '/', '(', '12', '-', '(', '2', '*', '2', ')', ')']`

##### evaluate ( left, right, operator )
Evaluate performs a mathematical *operation* (+, -, *, or /) on two numbers - the
one on the left hand side of the operator and the other on the right hand side.
For example:

`evaluate(24, 2, '/')`
    
should return the result of 24 / 2:

`12`

##### simplify ( expr )
Simplify takes a list of tokens representing an expression. It then does **one** 
thing to *simplify* the expression. It searches for things to simplify in this
order:

1. Unneeded pairs of parentheses `()` - delete when found.
2. Parentheses surrounding a single number `(12)` - delete parentheses when 
found.
3. A simple, two term expression that can be solved `12 + 1` - when found, 
delete expression and replace with the result, `13`.

Example:

`simplify( ['(', '1', '+', '(', '3', '-', '5', ')', ')'] )`

should return:

`['(', '1', '+', '(', '-2.0', ')', ')']`

simplifying this result:

`simplify( ['(', '1', '+', '(', '-2.0', ')', ')'] )`

should return:

`['(', '1', '+', '-2.0', ')']`

and so on...