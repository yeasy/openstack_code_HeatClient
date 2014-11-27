# tools

## heat.bash_completion
为 bash 提供 Heat 相关的命令补全。

## install_venv_common.py
提供一些环境安装的类，供 install_venv.py 调用。

## install_venv.py

调用 install_venv_common.py 中的类，用来安装 virtualenv 包，来实现虚拟 Python 开发环境。

## with_venv.sh
调用 tox，并让它在给定的虚拟环境中执行命令。
