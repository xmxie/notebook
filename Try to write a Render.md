

# Try to write a Render

# 图形学算法

## 线段光栅化：Bresenham's line algorithm

线段光栅化：给定线段的两个端点，返回可以近似表示这条线段的所有像素点坐标

Bresenham算法解决的是计算DDA（利用斜率，计算x增长1时对应的y坐标或y增长1时对应的x坐标，四舍五入得到结果像素点的方法）时需要进行多次浮点数运算的问题。

![image-20201024131206242](C:\Users\95462\AppData\Roaming\Typora\typora-user-images\image-20201024131206242.png)

Bresenham算法将原本DDA每一次计算斜率，四舍五入取点的方法，改为判断下一个点与原有点在同一行还是向斜率方向增长一位的二选一方法。（默认斜率为正，可以通过对称解决正负问题）

**假定**
$$
a=AB,b=BC,m=\frac{\Delta y}{\Delta x}（0<m<1),d=a-b
$$
**则最终只需要判定d的正负即可**

**那么当$x$增加时，$a$只可能增加$1-m$或减少$m$(即y值固定加m,而后上顶点是否加1，)。**

**同理$b$只可能增加m或减少1-m**

A为顶点y坐标值
$$
\begin{aligned} 
             origin&=A-y&,   \\  
             new&=
             \begin{array}{}
             	(A+1)-(y+m)&=origin+(1-m)\\
             	A-(y+m)&=origin-m
             \end{array}
             \\  
            
\end{aligned}
$$
显然当a增加时b减少，a减少时b增加，**则d的变量只可能为$+2(1-m)$或$-2m$**

**又有$\Delta y$和$\Delta x$为整数（起始点和终止点坐标为整数）**

为了避免浮点数运算，这里利用一个假定$\Delta x>0$，$p=\Delta x*d$来代替d

则问题转移到求p的正负，又有
$$
\begin{aligned}
p_{i+1}&=p_i+2*(\Delta x-\Delta y)&(p_i<=0)\\
p_{i+1}&=p_i-2*\Delta y&(p_i>0)
\end{aligned}
$$
则每一次的运算都可以使用定点运算而不使用浮点数运算	-

最后需要计算初始值$p_1$,推导较为复杂（图片中的d1为b,d2为a,故结果与上述推导是相反的，即图中d=b-a）

![image-20201024162050966](C:\Users\95462\AppData\Roaming\Typora\typora-user-images\image-20201024162050966.png)

![image-20201024162206886](C:\Users\95462\AppData\Roaming\Typora\typora-user-images\image-20201024162206886.png)

故使用原定a、b的结果为负值，如
$$
p_1=\Delta x -2*\Delta y
$$

## 三角形图元光栅化

**两种途径**

1. 任意一个三角形都可以被分为两部分，若将三角形的顶点按照y轴坐标进行排序，可以得到y轴最长的边，而后该三角形可以以此线段顶点以外的顶点，即三角形中间的顶点为基准分为上下两部分，之后进行逐行绘制即可。

   因为不需要考虑线连贯性的问题（只要y轴坐标上都有对应的点即可），在线段光栅化上可以更为简洁。

   ![img](https://raw.githubusercontent.com/ssloy/tinyrenderer/gh-pages/img/02-triangle/3a5643f513.png)

2. 使用三角形的包围盒，通过判断包围盒内的点是否在三角形内进行绘制

   在二维平面判断一个点是否在三角形内可以利用点的参数方程表达式，其中A,B,C为三角形的三个顶点
   $$
   P=(1-u-v) A+u B+v C
   $$

   转为向量表达式即
$$
   P=A+u \overrightarrow{A B}+v \overrightarrow{A C}
   $$
   可以得到
   $$
   \left\{\begin{array}{lll}{\left[\begin{array}{lll}u & v & 1\end{array}\right]}  {\left[\begin{array}{l}\overrightarrow{A B}_{x} \\ \overrightarrow{A C}_{x} \\ \overrightarrow{P A}_{x}\end{array}\right]=0} \\ {\left[\begin{array}{lll}u & v & 1\end{array}\right]\left[\begin{array}{l}\overrightarrow{A B}_{y} \\ \overrightarrow{A C}_{y} \\ \overrightarrow{P A}_{y}\end{array}\right]=0}\end{array}\right.
   $$
   即($\mu,v$)可以通过向量叉乘得到，之后带入判断$(1-\mu-v),\mu,v$认意值若小于0，则点$P$在三角形之外，无需绘制。

# 补充知识

## RGB图片格式

### **原理**

https://yangandmore.github.io/2019/03/27/%E5%9B%BE%E7%89%87RGB%E6%95%B0%E6%8D%AE%E6%A0%BC%E5%BC%8F/

RGB图片格式通过记录三种颜色的色值来显示图片，根据是否使用颜色表等信息，每个像素的存储信息大小有所不同

**索引形式**有RGB1，RGB4，RGB8,分别可以代表2、16、128种颜色。其含义如RGB1为每个像素用1个bit表示，可表示的颜色范围为双色，

像素形式有RGB565,RGB555, RGB24,RGB32,ARGB32

**另外RGB值在内存中通常以小端序存储**,如RGB24在内存中的实际存储顺序为BGR

![github](https://yangandmore.github.io/img/RGB/3.png)

ARGB32存储为BGRA

![github](https://yangandmore.github.io/img/RGB/4.png)

### **常见图片格式**

**PNG**

**结构** 

由一个8字节的PNG文件署名域和按照特定结构组织的3个以上的数据块组成。





**颜色表**

RGB颜色的索引表

****