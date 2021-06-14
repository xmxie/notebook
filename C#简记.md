C#简记

## Internal修饰符

对该程序集内可见，在public和protected之间的等级

## Nullable

c#没有C++类似的？运算符，取而代之的是如下使用方法

声明一个 **nullable** 类型（可空类型）的语法如下：

```C#
< data_type> ? <variable_name> = null;
```

即一个附加了可以为null功能的data_type

### Null合并和算符？？

```C#

double? num1 = null;
double? num2 = 3.14157;
double num3;
num3 = num1 ?? 5.34;    // num1 如果为空值则返回 5.34
Console.WriteLine("num3 的值： {0}", num3);
num3 = num2 ?? 5.34;
Console.WriteLine("num3 的值： {0}", num3);
```

## Struct和类的区别

- 1、结构是值类型，它在栈中分配空间；而类是引用类型，它在堆中分配空间，栈中保存的只是引用。
- 2、结构类型直接存储成员数据，让其他类的数据位于堆中，位于栈中的变量保存的是指向堆中数据对象的引用。
- 3、结构不能继承其他的结构或类。