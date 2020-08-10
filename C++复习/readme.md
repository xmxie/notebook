### 数组反转

<algorithm>

reverse（list.begin(),list.end());

### 字符串相关

insert(size_t pos,size_t n,char c);

**insert的效率远高于a=(string)a+(string)b**

**push_back()与pop_back()，向字符串尾添加或删除一个字符**

## std库函数

<algorithm>

#### 二分查找

int binary_search(arr[],arr[]+size,index)

```C++
int b=binary_search(a,a+9,4);//查找成功，返回1,失败返回0
```

int lower_bound（arr[],arr[]+size,index)//在first和last中的前闭后开区间进行二分查找，返回大于或等于val的第一个元素位置(注意是地址)。如果所有元素都小于val，则返回last的位置）。

```C++
pos==lower_bound(number,number+8,target)-number , pos为大于等于target的第一个元素的下标
```

int upper_bound与lower_bound相似，返回大于而不是等于的第一个位置，字面意思

#### 数据类型

查看类型

#include <typeinfo>

typeid(object);

#### std::itoa

用顺序递增的值赋值指定范围内的元素 。	

void iota( ForwardIterator first,ForwardIterator last, T value );

first，last：
分别指向序列中初始及末尾位置的正向迭代器（Forward Iterators）。这个范围即 [first,last) ，包括 first 到 last 间的所有元素，包括 first 指向的元素，但不包括 last 指向的元素。
val：用于累加的初始值。
原文链接：https://blog.csdn.net/s_lisheng/article/details/75282242

#### max/min



## 内存分配

### malloc/memset

void* malloc（size),需要显式转换为需要的类型

void* memeset（void* dest,int c,size_t count);//dest为目标指针，c为目标值，count为填充区域大小（size）而不是字面意思上的数目，如sizeof(int)*n



# 数据结构

## 树状数组

利用二进制原理解决区间变化问题

https://www.cnblogs.com/xenny/p/9739600.html

## Set

#### insert()插入 

insert().second返回插入成功或失败

insert().first返回插入的位置

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

