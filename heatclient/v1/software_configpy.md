### software_configs.py
software_config 资源及管理模块。

* SoftwareConfig 类，继承自 base.Resource，作为一种资源，支持删除和获取数据操作。
```python
class SoftwareConfig(base.Resource):
    def __repr__(self):
        return "<SoftwareConfig %s>" % self._info

    def delete(self):
        return self.manager.delete(config_id=self.id)

    def data(self, **kwargs):
        return self.manager.data(self, **kwargs)
```


* SoftwareConfigManager，继承自 base.BaseManager，支持获取某个特定软件配置的信息和创建、删除等操作。
```python
class SoftwareConfigManager(base.BaseManager):
    resource_class = SoftwareConfig

    def get(self, config_id):
        """Get the details for a specific software config.

        :param config_id: ID of the software config
        """
        resp, body = self.client.json_request(
            'GET', '/software_configs/%s' % config_id)

        return SoftwareConfig(self, body['software_config'])

    def create(self, **kwargs):
        """Create a software config."""
        resp, body = self.client.json_request('POST', '/software_configs',
                                              data=kwargs)

        return SoftwareConfig(self, body['software_config'])

    def delete(self, config_id):
        """Delete a software config."""
        self._delete("/software_configs/%s" % config_id)
```
