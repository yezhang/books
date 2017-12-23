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

pt::basic_ptree<std::string, struct Item> root;

item.ip = 0x123;
root.put_value(item);

pItem = &root.get_value<struct Item>();
```

注意：如果自定义的key值不是 string 类型，是自定义类型，则需要注意一下内容：

boost\_1\_66\_0\boost\property\_tree\ptree\_fwd.hpp

```
/// If you want to use a custom key type, specialize this struct for it
/// and give it a 'type' typedef that specifies your path type. The path
/// type must conform to the Path concept described in the documentation.
/// This is already specialized for std::basic_string.
template <typename Key>
struct path_of;
```

清楚数据和孩子节点

```cpp
/** Clear this tree completely, of both data and children. */
void clear();
```



