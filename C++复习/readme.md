### 类型转换

https://segmentfault.com/a/1190000016582440

更详细的解释:https://blog.csdn.net/D_Guco/article/details/106033180

**C风格的隐式转换（type）Target**

隐式类型转换会隐藏类型不匹配的错误. 有时, 目的类型并不符合用户的期望, 甚至用户根本没有意识到发生了类型转换.

**static_cast**

static_cast 转换时并不进行运行时安全检查，所以是非安全的，很容易出问题。

**dynamic_cast**

dynamic_cast 主要用来在继承体系中的安全向下转型,是实现多态的一种方式。它能安全地将指向基类的指针转型为指向子类的指针或引用，并获知转型动作成功是否。如果转型失败会返回null（转型对象为指针时）或抛出异常（转型对象为引用时）。

- dynamic_cast在将父类cast到子类时，父类必须要有虚函数，否则编译器会报错。
- 在类层次间进行上行转换时，dynamic_cast和static_cast的效果是一样的；
- 在进行下行转换时，dynamic_cast具有类型检查的功能，比static_cast更安全

**dynamic_cast会使用运行时信息（RTTI）来进行类型安全检查，因此dynamic_cast存在一定的效率损失。**

**const_cast**

 const_cast 可去除对象的常量性（const），它还可以去除对象的易变性（volatile）

**reinterpret_cast**

常见操作是指针之间的类型转换，比如int\*转为char\*

**reinterpret_cast 运算符并不会改变括号中运算对象的值，而是对该对象从位模式上进行重新解释**

仅重新解释类型，但没有进行二进制的转换：
  1) 转换的类型必须是一个指针，应用、算术类型、函数指针或者成员指针。
  2) 在比特级别上进行转换，可以把一个指针转换成一个整数，也可以把一个整数转换成一个指针（先把一个指针转换成一个整数，在把该整数转换成原类型的指针，还可以得到原先的指针值）。但不能将非32bit的实例转成指针。
  3) 最普通的用途就是在函数指针类型之间进行转换。
  4) 很难保证移植性。

### 字符串相关

#### 字符串与int类型的转换

```C++
std::string::size_type sz;   // alias of size_t

int i_dec = std::stoi(str_dec, &sz);//将非数字部分的下标记录在sz中
int i_hex = std::stoi(str_hex, nullptr, 16);
int i_bin = std::stoi(str_bin, nullptr, 2);
int i_auto = std::stoi(str_auto, nullptr, 0);

//可以使用sz输出剩下的字符串
std::cout << str_dec << ": " << i_dec << " and [" << str_dec.substr(sz) << "]\n";
```
insert(size_t pos,size_t n,char c);

**insert的效率远高于a=(string)a+(string)b**

**push_back()与pop_back()，向字符串尾添加或删除一个字符**

#### api

**copy（）**

Copy sequence of characters from string

需要保证s有足够的空间进行复制（复制不会申请空间）

```C++
size_t copy (char* s, size_t len, size_t pos = 0) const;
```

**strcopy**

## std库函数

### 随机数生成

<random>

```C++
//C++11 随机数生成器
std::default_random_engine random(time(NULL));
//C++11提供的分布
//整数使用的分布
std::uniform_int_distribution<int> dis1(0, 100);
//浮点数使用的分布
std::uniform_real_distribution<double> dis2(0.0, 1.0);
//调用
for(int i = 0; i < 10; ++i)
       cout<<dis2(random)<<' ';
```

**其他的一些随机数生成器**

![img](https://img-blog.csdn.net/20140623082658671?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbHVvdHVvNDQ=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)



<algorithm>

### 二分查找

int binary_search(arr[],arr[]+size,index)

```C++
int b=binary_search(a,a+9,4);//查找成功，返回1,失败返回0
```

int lower_bound（arr[],arr[]+size,index)//在first和last中的前闭后开区间进行二分查找，返回大于或等于val的第一个元素位置(注意是地址)。如果所有元素都小于val，则返回last的位置）

```C++
pos==lower_bound(number,number+8,target)-number , pos为大于等于target的第一个元素的下标
```

int upper_bound与lower_bound相似，返回大于而不是等于的第一个位置，字面意思

### 数据类型

查看类型

#include <typeinfo>

typeid(object);

### std::iota

用顺序递增的值赋值指定范围内的元素 。	

void iota( ForwardIterator first,ForwardIterator last, T value );

first，last：
分别指向序列中初始及末尾位置的正向迭代器（Forward Iterators）。这个范围即 [first,last) ，包括 first 到 last 间的所有元素，包括 first 指向的元素，但不包括 last 指向的元素。
val：用于累加的初始值。
原文链接：https://blog.csdn.net/s_lisheng/article/details/75282242

### max/min

