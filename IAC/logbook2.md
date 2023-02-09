# Parser

### Task 1

In task 1, I was trying to convert expressions that is separated by a lexer and recognized as tokens into a series of Operators/Functions to reconstruct the logic of the expression. For example: if we have input `7+8`, the parser should give the output of `const Expression *expr = new AddOperator(new Number(7),new Number(8));` As what we did in the lecture, I added several expressions to construct a good parser that include all add substruct multiplication and divide. Different from the code in the lecture, I changed negative values into a separate stem called `Unary`. 


Debugging step and careless error:
1. For string type tokens like `variable`, we are supposed to access the data inside the memory location instead of the pointer itself, so a `*` is needed whenever it is a pointer.

2. `FUNCTION_NAME` is used inside the parser to differentiate three of the functions so that in `FACTOR` stage, only 1 expression is written. `FUNCTION_NAME T_LBRACKET EXPR T_RBRACKET`. 
> Not sure why we cannot ignore `FUNCTION_NAME` and write up three functions rules inside `FACTOR` stage.

3. When debugging with the testing stage, I found invalid token errors for this input: `exp(z) * sqrt( log(1.0/x) )`. This is due to a careless mistake in the lexer stage, where the file does not include lexer to recognize `/` as `T_divide`. After adding it and remake the print_canonical(used to validate the output in the test.sh by printing into canonical form) using the command `make bin/print_canonical`, it works. 
> Remaking the files is because `print_canonical` incorporate lexer as a dependency.

### Task 2
In this task, I was trying to include evaluation by subsituting x with a specific value. For example:
```
$ make bin/eval_expr
$ bin/eval_expr x 7
x+6
13.000000
$
```

What I changed is in the header file, where we defined all Operators and Functions. Basically changing the `virtual evaluate()` function to override evluate function each time an operator or a function is called.

For minus:
```c
virtual double evaluate(
        const std::map<std::string,double> &bindings
    ) const override 
    {
        double vl=getLeft()->evaluate(bindings);
        double vr=getRight()->evaluate(bindings);
        return vl-vr;
    }
```

Similar evaluate function is added to other operators. Remember to include <cmath> libaray to use pow(), log(), sqrt(), and exp().


