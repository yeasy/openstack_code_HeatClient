### software_deployments.py
定义类 SoftwareDeployment 和 SoftwareDeploymentManager。
前者继承自 base.Resource，作为一种资源，支持更新和获取数据操作。
后者继承自 base.BaseManager，支持对软件部署的 CURD 和获取 metadata等操作。


software_deployments 资源及管理模块。

* SoftwareDeployment 类，继承自 base.Resource，作为一种资源，支持更新和获取数据操作。
```python
class SoftwareDeployment(base.Resource):
    def __repr__(self):
        return "<SoftwareDeployment %s>" % self._info

    def update(self, **fields):
        self.manager.update(deployment_id=self.id, **fields)

    def delete(self):
        return self.manager.delete(deployment_id=self.id)
```


* SoftwareConfigManager，继承自 base.BaseManager，支持对软件部署的 CURD 和获取 metadata等操作。
```python
class SoftwareDeploymentManager(base.BaseManager):
    resource_class = SoftwareDeployment

    def list(self, **kwargs):
        """Get a list of software deployments.
        :rtype: list of :class:`SoftwareDeployment`
        """
        url = '/software_deployments?%s' % parse.urlencode(kwargs)
        return self._list(url, "software_deployments")

    def metadata(self, server_id):
        """Get a grouped collection of software deployment metadata for a
        given server.
        :rtype: list of :class:`SoftwareDeployment`
        """
        url = '/software_deployments/metadata/%s' % parse.quote(
            server_id, '')
        resp, body = self.client.json_request('GET', url)
        return body['metadata']

    def get(self, deployment_id):
        """Get the details for a specific software deployment.

        :param deployment_id: ID of the software deployment
        """
        resp, body = self.client.json_request(
            'GET', '/software_deployments/%s' % deployment_id)

        return SoftwareDeployment(self, body['software_deployment'])

    def create(self, **kwargs):
        """Create a software deployment."""
        resp, body = self.client.json_request(
            'POST', '/software_deployments', data=kwargs)
        return SoftwareDeployment(self, body['software_deployment'])

    def update(self, deployment_id, **kwargs):
        """Update a software deployment."""
        resp, body = self.client.json_request(
            'PUT', '/software_deployments/%s' % deployment_id, data=kwargs)
        return SoftwareDeployment(self, body['software_deployment'])

    def delete(self, deployment_id):
        """Delete a software deployment."""
        self._delete("/software_deployments/%s" % deployment_id)
```
