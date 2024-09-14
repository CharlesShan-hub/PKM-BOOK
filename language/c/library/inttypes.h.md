---
description: https://pubs.opengroup.org/onlinepubs/009695399/basedefs/inttypes.h.html
icon: ring-diamond
---

# inttypes.h

* `inttypes.h` 头文件提供了格式化宏，用于与 `stdint.h` 中定义的整数类型一起使用。这些宏用于确保在不同的平台上，格式化字符串的行为是一致的。

1. **格式化宏**：例如 `PRIi8`, `PRIi16`, `PRIi32`, `PRIi64` 用于有符号整数，`PRIu8`, `PRIu16`, `PRIu32`, `PRIu64` 用于无符号整数。这些宏可以在 `printf` 和 `scanf` 类型的函数中使用，以确保正确地打印和读取指定宽度的整数。
2. **大数格式化宏**：例如 `PRId64`, `PRIo64`, `PRIu64`, `PRIx64`，用于格式化 `int64_t` 和 `uint64_t` 类型的值。
3. **扫描宏**：例如 `SCNi16`, `SCNu32`，这些宏用于 `scanf` 类型的函数，确保可以正确地读取指定宽度的整数。