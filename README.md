# C++ Primer Plus!!!

## 第１章　预备知识

**包含部分：**

OOP部分赋予了C++语言将问题所涉及的概念联系起来的能力

C部分则赋予了C++语言紧密联系硬件的能力

在C++获得一定程度的成功后，Stroustrup才添加了模板，这使得进行泛型编程成为可能

## 第二章 开始学习C++

**函数头**[ int main() ]:　对函数与程序其他部分之间的借口进行了总结

int代表这函数返回给调用它的程序的信息类型

> **Ｓｏ：main函数返回int型，不从调用它的函数那里获得任何参数信息**



**名称空间（using namespace std）:**　等效于将其中的名称如cout换为std::cout，或使用的头文件是iostream.h

> **Ｓｏ：std是描述了一个包括iostream的名称空间？不然为什么include库了还要说明用的那个名称空间**

**向类对象发送消息有两种方法**（如：告诉cout什么）

1. 向他发送一条消息
2. 重新定义运算符（cin / cout）



**原型**只描述函数接口，而**定义**中包含了函数的代码

> Ｃ和C++将库函数的这两项特性分开了，库文件中包含了函数的编译代码，而头文件则包含了原型

**Ｓｏ：**

调用库函数的时候可以

+ 在源代码文件中输入函数原型
+ 包含头文件cmath，其中定义了原型

**函数原型**一般要在call之前出现

> **Ｓｏ：可能因为跟向声明变量一样，也是开拓一个空间用来存储这个函数的返回值**

 

## 第三章 处理数据

面向对象编程（OOP）的本质是设计并扩展自己的数据类型！



signed short：-32768 ~ 32767

unsigned short ： 0 ~ 65535   	 ——二者超过**重置点**时都会绕回“原点”



不同基数（进制）的赋值方法

```C++
int x = 42;       //10进制
int y = 0x42;	  //16进制
int z = 042;	  //8进制
cout << hex;	  //转换为16进制输出模式
cout << oct;	  //转换为8进制输出模式
```



存储常量时会顺序使用最少能储存他的类型；

（不带后缀时）与10进制不同：16或8进制存储不下时会考察能否使用当前类型的unsigned类型

> #### **So:** 可以用这个方法配合sizeof()计算某个未知值的大小范围；



const比#define更灵活更好用

### 3.3 浮点型

特殊表示形式：+5.37E+16

一般默认存储为double类型，要存储为float类型可以如+5.37E+16**f**在结尾加一个f或F，同理l或1位long double

cout和float一般都只作用数字中前6、7位！

### 3.4 C++算术运算符

/运算符：如果两个操作数都是整数，则结果为商的整数部分

%运算符：两个操作数都必须会整型

```C++
cout.setf(ios_base::fixed, ios_base::floatfield);
//迫使输出使用定点表示法(而非E表示法)，并显示到小数点后6位
```

**1. 类型转换：值先转换为接收变量的类型，再赋值**

So:赋值给取值范围更大的值一般不会有什么问题，而大的赋值给小的时候值就不确定了！

**2. 使用{ }赋值（列表初始化）**

```C++
char c4 = {x}; //不允许，因为变量的值可能很大
x = 31325;
char c5 = x;   //允许
```

**3. 表达式中的转换**

bool、char、unsigned char、signed char和short在表达式中会被转换为int

低级别的在运算时会被转换为高级别的（避免丢失数据）



## 第四章 复合类型

### 4.1 数组

**类**也是一种复合类型

```C++
float loans[20]  //loan的类型不是数组，而是float数组
int yams[3] = {20, 15}    //{}赋值Okay， 括号为空代表全0
yams[3] = {20, 15, 5}    //不行，只能在初始化时这样赋值
```

### 4.2 字符串

**字符串数组初始化的小技巧：**

```C++
char fish[] = "Bubbles";   //可以让编译器自行确定大小比较靠谱
```

**用char数组来存储字符串可能发生的错误：**

```C++
cin >> name[20];
//打字输入Echo Xie
cin >> home[20];
//不再需要输入
```

> 因为编译器将中间的空格作为结束符，从而将一个字符串分为了两次输入

**由上述错误引出，istream中的类（如cin）提供了面向行的成员函数getline()/ get()**

```C++
cin.getline(name, 20).getline(home, 20);
cin.get(name, 20).get().get(home, 20);//cin.get()函数返回一个cin对象,再用来调用get()
//.get()不带参数代表读取下一个字符哪怕是换行符
```

> 若读到空行会阻断接下来的读取！

**混合输入字符串和数字：**

```C++
cin >> year;
//输入2000
char address[80];
cin.getline(address, 80);
//会出现getline到了一个换行符，因为2000后面的换行符在cin流里但没有被拿走
//因此需要改为：
cin >> year;
cin.get():
......
```

> #### cin.getline()读一行+换行符0
>
> #### cin.get(dir, size)读一行（留下换行符）
>
> #### cin.get()读取下一个字符，哪怕是换行符

### 4.3 String类简介

与iostream类相同，需要#include <string>

```C++
getline(cin, str) //意为将cin 存入 str中
```

```C++ 
wchar_t title[] = L"TitleText"；  //用L输入wchar string
char16_t name[] = u"NameText";	 //用u输入char_16 string
char32_t car[] = U"CarText";	 //用U输入char_32 string
R"(原始字符串)"    //可以在“和/中间加任何字符但开头结尾要相同
```

### 4.4 结构简介

强强强！！！

### 4.5 共用体

kinda 变形体，某一时刻只有一个固定类型

作用是可以节省空间，例如有的id是int而有的是string

### 4.6 枚举

```C++
enum categr {red = 0, green = 1, blue = 9};
categr = red
int i = red    //=0
```

> #### 可分类用

### 4.7  指针和自由存储空间

OOP相对于过程性编程强调在运行阶段（而不是编译阶段）进行决策，例如可以使用关键字new来重新请求合适的内存！

此时：地址成为指定的量，而值称为派生量。

> int*  sth 整型的间接变量（indirect value）sth
>
> int   *sth 意为取消引用（dereference） sth后是整型

```C++
int * pt = &higgens;  //初始化的是指针pt而不是整型*pt
//可理解为：integer‘s indirect value is &...
```

**一定要在对指针该应用接触引用运算符（*）之前，将指针初始化为一个确定的、适当的地址。这是关于使用指针的金科玉律**

```C++
int * pt；
pt = 0xB8000000;  //会报错，因为左边是指针类型，右边是整型
pt = (int *)0xB8000000;  //正确，需要强制类型转换
```

**指针真正的用武之地在于，在运行阶段分配未命名的内存以存储值！！！（节省内存）**

再加上声明时一定要赋值，因此体现出new函数的重要性，相对应使用完后可以delete来释放空间

> delete不能释放声明变量

```C++
int * psome = new int [10];   //声明数组大小的不在前面在后面，前面只存储数据按什么类型解析
delete [] psome;   //对于数组指针的特殊释放语句
```

> 通过指针访问数组元素的方法为psome[0]、psome[1]....因为数组本身就是通过指针访问的！！

```C++
short tell[10];
//tell+1代表地址加2
//&tell+1代表地址加20
```







自2020-6-8日起以C++ Primer Plus为中心自学Ｃ++的过程与心得！欢迎大家交流
