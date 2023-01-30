# Lab 1 Regexes
#### Steven Shao 30/01/2021


What I change in `.flex` file is the following:

```
...

%%
[[][^]]*]               {  fprintf(stderr, "Word : %s\n", yytext); 
                           char *a = yytext; a++; a[strlen(a)-1]= '\0'; 
                           yylval.wordValue = new std::string(a); return Word; }

-?([0-9]+[.])?[0-9]+    {  fprintf(stderr, "Number : %s\n", yytext); 
                           yylval.numberValue = strtod(yytext, NULL);  return Number; }

-?([0-9]+[/])[0-9]+     {  fprintf(stderr, "Fraction : %s\n", yytext); 
                           int num, denom;
                           sscanf(yytext, "%d/%d", &num, &denom);
                           double result = (double) num / (double) denom;
                           yylval.numberValue = result;  return Number; }


[a-zA-Z]+               {  fprintf(stderr, "Word : %s\n", yytext); 
                           yylval.wordValue = new std::string(yytext); return Word; }

[\n]                    {  fprintf(stderr, "Newline\n"); }

.                       {}
%%

...
```
This is the rule section which is in between two %%. The rules are following top-down orders, so the regrexes are trying to fit into the first rule, and then the second until the last rule.

`[[][^]]*]` represents anything inside a square brackets except for `[]]` , because this example should be recognized as separate words `[]` and `]`.

__Examples:__ [abc], [1.5], [], [ ]

Because this is already in square brackets, but in the `cpp` file, I place another square bracket before printing for other Word Type expressions, so I have to remove the one pair of square bracket here. I create a pointer `a` to `yytext`, and remove the first and last character by some operations to the new pointer.

`-?([0-9]+[.])?[0-9]+` represents any decimal numbers including negative numbers and integer. 
* `-?` = there might be a `-` sign.
* `([0-9]+[.])?` = one or more numbers in front of decimal point. The whole thing can have 1 or 0 time.
* `[0-9]+` = one or more numbers after the decimal point.

__Examples:__  0.12, 1.1, 1, 1.0, -12, 21

__Exclude:__   .1, .555. These would be recognized as 1, 555

In the program part, I use strtod() to convert a string representation of a floating-point number to a double-precision floating-point number.

`-?([0-9]+[/])[0-9]+` represents a fractional number in the form `a/b`. But this time, the `?` is removed, because only when `/` is present can be recognized by this rule.

__Examples:__ 1/2, 3/5, 7/8

__Exclude:__ 1.0/2.0    This will be recognized as 1.0, [/], 2.0 separatly.

In the program part, I use sscanf(yytext, "%d/%d", &num, &denom) to store two integers before and after `/` in `num` and `denom`.

`[a-zA-Z]+` represents any orders of uppercase and lowercase combinations.

`\n` represents a new line.

`.` means everything else except the first five rules, do nothing.





