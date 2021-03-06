## [memset(this, 0, sizeof *this)](https://www.cnblogs.com/renzhuang/articles/6737917.html)
有时候类里面定义了很多int,char,struct等c语言里的那些类型的变量，我习惯在构造函数中将它们初始化为0，但是一句句的写太麻烦，所以直接就memset(this, 0, sizeof *this);将整个对象的内存全部置为0。对于这种情形可以很好的工作，但是下面几种情形是不可以这么使用的：

1.类含有虚函数表：这么做会破坏虚函数表，后续对虚函数的调用都将出现异常

2.类中含有C++类型的对象：例如，类中定义了一个list的对象，由于在构造函数体的代码执行之前就对list对象完成了初始化，假设list在它的构造函数里分配了内存，那么我们这么一做就破坏了list对象的内存。

 

某些人认为不应该在构造函数中使用this指针，因为这时this对象还没有完全形成。

但是，只要小心，是可以在构造函数中使用this指针的：

 

初始化列表中

因为“对象还没有完全形成”不意味着“什么都没有”。

在进入构造函数（及其chaining）之前，Compiler会：

●给class的instance分配内存

●建立运行时刻系统所需的信息（如vtbl等）

●##缺省地## 构造所有类成员

-----------------------------【能】---------------------------------

构造函数的函数体（或构造函数所调用的函数）【能】可靠地访问：

●基类中声明的数据成员

●构造函数所属类声明的数据成员

这是因为所有这些数据成员被保证在构造函数函数体开始执行时已经被完整的建立。

-----------------------------【不能】---------------------------------

构造函数的函数体（或构造函数所调用的函数）【不能】向下调用：

●被派生类重定义的虚函数

这是因为在基类的构造函数执行期间，“对象还不是一个派生类的对象”。
```cpp
#include <iostream>
using namespace std;


class A
{
public:
    int a;
    A()  
    { 
        memset(this, 0, sizeof(*this));
        cout << "A cons" << endl; 
    }
    ~A()  
    {
        cout << "A des" << endl; 
    }

};

void play()
{
    A o;
    cout << o.a << endl;
}

void main()
{
    play();

    system("pause");
}
```
输出结果：
```shell
A cons
0
A des
```
如果没有 memset(this,0,(*this)),那么输出的a的值就是垃圾值。
```shell
A cons
-858993460
A des
```
