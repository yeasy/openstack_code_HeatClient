### events.py
event 资源及管理模块。

* Event 类，继承自 base.Resource，代表一个 event 资源，包括 update、delete、data 等方法。


```python
 update(self, **fields):
        self.manager.update(self, **fields)

    def delete(self):
        return self.manager.delete(self)

    def data(self, **kwargs):
        return self.manager.data(self, **kwargs)
```

* EventManager，继承自 stacks.StackChildManager，管理行动资源，提供 list、get 方法。

```python
class EventManager(stacks.StackChildManager):
    resource_class = Event

    def list(self, stack_id, resource_name=None, **kwargs):
        """Get a list of events.
        :param stack_id: ID of stack the events belong to
        :param resource_name: Optional name of resources to filter events by
        :rtype: list of :class:`Event`
        """
        params = {}
        if 'filters' in kwargs:
            filters = kwargs.pop('filters')
            params.update(filters)

        for key, value in six.iteritems(kwargs):
            if value:
                params[key] = value

        if resource_name is None:
            url = '/stacks/%s/events' % stack_id
        else:
            stack_id = self._resolve_stack_id(stack_id)
            url = '/stacks/%s/resources/%s/events' % (
                parse.quote(stack_id, ''),
                parse.quote(strutils.safe_encode(resource_name), ''))
        if params:
            url += '?%s' % parse.urlencode(params, True)

        return self._list(url, 'events')

    def get(self, stack_id, resource_name, event_id):
        """Get the details for a specific event.

        :param stack_id: ID of stack containing the event
        :param resource_name: ID of resource the event belongs to
        :param event_id: ID of event to get the details for
        """
        stack_id = self._resolve_stack_id(stack_id)
        url_str = '/stacks/%s/resources/%s/events/%s' % (
                  parse.quote(stack_id, ''),
                  parse.quote(strutils.safe_encode(resource_name), ''),
                  parse.quote(event_id, ''))
        resp, body = self.client.json_request('GET', url_str)
        return Event(self, body['event'])
```
