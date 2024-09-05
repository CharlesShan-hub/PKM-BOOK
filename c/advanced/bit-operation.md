---
description: 位操作
icon: square-b
---

# Bit Operation

## 位运算符

<details>

<summary>按位与，或，非，异或</summary>

```c
#include <stdio.h>

void printBits(int num)
{
    // 获取整数的位数
    int bits = sizeof(num) * 8; // sizeof(num) 返回整数的大小（以字节为单位），乘以 8 得到位数

    // 遍历整数的每一位
    for (int i = bits - 1; i >= 0; i--)
    {
        // 检查当前位是否为 1
        if (num & (1 << i))
        {
            printf("1"); // 如果当前位是 1，则打印 1
        }
        else
        {
            printf("0"); // 如果当前位是 0，则打印 0
        }
    }
    printf("\n"); // 打印换行符，以便在不同的位之间分隔
}

int main()
{
    int a = 0b011;
    printBits(a); // 00000000000000000000000000000011
    // 按位取反：～
    printBits(~a); // 11111111111111111111111111111100
    // 按位与: &
    printBits(0b10001 & 0b10010); // 00000000000000000000000000010000
    // 按位或: |
    printBits(0b10001 | 0b10010); // 00000000000000000000000000010011
    // 按位异或: ^
    printBits(0b10001 ^ 0b10010); // 00000000000000000000000000000011
}

```

</details>

<details>

<summary>移位：左右</summary>



```c
#include <stdio.h>

void printBits(int num)
{
    // 获取整数的位数
    int bits = sizeof(num) * 8; // sizeof(num) 返回整数的大小（以字节为单位），乘以 8 得到位数

    // 遍历整数的每一位
    for (int i = bits - 1; i >= 0; i--)
    {
        // 检查当前位是否为 1
        if (num & (1 << i))
        {
            printf("1"); // 如果当前位是 1，则打印 1
        }
        else
        {
            printf("0"); // 如果当前位是 0，则打印 0
        }
    }
    printf("\n"); // 打印换行符，以便在不同的位之间分隔
}

int main()
{
    int positive = 3;
    int negtiave = -3;
    printBits(positive);
    printBits(positive << 1);
    printBits(positive << 2);
    printBits(positive << 3);
    printBits(positive >> 1);
    printBits(positive >> 2);
    printBits(positive >> 3);
    // 00000000000000000000000000000011
    // 00000000000000000000000000000110
    // 00000000000000000000000000001100
    // 00000000000000000000000000011000
    // 00000000000000000000000000000001
    // 00000000000000000000000000000000
    // 00000000000000000000000000000000

    printBits(negtiave);
    printBits(negtiave << 1);
    printBits(negtiave << 2);
    printBits(negtiave << 3);
    printBits(negtiave >> 1);
    printBits(negtiave >> 2);
    printBits(negtiave >> 3);
    // 11111111111111111111111111111101
    // 11111111111111111111111111111010
    // 11111111111111111111111111110100
    // 11111111111111111111111111101000
    // 11111111111111111111111111111110
    // 11111111111111111111111111111111
    // 11111111111111111111111111111111
}
```

</details>

## 位字段



