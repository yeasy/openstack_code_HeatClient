## client.py
定义 Client 类，作为对外的统一封装。
实际上会找到指定版本下的 client 模块中的 Client 类。
以 v1 为例，会调用 heatclient.v1.client 模块中的 Client 类。

代码为：

```python
from heatclient.common import utils


def Client(version, *args, **kwargs):
    module = utils.import_versioned_module(version, 'client')
    client_class = getattr(module, 'Client')
    return client_class(*args, **kwargs)
```