```C++
min({1+i%2+dfs(i/2),1+i%3+dfs(i/3),i})//多个数取最大\最小
```

### log

log默认以e为底数

log2以2为底数

其他底数$log_mn$可以通过log(n)/log(m) (换底公式)得到，返回值为double

### accumulate

头文件：<numeric>

accumulate带有**三个形参**：头两个形参指定要**累加的元素范围**，第三个形参则是**累加的初值**。

```C++
//sum the elements in vec starting the summation with the value 42
int sum = accumulate(vec.begin() , vec.end() , 42);
//它会将区间范围内的值转换为第三个参数的类型，所以如果原类型是double，则应该在第三个参数显式转换为double
//concatenate elements from V and store in sum
string sum = accumulate(v.begin() , v.end() , string(" "));
```

### isdigit(char c)

c是否是阿拉伯数字字符

### inner_product

```C++
cout << inner_product(ivec.begin(), ivec.end(), ivec.begin(), 10) << endl;								
cout << inner_product(ivec.begin(), ivec.end(), ivec.begin(), 10, minus<int>(), plus<int>()) << endl;		
```

ivec{0,1,2,3,4};

参数列表（左矩阵，右矩阵，初始值，点乘符号） 

10 + 0\*0 + 1\*1 + 2\*2 + 3\*3 + 4\*4 = 40

10 - (0+0) - (1+1) - (2+2) - (3+3) - (4+4) = -10     

## 内存分配

### malloc/memset

void* malloc（size),需要显式转换为需要的类型

void* memeset（void* dest,int c,size_t count);//dest为目标指针，c为目标值，count为填充区域大小（size）而不是字面意思上的数目，如sizeof(int)*n

### memcpy/strcpy

```C++
memcpy(void* Dst, void* Src, Size_t size);//复制一段内存
strcpy(char* Dst,char* Src);//strcpy会在遇到/0时终止操作
```

### std::move()/std::forward()

1. C++ 标准库使用比如vector::push_back 等这类函数时,会对参数的对象进行复制,连数据也会复制.这就会造成对象内存的额外创建, 本来原意是想把参数push_back进去就行了.
2. C++11 提供了std::move 函数来把**左值转换为rvalue**, 而且新版的push_back也支持&&参数的重载版本,这时候就可以高效率的使用内存了.

std::move()做得就是强制将变量转换为右值引用类型

需要注意的是，使用move后，原对象就会丢失

**std::forward**

与`std::move()`相区别的是，`move()`会无条件的将一个参数转换成右值，而`forward()`则会保留参数的左右值类型。

forward\<typename>()应该与通用引用（universal reference）一同使用

#### 通用引用

通用引用（universal reference）是Scott Meyers在*C++ and Beyond 2012*演讲中自创的一个词，用来特指一种引用的类型。构成通用引用有两个条件：

1. 必须满足`T&&`这种形式
2. 类型`T`必须是通过推断得到的

可以构成通用引用的有如下几种可能：

1. 函数模板参数（function template parameters）

   ```C++
    template <typename T>
    void f(T&& param);
   ```

2. `auto`声明（auto declaration）

   ```C++
    auto && var = ...;
   ```

3. `typedef`声明（typedef declaration）

4. `decltype`声明（decltype declaration）

通用引用下的推导使得我们可以在形参为T&&的情况下传入左值，在此前提下，我们使用函数的时候使用forward（）方法就可以在不改变语义的前提下提高效率

### std::copy()

```c++
std::copy(start, end, std::back_inserter(container));
```

copy只负责复制，不负责申请空间，所以复制前必须有足够的空间



# 数据结构

## 树状数组

利用二进制原理解决区间变化问题

https://www.cnblogs.com/xenny/p/9739600.html

## Set

#### insert()插入 

insert().second返回插入成功或失败

insert().first返回插入的位置

## Vector

#### [C++数组或vector求最大值最小值](https://www.cnblogs.com/Tang-tangt/p/9352093.html)

可以用max_element（）及min_element（）函数，二者返回的都是迭代器或指针。

头文件：#include<algorithm>

### push_back与emplace_back

push_back()会对传入的对象进行复制放入当前对象的尾端，当传入的对象为右值的时候就会使用移动构造函数，避免调用拷贝构造函数。

emplace_back（）则会在原地构造对象，避免了一切的拷贝、移动构造函数，因此有更高的效率

前提是使用时是在参数列表中初始化对象，在push_back中，需要如下形式

push_back（class(parm))

而emplace_back则更为简洁

emplace_back(parm)

### 迭代器

insert（）插入一个vector可以使用迭代器

dest.insert(dest.end(),src.begin(),src.end());

初始化可以使用迭代器

dest(src.begin(),src.begin()+targetSize);

#### 特殊迭代器

