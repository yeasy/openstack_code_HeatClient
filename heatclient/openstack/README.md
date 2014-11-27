## openstack

### common

#### apiclient

##### auth.py
跟认证插件相关的方法，包括 discover_auth_systems、load_auth_system_opts、load_plugin、load_plugin_from_args 等。

另外实现了 BaseAuthPlugin 类，作为实现各种认证插件的基础元类。

##### base.py
定义了若干基础类，包括
* Resource 代表 OpenStack 中的资源类型（项目、用户等）
* BaseManager 代表进行资源操作的基础类
* ManagerWithFind（继承自 BaseManger） 代表对资源进行操作的类
* BaseAuthPlugin（继承自 BaseManger） 代表支持 find 相关方法的资源
* Extension 代表扩展等。

##### client.py
包括两个类 BaseClient 和 HTTPClient。
* BaseClient 顶层类，利用自身属性 http_client 来发出各种 HTTP 资源请求。
* HTTPClient 实现向 OpenStack 的服务发出 HTTP 请求。

##### exceptions.py
定义了各种异常类型。

##### fake_client.py
定义了 FakeHTTPClient 类，继承自 client.HTTPClient 类。一个假的客户端，调用各种方法，直接返回写好的回复内容。

#### cliutils.py
命令行辅助函数，包括在给定 manager 中查找资源，获取输入的密码等。

#### gettextutils.py
国际化字符串相关方法。

#### importutils.py
跟导入相关的方法，包括 import_class、import_module、import_object、import_object_ns
import_versioned_module 和 try_import。
这些方法会根据传入的参数和名称来导入指定的类、模块、对象等。

#### strutils.py
对字符串进行操作，包括转码等。

#### timeutils.py
对时间进行比较，提取和格式化等。

#### uuidutils.py
生成 uuid 和进行校验等。
