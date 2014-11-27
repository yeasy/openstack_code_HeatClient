### resource_types.py
resource_type 资源及管理模块。

* ResourceType 类，继承自 base.Resource，代表一个 resource_type 资源，包括 data 等方法。

```python
class ResourceType(base.Resource):
    def __repr__(self):
        return "<ResourceType %s>" % self._info

    def data(self, **kwargs):
        return self.manager.data(self, **kwargs)

    def _add_details(self, info):
        self.resource_type = info
```

* ResourceTypeManager，继承自 base.BaseManager，支持获取某个特定资源类型的信息和生成模板操作。

```python
class ResourceTypeManager(base.BaseManager):
    resource_class = ResourceType

    def list(self):
        """Get a list of resource types.
        :rtype: list of :class:`ResourceType`
        """
        return self._list('/resource_types', 'resource_types')

    def get(self, resource_type):
        """Get the details for a specific resource_type.

        :param resource_type: name of the resource type to get the details for
        """
        url_str = '/resource_types/%s' % (
                  parse.quote(strutils.safe_encode(resource_type), ''))
        resp, body = self.client.json_request('GET', url_str)
        return body

    def generate_template(self, resource_type):
        url_str = '/resource_types/%s/template' % (
                  parse.quote(strutils.safe_encode(resource_type), ''))
        resp, body = self.client.json_request('GET', url_str)
        return body
```
