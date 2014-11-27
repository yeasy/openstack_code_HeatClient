OpenStack HeatClient 源码分析
============
[HeatClient](http://docs.openstack.org/developer/python-heatclient) 是 OpenStack Heat 引擎的客户端实现，包括一个客户端 heat 命令，和一套 Python 的 API（实现了 heatclient 模块）。

本书将剖析 HeatClient 的代码。

最新版本在线阅读：[GitBook](https://www.gitbook.io/book/yeasy/openstack_code_HeatClient)。

本书源码在 Github 上维护，欢迎参与： [https://github.com/yeasy/openstack_code_HeatClient](https://github.com/yeasy/openstack_code_HeatClient)。

感谢所有的 [贡献者](https://github.com/yeasy/openstack_code_HeatClient/graphs/contributors)。

## 更新历史:

* 0.2: 2014-11-27
	* 根据最新代码修正。
* 0.1: 2014-08-07
	* 完成代码基本结构。

## 参加步骤
* 在 GitHub 上 `fork` 到自己的仓库，如 `user/openstack_code_HeatClient`，然后 `clone` 到本地，并设置用户信息。
```
$ git clone git@github.com:user/openstack_code_HeatClient.git
$ cd openstack_code_HeatClient
$ git config user.name "User"
$ git config user.email user@email.com
```

* 修改代码后提交，并推送到自己的仓库。
```
$ #do some change on the content
$ git commit -am "Fix issue #1: change helo to hello"
$ git push
```

* 在 GitHub 网站上提交 pull request。
* 定期使用项目仓库内容更新自己仓库内容。
```
$ git remote add upstream https://github.com/yeasy/openstack_code_HeatClient
$ git fetch upstream
$ git checkout master
$ git rebase upstream/master
$ git push -f origin master
```
