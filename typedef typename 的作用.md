# 关于typename的疑点

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

### 使用说明

```
class MyArray 
{ 
public：
typedef int LengthType;
.....
}

template<class T>
void MyMethod( T myarr ) 
{ 
typedef typename T::LengthType LengthType; 
LengthType length = myarr.GetLength; 
}
```

**这个时候typename的作用就是告诉c++编译器，typename后面的字符串为一个类型名称，而不是成员函数或者成员变量。这个时候如果前面没有typename，编译器没有任何办法知道T::LengthType是一个类型还是一个成员名称(静态数据成员或者静态函数)，所以编译不能够通过。**


***typedef创建了存在类型的别名，而typename告诉编译` std::vector<T>::size_type`是一个类型而不是一个成员。 ***

### typename 和 class 的区别
 
 - 在模板定义中，typename和class没有区别
 - typename的另一个作用是使用嵌套依赖类型

### typename的作用

- 用在模板定义中，typename是用于表明其后的模板参数是类型参数
- 用于模板中表明，“内嵌依赖类型名”





