### actions.py
action 资源及管理模块。

* Action 类，继承自 base.Resource，代表一个 action 资源，包括 update、delete、data 等方法。

```python
class Action(base.Resource):
    def __repr__(self):
        return "<Action %s>" % self._info

    def update(self, **fields):
        self.manager.update(self, **fields)

    def delete(self):
        return self.manager.delete(self)

    def data(self, **kwargs):
        return self.manager.data(self, **kwargs)
```
* ActionManager，继承自 stacks.StackChildManager，管理行动资源，提供利用自身的 client 来发出 suspend、resume、cancel_update、check 等请求的方法。

```python
class ActionManager(stacks.StackChildManager):
    resource_class = Action

    def suspend(self, stack_id):
        """Suspend a stack."""
        body = {'suspend': None}
        resp, body = self.client.json_request('POST',
                                              '/stacks/%s/actions' % stack_id,
                                              data=body)

    def resume(self, stack_id):
        """Resume a stack."""
        body = {'resume': None}
        resp, body = self.client.json_request('POST',
                                              '/stacks/%s/actions' % stack_id,
                                              data=body)

    def cancel_update(self, stack_id):
        """Cancel running update of a stack."""
        body = {'cancel_update': None}
        resp, body = self.client.json_request('POST',
                                              '/stacks/%s/actions' % stack_id,
                                              data=body)

    def check(self, stack_id):
        """Check a stack."""
        body = {'check': None}
        resp, body = self.client.json_request('POST',
                                              '/stacks/%s/actions' % stack_id,
                                              data=body)
```
