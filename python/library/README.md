# Library

* 程序
  * alabaster：项目文档编写
  * attrs：帮助开发者简化并加强类的创建
  * backcall：处理回调函数的参数问题
  * cffi：编写 C 语言扩展
  * click：编写命令行界面（CLI）工具
  * colorama：为终端文本添加颜色
  * decorator：创建装饰器
* 测试
  * absl-py：log，测试等封装
  * coverage：用于测量代码覆盖率
  * debugpy：调试远程 Python 应用程序
* 静态代码分析
  * astroid：抽象语法树（AST）解析、静态分析和推理
  * asttokens：为抽象语法树（AST）添加源代码的位置信息
  * astunparse：解析和操作抽象语法树（AST）
* 爬虫
  * beautifulsoup4：解析HTML和XML文档
  * defusedxml：安全地处理 XML 数据
  * bleach：清理 HTML 文本，并防止跨站脚本攻击（XSS）
  * certifi：当你使用 `requests` 或 `urllib3` 进行 HTTPS 请求时，`certifi` 中的证书会被自动使用。
* 网络
  * ca-certificates：处理和验证 SSL/TLS 证书
  * cyrus-sasl：实现 SASL（简单认证和安全性层）协议
* 系统
  * atomicwrites：原子性读写文件
  * binaryornot：检查文件是否为二进制文件
  * cachetools：高级缓存工具
  * comm：处理 Unix 风格的文本文件比较和合并
* 自动化
  * applaunchservices：macos 的自动化
  * appnope：禁用 macos 的系统休眠
  * cookiecutter：用于从模板创建项目
* 线程
  * anyio：异步与并发
  * async-lru：专为 `asyncio` 设计的轻量级 LRU（Least Recently Used）缓存实现
* 算法
  * ahrs：姿态和航向参考系统
  * astropy：天文学和天体物理学
  * astropy-iers-data：国际地球自转和参考系统服务（IERS）的地球旋转和闰秒表，支持astropy
  * biopython：用于生物信息学领域的计算
  * contourpy：生成高质量的等高线图
* AI
  * d2l：用于教育目的，帮助学生和初学者学习数据科学（李沐动手学 AI 用的这个）
  * depthai：用于与 NVIDIA Jetson TX2、TX1、Xavier 和 Nano 开发板上的深度学习加速器（例如 Jetson TX2 上的 NVIDIA TX2）进行交互
  * depthai-pipeline-graph：用于构建和运行深度学习加速器（如 NVIDIA Jetson TX2 上的 NVIDIA TX2）的深度学习流水线
* 绘图
  * cycler：用于在 Matplotlib 图形库中循环使用不同的样式、标记和颜色
* 编码
  * chardet：检测字节序列的字符编码
  * charset-normalizer：解决 `chardet` 在某些边缘情况下的不准确性问题
* 密码
  * argon2-cffi：哈希算法
  * argon2-cffi-bindings：argon2-cffi的低级绑定工具
  * cryptography：用于加密和解密数据
* 压缩
  * brotli-python：Brotli 压缩算法
  * brotlipy：Brotli 压缩算法
  * bzip2：Burrows-Wheeler 变换（BWT）和 Huffman 编码来实现高效的压缩
* 时间
  * arrow：对 datatime 的补充
* 科学计算
  * blas：是一个底层库，提供基本的线性代数运算。（numpy 会调用它）
  * blobconverter：将图像转换为Blob格式（pytorch 会调用它）
* 其他
  * autopep8：代码格式化
  * black：代码格式化工具
  * babel：国际化与本地化
  * boto3：AWS（Amazon Web Services）提供的 Python SDK，用于与 AWS 服务进行交互
  * botocore：AWS（Amazon Web Services）提供的一个 Python SDK，用于构建 AWS 服务客户端
  * cloudpickle：专门为 AWS Lambda 函数、Docker 容器和其他远程执行环境设计
