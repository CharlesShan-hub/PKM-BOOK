---
icon: robot-astromech
description: 控制语句：循环，分支，跳转
---

# Control

## Loop

### while

```c
while (expression)
    statement
```

<details>

<summary>while + scanf，循环输入</summary>

<pre class="language-c"><code class="lang-c">// power.c -- raises numbers to integer powers
#include &#x3C;stdio.h>
double power(double n, int p); // ANSI prototype
int main(void)
{
    double x, xpow;
    int exp;
    
    printf("Enter a number and the positive integer power");
    printf(" to which\nthe number will be raised. Enter q");
    printf(" to quit.\n");
<strong>    while (scanf("%lf%d", &#x26;x, &#x26;exp) == 2)
</strong>    {
        xpow = power(x,exp);   // function call
        printf("%.3g to the power %d is %.5g\n", x, exp, xpow);
        printf("Enter next pair of numbers or q to quit.\n");
    }
    printf("Hope you enjoyed this power trip -- bye!\n");
    
    return 0;
}

double power(double n, int p)  // function definition
{
    double pow = 1;
    int i;
    
    for (i = 1; i &#x3C;= p; i++)
        pow *= n;
    
    return pow;                // return the value of pow
}

</code></pre>

```
(base) kimshan@MacBook-Pro output % ./"power"
Enter a number and the positive integer power to which
the number will be raised. Enter q to quit.
1 2
1 to the power 2 is 1
Enter next pair of numbers or q to quit.
1.1 2
1.1 to the power 2 is 1.21
Enter next pair of numbers or q to quit.
100 2    
100 to the power 2 is 10000
Enter next pair of numbers or q to quit.
100.1 2
100 to the power 2 is 10020
Enter next pair of numbers or q to quit.
100 11.1
100 to the power 11 is 1e+22
Enter next pair of numbers or q to quit.
q
Hope you enjoyed this power trip -- bye!
```

</details>

<details>

<summary>while + scanf，输入一个字符串</summary>

<pre class="language-c"><code class="lang-c">// cypher2.c -- alters input, preserving non-letters
#include &#x3C;stdio.h>
#include &#x3C;ctype.h>            // for isalpha()
int main(void)
{
    char ch;
    
<strong>    //while ((ch = getchar()) != '\n')
</strong><strong>    while ((ch = getchar()) != EOF)
</strong>    {
        if (isalpha(ch))      // if a letter,
            putchar(ch + 1);  // display next letter
        else                  // otherwise,
            putchar(ch);      // display as is
    }
    putchar(ch);              // display the newline
    
    return 0;
}

</code></pre>

```
(base) kimshan@MacBook-Pro output % ./"cypher2"
ABCDabcd
BCDEbcde
```

</details>

### do while

```c
do
    statement
while(expression);
```

### for

```c
for(init; condition; update)
    statement
```

等价于

```c
init
for(;condition;)
{
    statement
    update
}
```

可以省略init，condition，update，statement任意位置

另外可以用逗号插入多个内容在一个语句里：`for(int i=1,j=2; i+j<100; i++,j++)`

***

## Branch

### if, else

<details>

<summary>Demo</summary>

```c
// electric.c -- calculates electric bill 
#include <stdio.h>
#define RATE1   0.13230       // rate for first 360 kwh      
#define RATE2   0.15040       // rate for next 108 kwh  
#define RATE3   0.30025       // rate for next 252 kwh
#define RATE4   0.34025       // rate for over 720 kwh       
#define BREAK1  360.0         // first breakpoint for rates  
#define BREAK2  468.0         // second breakpoint for rates 
#define BREAK3  720.0         // third breakpoint for rates
#define BASE1   (RATE1 * BREAK1)
// cost for 360 kwh            
#define BASE2  (BASE1 + (RATE2 * (BREAK2 - BREAK1)))
// cost for 468 kwh
#define BASE3   (BASE1 + BASE2 + (RATE3 *(BREAK3 - BREAK2)))
//cost for 720 kwh
int main(void)
{
    double kwh;               // kilowatt-hours used         
    double bill;              // charges                     
    
    printf("Please enter the kwh used.\n");
    scanf("%lf", &kwh);       // %lf for type double         
    if (kwh <= BREAK1)
        bill = RATE1 * kwh;
    else if (kwh <= BREAK2)   // kwh between 360 and 468     
        bill = BASE1 + (RATE2 * (kwh - BREAK1));
    else if (kwh <= BREAK3)   // kwh betweent 468 and 720
        bill = BASE2 + (RATE3 * (kwh - BREAK2));
    else                      // kwh above 680               
        bill = BASE3 + (RATE4 * (kwh - BREAK3));
    printf("The charge for %.1f kwh is $%1.2f.\n", kwh, bill);
    
    return 0;
}

```

</details>

### ?:（条件运算符）



### break, continue



### switch



### goto



***

## Jump



