### resources.py
resource 资源及管理模块。

* Resource和 类，继承自 base.Resource，代表一个 event 资源，支持更新、删除和获取数据操作。
```python
class Resource(base.Resource):
    def __repr__(self):
        return "<Resource %s>" % self._info

    def update(self, **fields):
        self.manager.update(self, **fields)

    def delete(self):
        return self.manager.delete(self)

    def data(self, **kwargs):
        return self.manager.data(self, **kwargs)
```

* ResourceManager，继承自 stacks.StackChildManager，支持对资源进行列出、获取和发出信号等操作。
```python
class ResourceManager(stacks.StackChildManager):
    resource_class = Resource

    def list(self, stack_id, nested_depth=0):
        """Get a list of resources.
        :rtype: list of :class:`Resource`
        """
        url = '/stacks/%s/resources' % stack_id
        if nested_depth:
            url += '?nested_depth=%s' % nested_depth
        return self._list(url, "resources")

    def get(self, stack_id, resource_name):
        """Get the details for a specific resource.

        :param stack_id: ID of stack containing the resource
        :param resource_name: ID of resource to get the details for
        """
        stack_id = self._resolve_stack_id(stack_id)
        url_str = '/stacks/%s/resources/%s' % (
                  parse.quote(stack_id, ''),
                  parse.quote(strutils.safe_encode(resource_name), ''))
        resp, body = self.client.json_request('GET', url_str)
        return Resource(self, body['resource'])

    def metadata(self, stack_id, resource_name):
        """Get the metadata for a specific resource.

        :param stack_id: ID of stack containing the resource
        :param resource_name: ID of resource to get metadata for
        """
        stack_id = self._resolve_stack_id(stack_id)
        url_str = '/stacks/%s/resources/%s/metadata' % (
                  parse.quote(stack_id, ''),
                  parse.quote(strutils.safe_encode(resource_name), ''))
        resp, body = self.client.json_request('GET', url_str)
        return body['metadata']

    def signal(self, stack_id, resource_name, data=None):
        """Signal a specific resource.

        :param stack_id: ID of stack containing the resource
        :param resource_name: ID of resource to send signal to
        """
        stack_id = self._resolve_stack_id(stack_id)
        url_str = '/stacks/%s/resources/%s/signal' % (
                  parse.quote(stack_id, ''),
                  parse.quote(strutils.safe_encode(resource_name), ''))
        resp, body = self.client.json_request('POST', url_str, data=data)
        return body

    def generate_template(self, resource_name):
        """DEPRECATED! Use `generate_template` of `ResourceTypeManager`
        instead.
        """
        url_str = '/resource_types/%s/template' % (
                  parse.quote(strutils.safe_encode(resource_name), ''))
        resp, body = self.client.json_request('GET', url_str)
        return body
```

