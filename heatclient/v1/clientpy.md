### client.py
主要定义了 Client 类。代表跟 Heat 服务端进行交互的客户端。

其中 httpclient 是发出 http 请求的具体代理。

所有资源（包括 stacks、resources、resources_type、events、actions、build_info、software_deployments、software_configs）操作都是通过调用对应的 manager，并传递 http_client 来进行的。

例如对 stack 资源进行操作的话，通过 self.stacks = stacks.StackManager(self.http_client) 进行。

其代码为如下：
```python
class Client(object):
    """Client for the Heat v1 API.

    :param string endpoint: A user-supplied endpoint URL for the heat
                            service.
    :param string token: Token for authentication.
    :param integer timeout: Allows customization of the timeout for client
                            http requests. (optional)
    """

    def __init__(self, *args, **kwargs):
        """Initialize a new client for the Heat v1 API."""
        self.http_client = http._construct_http_client(*args, **kwargs)
        self.stacks = stacks.StackManager(self.http_client)
        self.resources = resources.ResourceManager(self.http_client)
        self.resource_types = resource_types.ResourceTypeManager(
            self.http_client)
        self.events = events.EventManager(self.http_client)
        self.actions = actions.ActionManager(self.http_client)
        self.build_info = build_info.BuildInfoManager(self.http_client)
        self.software_deployments = \
            software_deployments.SoftwareDeploymentManager(
                self.http_client)
        self.software_configs = software_configs.SoftwareConfigManager(
            self.http_client)
```
