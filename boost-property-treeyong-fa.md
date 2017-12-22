

数据的访问

http://www.boost.org/doc/libs/1\_47\_0/doc/html/boost\_propertytree/accessing.html

访问节点上的值

```cpp
pt::ptree root;
root.put_value(0x123);
int value = root.get_value<int>();
```

设置节点的值

```cpp
ptree pt;
pt.put_value(3.14f);
```



