## common
### environment_format.py
提供对环境中字符串的格式检查等辅助操作。

例如 parse 方法将检查一个字符串是否符合 YAML 格式，如果符合将它转化为数据结构。

```python
def parse(env_str):
    '''Takes a string and returns a dict containing the parsed structure.

    This includes determination of whether the string is using the
    YAML format.
    '''
    try:
        env = yaml.load(env_str, Loader=yaml_loader)
    except yaml.YAMLError as yea:
        raise ValueError(yea)
    else:
        if env is None:
            env = {}
        elif not isinstance(env, dict):
            raise ValueError('The environment is not a valid '
                             'YAML mapping data type.')

    for param in env:
        if param not in SECTIONS:
            raise ValueError('environment has wrong section "%s"' % param)

    return env
```

### http.py
主要实现了一个完整的 HTTPClient 类，支持 CRUD 操作，以及一个继承自 HTTPClient 类的 SessionClient 类。

后者基于 Keystone 的客户端 session。

### template_format.py
提供对模板中字符串格式进行处理的方法。比如检查是否符合 YAML 标准，以及转化字符串为解析后的数据结构等。

### template_utils.py
对模板进行操作的若干辅助方法，包括 get_template_contents() 方法，从文件中获取模板内容等。

### utils.py
一些辅助方法，包括查找资源、导入模块、格式化参数等方法。
