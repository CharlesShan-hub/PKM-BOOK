---
description: 简略的过一下yaml语法
---

# Yaml Syntax

## Syntax

**键值对**：并不像 json 需要括号，yaml 想 python 一样，仅用缩进就可以了，所以说 yaml 是一种适合人类阅读的标记语言

```yaml
app: user-authentication
port: 9000
version: 1.7
```

字符串我们可以用单引号，双括号或者不加引号。但是如果有转义符号，还是要加引号

```yaml
str1: "string"
str2: 'string'
str3: string
str4: "Hello World\n"
```

注释：yaml 也是支持注释的，json 不支持

```yaml
#  
```



## Reference

\[1] [Yaml Tutorial | Learn YAML in 18 mins](https://www.youtube.com/watch?v=1uFVr15xDGg)
