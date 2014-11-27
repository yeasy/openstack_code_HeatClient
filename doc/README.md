# doc
可以利用 sphinx 工具来生成文档（官方的在线文档即为此方法生成）。

## Makefile
用户执行 make 命令时候读取的配置。例如在此目录下执行
```
make html
```
会生成 build 目录，下面有 html 格式的文档。生成过程需要 sphinx、oslosphinx 等 Python 包的支持。

## source 子目录

文档相关的代码。

其中 index.rst 文件为文档主页面文件。

conf.py 文件为 sphinx 工具的配置文件。