back_inserter() 使用push_back的迭代器

front_inserter() 使用push_front的迭代器

inserter(cap,iterator it) 使用insert的迭代器，初始化接收第二个参数，元素被插入到给定迭代器所表示的元素之前

equal_range(,key_type) 返回一个pair，{lower_bound,upper_bound}

### 切割

如果只需要引用数字而不需要对它们进行操作，那么您可以这样做：

```js
int *array_1 = &lines[0];
int *array_2 = &lines[lines.size() / 2];
```

阵列_1和数组_2实际上是指向向量开始和中间的指针。这是因为STL保证向量将它们的元素存储在一个连续的内存中。

### 内存相关

https://blog.csdn.net/u012658346/article/details/50725933

#### vector的容量不足时分配公式

_Capacity = _Capacity + _Capacity / 2

#### reserve（）

```C++
void reserve (size_type n);
```

 主要是预留Count大小的空间，对应的是容器的容量，目的是保证（_Myend - _Myfirst）>=Count。只有当空间不足时，才会操作，即重新分配一块内存，将原有元素拷贝到新内存，并销毁原有内存

#### resize()

```C++
void resize (size_type n);
void resize (size_type n, value_type val);
```

resize函数**重新分配**大小，改变容器的大小，并且创建对象

**当新的n小于等于size的时候，即使调用第二个形参列表，也不会向vector中加入或改变元素，而只会删除元素**

当n小于当前size()值时候，vector首先会减少size()值 保存前n个元素，然后将超出n的元素删除(remove and destroy)

当n大于当前size()值时候，vector会插入相应数量的元素 使得size()值达到n，并对这些元素进行初始化，如果调用上面的第二个resize函数，指定val，vector会用val来初始化这些新插入的元素

# 多线程

C++11引入了std::thread 

菜鸟教程：https://www.runoob.com/w3cnote/cpp-std-thread.html

几种thread初始化的方式

```C++
std::thread t1; // t1 is not a thread
std::thread t2(f1, n + 1); // pass by value
std::thread t3(f2, std::ref(n)); // pass by reference
std::thread t4(std::move(t3)); // t4 is now running f2(). t3 is no longer a thread
```

**join**:  Join 线程，调用该函数会阻塞当前线程，直到由 *this 所标示的线程执行完毕 join 才返回。

**get_id**: 获取线程 ID，返回一个类型为 std::thread::id 的对象

**detach**: Detach 线程。 将当前线程对象所代表的执行实例与该线程对象分离，使得线程的执行可以单独进行。一旦线程执行完毕，它所分配的资源将会被释放。

```C++
void independentThread()
{
	std::cout << "Starting concurrent thread.\n";
	int n = 0;
	while (n++ < 5) {
		std::this_thread::sleep_for(std::chrono::seconds(1));
		cout << n << "s\n";
	}
	std::cout << "Exiting concurrent thread.\n";
}
void threadCaller()
{
	std::cout << "Starting thread caller.\n";
	std::thread t(independentThread);
	//t.join();//如果使用join，函数将在t执行结束后才执行接下来的语句
	t.detach();//而使用detach就可以将t作为独立线程，调用t的线程将继续执行后续任务
	std::this_thread::sleep_for(std::chrono::seconds(1));
	std::cout << "Exiting thread caller.\n";
}
```

**joinable**: 检查线程是否可被 join。检查当前的线程对象是否表示了一个活动的执行线程，由默认构造函数创建的线程是不能被 join 的。另外，如果某个线程 已经执行完任务，但是没有被 join 的话，该线程依然会被认为是一个活动的执行线程，因此也是可以被 join 的。**每个线程创建后都必须执行join或detach**

**swap**: Swap 线程，交换两个线程对象所代表的底层句柄(underlying handles)。

**yield**: 当前线程放弃执行，操作系统调度另一线程继续执行。（

**sleep_for**: 线程休眠某个指定的时间片(time span)，该线程才被重新唤醒，不过由于线程调度等原因，实际休眠时间可能比 sleep_duration 所表示的时间片更长。

**sleep_until**: 线程休眠至某个指定的时刻(time point)，该线程才被重新唤醒。

```C++
template< class Clock, class Duration >
void sleep_until( const std::chrono::time_point<Clock,Duration>& sleep_time );
```

**hardware_concurrency [static]**: 检测硬件并发特性，返回当前平台的线程实现所支持的线程并发数目，但返回值仅仅只作为系统提示(hint)。

**native_handle**: 返回 native handle（由于 std::thread 的实现和操作系统相关，因此该函数返回与 std::thread 具体实现相关的线程句柄，例如在符合 Posix 标准的平台下(如 Unix/Linux)是 Pthread 库）。



# Tips

string insert()的效率远高于+运算符

越界问题

