# x265 源码分析
## 项目简介
HEVC的参考软件有许多，在学术界常用的是HM，而在工业界常用的是`x265`。该项目对`x265` 3.0版本的源码实现进行分析，在源代码文件中用中文进行注释，并在readme中进行相应说明。

## 源码文件

### x265.cpp

`main`函数位于`x265.cpp`文件中，在`main`函数中编码工作主要和`encoder_encode`函数有关，`encoder_encode`是位于`api`结构体里的函数指针。`api`是`x265_api`类型的结构体指针，`api`位于类`CLIOptions`里，通过不同的`profile`设定不同的输出比特深度，再根据不同的比特深度给`api`设定不同的`libx264`。`CLIOptions`定义于`x265.cpp`文件里，主要做处理命令行参数的工作。

这个文件里几个主要的函数是

* `cliopt.parse()` 解析参数
* `api->encoder_open()` 打开编码器配置
* `api->encoder_headers()` 设置NAL相关信息
* `api->encoder_encode()` 编码
* `api->encoder_close()`  结束关闭编码器

> 在`x265.cpp`里有一个命名为`pts_queue`的优先队列，里面存放了`pts`的负值，暂时不太明白作用

