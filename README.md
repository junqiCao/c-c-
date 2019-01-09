Table of Contents
=================

* [模板](#%E6%A8%A1%E6%9D%BF)
  * [函数模板](#%E5%87%BD%E6%95%B0%E6%A8%A1%E6%9D%BF)
    * [定义：](#%E5%AE%9A%E4%B9%89)
    * [定义方法：](#%E5%AE%9A%E4%B9%89%E6%96%B9%E6%B3%95)
    * [使用方法](#%E4%BD%BF%E7%94%A8%E6%96%B9%E6%B3%95)
    * [注意事项](#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9)
  * [类模板](#%E7%B1%BB%E6%A8%A1%E6%9D%BF)
    * [定义：](#%E5%AE%9A%E4%B9%89-1)
    * [定义方法：](#%E5%AE%9A%E4%B9%89%E6%96%B9%E6%B3%95-1)
    * [使用方法](#%E4%BD%BF%E7%94%A8%E6%96%B9%E6%B3%95-1)
    * [注意事项](#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9-1)
## 模板

模板（Template）指C++程序设计设计语言中采用类型作为参数的程序设计，支持通用程序设计。C++ 的标准库提供许多有用的函数大多结合了模板的观念，如STL以及IO Stream。

### 函数模板

#### 定义： 

```template <typename identifier> function_declaration;//函数模板的定义```

**类模板和函数模板的意义是一样的。**
#### 定义方法：
```
//method.h
template<typename  T> void swap(T& t1, T& t2) 
{
    T tmpT;
    tmpT = t1;
    t1 = t2;
    t2 = tmpT;
}
```
#### 使用方法
``` 
//main.cpp
#include <stdio.h>
#include "method.h"
int main()
{
    //模板方法 
    int num1 = 1, num2 = 2;
    swap<int>(num1, num2);
    printf("num1:%d, num2:%d\n", num1, num2);  
    return 0;
}
```
#### 注意事项
- 函数模板成员函数的定义通常放在头文件中

### 类模板
#### 定义：
```temmplate <class identifier> function_declaration;  //类模板的定义```
**类模板和函数模板的意义是一样的。**
#### 定义方法：
```
template <class T> //声明一个模板，虚拟类型名为T。**注意：这里没有分号。**
class Compare //类模板名为Compare
{
public:

	Compare(T a, T b)
	{
		x = a;
		y = b;
	}

	T max()
	{
		return (x > y) ? x : y;
	}

	T min()
	{
		return(x < y) ? x : y;
	}
	T add(T a, T b);
private:
	T x, y;
};

```
在类模板外定义函数的形式为
```
template <class T> T Compare<T>::add(T a, T b)
{
	return a + b;
}
```

#### 使用方法
```
Compare <int> cmp(4, 7);
Compare <float> cmp(4.0, 7.0);
```
#### 注意事项

- 声明类模板时要增加一行 ```template <class T>```
- 固定的类型名换成虚拟类型参数名T
- 类模板成员函数的定义通常放在头文件中


