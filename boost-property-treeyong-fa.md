# Boost Property Tree 基本用法

### 数据的访问

[http://www.boost.org/doc/libs/1\_47\_0/doc/html/boost\_propertytree/accessing.html](http://www.boost.org/doc/libs/1_47_0/doc/html/boost_propertytree/accessing.html)

声明 Key 是 string、Value 也是 string 类型的树

```
pt::ptree root;
```

访问节点上的值

```cpp
pt::ptree defRoot;
defRoot.put_value("12");
////////////////////////
std::string val = defRoot.get_value<std::string>();
```

设置节点的值

```cpp
pt::ptree defRoot;
defRoot.put_value("12");
```

声明自定义类型的树

```cpp
struct Item {
    unsigned int ip;
} item, *pItem;

pt::basic_ptree<unsigned long, struct Item> root;

item.ip = 0x123;
root.put_value(item);

pItem = &root.get_value<struct Item>();
```



