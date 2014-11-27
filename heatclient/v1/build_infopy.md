### build_info.py
build_info 资源及管理模块。
* BuildInfo 类，继承自 base.Resource，代表一个 build_info 资源，包括 build_info 方法。

```python
from heatclient.openstack.common.apiclient import base


class BuildInfo(base.Resource):
    def __repr__(self):
        return "<BuildInfo %s>" % self._info

    def build_info(self):
        return self.manager.build_info()
```

* BuildInfoManager，继承自 base.BaseManager，提供利用自身的 client 来发出 build_info 请求的方法。

```python
class BuildInfoManager(base.BaseManager):
    resource_class = BuildInfo

    def build_info(self):
        resp, body = self.client.json_request('GET', '/build_info')
        return body
```
