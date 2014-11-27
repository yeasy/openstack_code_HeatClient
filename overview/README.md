# 整体结构

源代码包 python-heatclient 主要分为 3 个目录和若干文件：
doc，heatclient 和 tools。
除了这 3 个目录外，还包括一些说明文档、安装需求说明文件和测试脚本等。

## doc
包括利用 sphinx 生成文档的相关配置和源码。

## heatclient

核心的代码实现都在这个目录下。
可以通过下面的命令来统计主要实现的核心代码量。
```sh
find heatclient -name "*.py" | xargs cat | wc -l
```
目前版本，约为 12.4 k 行。

## tools
一些相关的环境安装和命令补全的脚本。

此外，还包括包安装的一些配置文件和说明文件等，包括 setup.cfg、setup.py、requirements.txt、tox.ini（tox 是一套 Python 项目的测试工具）等。
