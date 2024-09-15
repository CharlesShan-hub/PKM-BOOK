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

```c
if(condition)
    statement1
else
    statement2
```

等价于

```c
condition ? statement1 : statement2
```

<details>

<summary>注意， Rust 里边的 if else 是表达式，但是C 里边 if else 并不是表达式</summary>

```c
#include <stdio.h>

int main()
{
    int a = 100;
    int b = a == 100 ? a + 1 : a + 2;
    int c = (if (a == 100) a + 1 else a + 2); // wrong!
    return 0;
}
```

</details>

### break, continue

break和 continue 都是针对本轮循环

### switch

本质就是 if else

<details>

<summary>Demo</summary>

```c
/* animals.c -- uses a switch statement */
#include <stdio.h>
#include <ctype.h>
int main(void)
{
    char ch;
    
    printf("Give me a letter of the alphabet, and I will give ");
    printf("an animal name\nbeginning with that letter.\n");
    printf("Please type in a letter; type # to end my act.\n");
    while ((ch = getchar()) != '#')
    {
        if('\n' == ch)
            continue;
        if (islower(ch))     /* lowercase only          */
            switch (ch)
        {
            case 'a' :
                printf("argali, a wild sheep of Asia\n");
                break;
            case 'b' :
                printf("babirusa, a wild pig of Malay\n");
                break;
            case 'c' :
                printf("coati, racoonlike mammal\n");
                break;
            case 'd' :
                printf("desman, aquatic, molelike critter\n");
                break;
            case 'e' :
                printf("echidna, the spiny anteater\n");
                break;
            case 'f' :
                printf("fisher, brownish marten\n");
                break;
            default :
                printf("That's a stumper!\n");
        }                /* end of switch           */
        else
            printf("I recognize only lowercase letters.\n");
        while (getchar() != '\n')
            continue;      /* skip rest of input line */
        printf("Please type another letter or a #.\n");
    }                        /* while loop end          */
    printf("Bye!\n");
    
    return 0;
}

```

</details>

如果没有 break 就会进入下一个代码块，可以利用这个特性，制作多重标签

<details>

<summary>Demo</summary>

```c
// vowels.c -- uses multiple labels
#include <stdio.h>
int main(void)
{
    char ch;
    int a_ct, e_ct, i_ct, o_ct, u_ct;

    a_ct = e_ct = i_ct = o_ct = u_ct = 0;

    printf("Enter some text; enter # to quit.\n");
    while ((ch = getchar()) != '#')
    {
        switch (ch)
        {
        case 'a':
        case 'A':
            a_ct++;
            break;
        case 'e':
        case 'E':
            e_ct++;
            break;
        case 'i':
        case 'I':
            i_ct++;
            break;
        case 'o':
        case 'O':
            o_ct++;
            break;
        case 'u':
        case 'U':
            u_ct++;
            break;
        default:
            break;
        } // end of switch
    } // while loop end
    printf("number of vowels:   A    E    I    O    U\n");
    printf("                 %4d %4d %4d %4d %4d\n",
           a_ct, e_ct, i_ct, o_ct, u_ct);

    return 0;
}

// (base) kimshan@MacBook-Pro output % ./"vowels"
// Enter some text; enter # to quit.
// A
// a
// #
// number of vowels:   A    E    I    O    U
//                     2    0    0
```

</details>

***

## Jump

### goto

<details>

<summary>唯一的 goto 使用场景：跳出多重循环</summary>

<pre class="language-c"><code class="lang-c">#include &#x3C;stdio.h>

int main()
{

    for (int i = 0; i &#x3C; 3; ++i)
    {
        for (int j = 0; j &#x3C; 3; ++j)
        {
            for (int k = 0; k &#x3C; 3; ++k)
            {
                printf("i: %d, j: %d, k: %d\n", i, j, k);
                // 假设当 i == 1, j == 2, k == 2 时，我们需要跳出所有循环
                if (i == 1 &#x26;&#x26; j == 2 &#x26;&#x26; k == 2)
                {
<strong>                    goto end_of_loops;
</strong>                }
            }
        }
    }

<strong>end_of_loops:
</strong>    printf("跳出所有循环。\n");
<strong>test:
</strong>    printf("不调用也会 print\n");

    return 0;
}
// (base) kimshan@MacBook-Pro output % ./"a"
// i: 0, j: 0, k: 0
// i: 0, j: 0, k: 1
// i: 0, j: 0, k: 2
// i: 0, j: 1, k: 0
// i: 0, j: 1, k: 1
// i: 0, j: 1, k: 2
// i: 0, j: 2, k: 0
// i: 0, j: 2, k: 1
// i: 0, j: 2, k: 2
// i: 1, j: 0, k: 0
// i: 1, j: 0, k: 1
// i: 1, j: 0, k: 2
// i: 1, j: 1, k: 0
// i: 1, j: 1, k: 1
// i: 1, j: 1, k: 2
// i: 1, j: 2, k: 0
// i: 1, j: 2, k: 1
// i: 1, j: 2, k: 2
// 跳出所有循环。
// 不调用也会 print
</code></pre>

</details>
