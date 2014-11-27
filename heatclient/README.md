# heatclient

主要的客户端模块代码在这里实现。

heatclient 模块主要把通过 Heat 输入的命令转化为对 heat-engine 的 RESTAPI 调用，起到一个翻
译的作用，因此代码架构十分简单。

命令执行的入口在 shell.py 文件。
