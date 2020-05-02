# 找工编程语言问题

## C++
### 1. Struct 的对齐机制
**原则A**：struct或者union的成员，第一个成员在偏移0的位置，之后的每个成员的起始位置必须是当前成员大小的整数倍

**原则B**：如果结构体A含有结构体成员B，那么B的起始位置必须是B中最大元素大小整数倍地址

**原则C**：结构体的总大小，必须是内部最大成员的整数倍；

```cpp
struct st1
{
    int *p;
    int i;
    char a;
}
```

- 指针 8 字节
- int 4 字节，起始位置为8符合原则A
- char 1 字节，要求符合原则C，所以补全至 16 字节


```cpp
struct st2
{
    char a;
    int *p;
    int i;
}
```
- char 1 字节
- 指针 8 字节，要求符合原则A，则补到8字节作为起始位置
- int 4 字节，起始位置16符合原则B，按原则C补全至24字节

### 2. 各数据类型大小
|type|size|
|---|---|
|char|1字节|
|short|2字节|
|int|4字节|
|long|4字节|
|long long|8字节|
|float|4字节|
|double|8字节|
|long double|8字节|

32位与64位系统唯一区别：指针大小为 4字节 与 8字节。

### 3. 静态成员
1. 类的静态成员属于整个类,而不是某个对象，可以被类的所有方法访问，子类当然可以访问父类静态成员；
2. 静态方法属于整个类，在对象创建之前就已经分配空间，类的非静态成员要在对象创建后才有内存。所以静态方法只能访问静态成员，不能访问非静态成员；
3. 静态成员可以被任一对象修改，修改后的值可以被所有对象共享。
 
## Golang

### 1. 为啥GO里面的channel比别的语言好？
因为不用加锁。