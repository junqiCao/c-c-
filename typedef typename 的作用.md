# 关于typedef typename的疑点

## typedef typename 使用方法

` typedef typename std::vector<T>::size_type size_type; `

### 问题1： std::vactor<T>::size_type 的意思
 
 参考《STL源码剖析》可得：
 
```
template <class T,class Alloc=alloc>
class vector{
public:
    //...
    typedef size_t size_type;
    //...
};
```

`vector::size_type`是`vector`的嵌套类型定义，其实际等价于 `size_t` 类型。

```
vector<int>::size_type ssssize;
//就等价于
size_t ssssize;
```

### 问题2： 为什么使用typename

`typedef std::vector<T>::size_type size_type;`

在模板类型实例化之前，编译器是不知道`std::vector<T>::size_type是什么东西，有以下三种可能：
- 静态数据成员
- 静态成员函数
- 嵌套类型

那么在加上typename之后就可以确定了是那种类型了，嵌套类型。


### 总结

**typedef创建了存在类型的别名，而typename告诉编译器std::vector<T>::size_type是一个类型而不是一个成员。**


