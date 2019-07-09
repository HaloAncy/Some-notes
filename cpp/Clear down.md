### 名称空间编译指令

using namespace std;</br>
using 编译指令</br>
std 名称空间</br>

<font color=gray size=1>将其产品封装在一个叫做名称空间的单元中，这样就可以用名称空间的名称来指出想使用哪个厂商的产品。</font>

++std::cout</br> std::endl</br> 省略编译指令using++

```c++
using std::cout;
using std::endl;
using std::cin;
```


##### 使程序能够访问名称空间std

- 将using namepace std;放在函数定义之前，让文件中所有的函数都能够使用名称空间std中所有的元素。
- 将using namespace std;放在待定的函数定义中，让该函数能够使用名称空间std中的所有元素。
- 在特定的函数中使用类似using std::cout;这样的编译指令，让该函数能够使用指定的元素。
- 完全不使用编译指令using，而在需要使用名称空间std中的元素时，使用前缀std::。


### 输入输出

##### cin -istream类对象

cin使用空白（空格、制表符和换行符）来确定字符串的结束位置，</br>这意味着cin在获取字符数组输入时只读取一个单词。</br>
读取该单词后，cin将该字符串放到数组中，并自动在结尾添加空字符。

iotream中的类提供了一些面向行的类成员函数</br>
**getline()和get()**</br>
两个函数都读取一行输入 直到到达换行符</br>
++getline()将丢弃换行符</br>
get()将换行符保留在输入序列中++


```c++
cin.getline(name,20);
//第一个参数 用来存储输入行的数组名称
//第二个参数 要读取的字符数
//如果为20则函数最多读取19个字符
//余下的空间用于存储自动在结尾处添加的空字符

cin.get(name,ArSize);
cin.get(); //处理换行符
cin.get(dessert,Arsize);
//第一次调用后换行符将留在输入队列中
//拼接
cin.get(name,ArSize).get();

getline(cin,str);
cin.getline(charr,20);
```

下一条输入语句将在前一条getline()或get()结束读取的位置开始读取</br>
当get()读取空行后将设置失效位，接下来的输入将被阻断用</br>
cin.clear();</br>
恢复输入。</br>

如果输入行包含的字符数比指定的多，则getline()和get()将把余下的字符留在输入队列中，而getline()还会设置失效位，并关闭后面的输入。


```c++
cin >> year;
cin.get();
//利用表达式cin>>year返回cin对象，将调用拼接
(cin >> year).get();
```

成员函数cin.get(ch)读取输入中的下一个字符（即使它是空格），并将其赋给变量ch。

![6](https://github.com/HaloAncy/Some-notes/blob/master/cpp/picture/6.jpg)

![7](https://github.com/HaloAncy/Some-notes/blob/master/cpp/picture/7.jpg)

##### cout -ostream类对象

++头文件iostream++</br>
-endl-cout</br>
显示整数</br>
-dec 十进制</br>
-hex 十六进制</br>
-oct 八进制

```c++
//合并输出
cout << "" << "" << int << endl;
//可分占一行

//通常cout在显示bool值之前将它们转换为int
//但cout.setf(ios:: boolalpha)函数调用设置了一个标记
//该标记命令cout显示true和false而不是1和0
cout.setf(ios_base::boolalpha);
```

通常cout会删除结尾的零。调用 ++cout.setf()++ 将覆盖这种行为。

##### endl and \n

endl确保程序继续运行前刷新输出（将其立刻显示在屏幕上）

##### getchar()、putchar()

包含头文件stdio.h(cstdio)

类似getchar()</br>
不接受任何参数的cin.get()成员函数返回输入中的下一个字符。</br>
**ch = cin.get();**</br>
类似putchar()</br>
**cout.put(ch)**

![5](https://github.com/HaloAncy/Some-notes/blob/master/cpp/picture/5.jpg)


### sizeof运算符

返回类型或变量的长度，单位为字节

对类型名使用sizeof时，应将名称放在括号中；
对变量名使用该运算符，括号可选。


### <climits>

整型限制</br>
定义了表示各种限制的符号名称</br>
定义了符号变量

<font color=gray size=1>INT_MAX -int</br>
CHAR_BIT -字节</font>


### 赋值

++大括号初始化器++</br>
（可以使用等号，也可以不使用）

```c++
int emus{7};
```


### 数组初始化

- 只对数组的一部分进行初始化，编译器把其他元素设置为0。
- 初始化数组时方括号（[]）为空，C++编译器将计算元素个数。
- 初始化数组时，可省略等号（=）。
- 可不在大括号内包含任何东西，这将把所有元素都设置为0.

**auto**让编译器能够根据初始值的类型推断变量的类型 


### 结构

##### 创建结构 两步

定义结构描述-描述并标记了能够存储在结构中的各种数据类型</br>
然后按描述创建结构变量（结构数据类型）</br>
列表中每一项称为 结构成员

使用成员运算符（.）访问各个成员

结构初始化时 等号可选 如果大括号内未包含任何东西，各个成员都将被设置为零

成员赋值 可以使用赋值运算符将结构赋给另一个同类型的结构（即便成员时数组）

```c++
//C++允许在声明结构变量时省略关键字struct

//可以同时完成定义结构和创建结构变量的工作
struct perke
{
    int key_number;
    char car[12];
}mr_smith, ms_jones;
//甚至可以初始化以这种方式创建的变量
struct perks
{
    int key_number;
    char car[12];
}mr_glitz =
{
    7,
    "Packard"
};
//可以声明没有名称的结构类型，方法是省略名称同时定义一种结构类型和一个这种类型的变量
struct
{
    int x;
    int y;
}position;
```


### 枚举 enum工具

创建符号常量（可以代替const）

使用enum的句法与使用结构相似


```c++
//让spectrum称为新类型的名称：spectrum被称为枚举
enum spectrum {red, orange, yellow, green, blue, violet, indigo, ultraviolet};
//可以用枚举名来声明这种类型的变量
spectrum band;
//在不进行强制类型转换的情况下，只能将定义枚举时使用的枚举量赋给这种枚举的变量
band = blue;

//可以使用赋值运算符来显式地设置枚举量的值
enum bits{one=1, two=2, four=4, eight=8};
//指定的值必须是整数。
//也可以只显式地定义其中一些枚举量的值
enum bigstep{first, second=100, third};
//这里first默认情况下为0。
//后面没有被初始化的枚举量的值将比其前面的枚举量大1。
//可以创建多个值相同的枚举量
enum {zero, null=0, one, numero_uno=1};
//可以使用long甚至long long类型的值
```

将red等作为符号常量，它们对应整数值0~7。这些常量叫作枚举量。</br>
在默认情况下，将整数值赋给枚举量，第一个枚举量的值为0，第二个枚举量的值为1，依此类推。

<font color=gray size=1>因此spectrum变量受到限制，只有8个可能的值。如果试图将一个非法值赋给它，则有些编译器将出现编译器错误，而另一些则发出警告。为获得最大限度的可移植性，应将把非enum值赋给enum变量视为错误。</font>

对于枚举，只定义了赋值运算符。即没有为枚举定义算术运算。

枚举量是整型，可被提升为int类型，反之不能自动转换。

可以用枚举来定义switch语句中使用的符号常量。

如果打算只使用常量，而不创建枚举类型的变量，则可以省略枚举类型的名称。

枚举的取值范围</br>
![1](https://github.com/HaloAncy/Some-notes/blob/master/cpp/picture/1.png)


### 指针 new

在C语言中，可以用库函数malloc()来分配内存；</br>
C++中，使用关键字new请求正确数量的内存以及使用指针来跟踪新分配的内存的位置。

指针真正的用处 在运行阶段分配未命名的内存以及储值

```c++
//返回地址 赋给pn
int *pn = new int;
//将变量的地址赋给指针
int higgens;
int *pt = &higgens;
//第二种情况可以通过名称higgens来访问该int
//第一种情况只能通过该指针进行访问
//pn指向一个数据对象 指的是为数据项分配的内存块

typeName *pointer_name = new typeName;
//常规变量声明分配的内存存储在被成为栈的内存区域中
//new从被称为堆或自由存储区的内存区域分配内存
```

##### delete运算符

使用完内存后将其归还给内存池

```c++
//使用delete时后面要加上指向内存块的指针（最初用new分配的内存块）
int *ps = new int;
...
delete ps;
//这将释放ps指向的内存，但不会删除指针ps本身

//一定要配对地使用new和delete；否则将发生内存泄漏
//也就是说被分配的内存再也无法使用了
//不能使用delete来释放声明变量所获得的内存
//对空指针使用delete是安全的
```

##### 创建数组

在编译时给数组分配内存 被称为静态联编

使用new 数组在程序运行时创建 还可以选择数组长度 动态联编 动态数组

```c++
int *psome = new int[10];
//new运算符返回第一个元素的地址
delete [] psome;
//方括号告诉程序 应释放整个数组

//使用时只要把指针当作数组名使用即可
//数组名和指针之间的根本差别：
//不能修改数组名的值；但指针时变量，因此可以修改它的值。
```

<font color=gray size=1>psome是指向一个int（数组第一个元素）的指针。编译器不能对psome是指向10个整数中的第1个这种情况进行跟踪。因此编写程序时必须让程序跟踪元素的数目，但这种信息不共用。</br>例如，不能使用sizeof运算符来确定动态分配的数组包含的字节数。
</font>

整数变量+1后，其值将增加1</br>
将指针变量+1后，增加的量等于它指向的类型的字节数

数组表达式stack[1] C++编译器将该表达式看作是*(stacks+1)

对数组使用sizeof运算符得到的是数组的长度（这种情况下，C++包含将数组名解释为地址）</br>
对指针应用sizeof得到的是指针的长度

数组名被解释为其第一个元素的地址，而对数组名应用地址运算符时，得到的是整个数组的地址。

```c++
short tell[10];
cout << tell << endl;
cout << &tell << endl;
```

![2](https://github.com/HaloAncy/Some-notes/blob/master/cpp/picture/2.png)

##### 字符串

在C++中，用引号括起的字符串像数组名一样，也是第个元素的地址。

```c++
//获得字符串的副本
ps = new char[strlen(animal)+1];
```

##### 创建结构 访问成员

```c++
//创建一个未命名的inflatable类型并将其地址赋给一个指针
inflatable *ps = new inflatable;
```

创建动态结构时，不能将成员运算符句点用于结构名，因为这种结构没有名称，只是知道它的地址。</br>
**箭头成员运算符（->）**</br>
如果ps指向一个inflatable结构，则ps->price是被指向的结构的price成员

另一种访问结构成员的方法</br>
如果ps是指向结构的指针，则*ps就是被指向的值——结构本身</br>
因此(*ps).price是该结构的price成员

##### C++管理数据内存的方式

- 自动存储：存储在栈中，先进后出
- 静态存储：整个程序执行期间都存在，函数外定义或在声明变量时使用关键字static
- 动态存储（自由存储空间或堆）

##### 将const关键字用于指针

两种不同的方式

```c++
//让指针指向一个常量对象，可以防止使用该指针来修改所指向的值
int age = 39;
const int * pt = &age;
//pt的声明并不意味着它指向的值实际上就是一个常量，而只是意味着对pt而言，这个值是常量
```

将指针本身声明为常量，防止改变指针指向的位置

##### 声明指向函数的指针

必须制定指针指向的函数类型</br>
意味着声明应指定函数的返回类型以及函数的特征标（参数列表）

```c++
//函数原型
double pam(int);
//则正确的指针类型声明如下
double (*pf)(int);
//声明类似，pam是函数，因此(*pf)也是函数，则pf就是函数指针
```

*pf(int)意味着pf()是一个返回指针的函数


### 循环

##### 延时循环

![4](https://github.com/HaloAncy/Some-notes/blob/master/cpp/picture/4.jpg)


### 建立别名

C++为类型建立别名的方式有两种

```c++
//使用预处理器
#define BYTE char
//声明一系列变量时这种方法不适用

//关键字typedef
typedef typeName aliasName;
//该方法不会创建新类型而只是已有的类型建立一个新名称
```

##### typedef

![8](https://github.com/HaloAncy/Some-notes/blob/master/cpp/picture/8.png)


### 函数原型

通常在原型的参数列表中，可以包括变量名，也可以不包括。原型中的变量名相当于占位符，因此不必与函数定义中的变量名相同。
```c++
void cheers(int);
```
ANSI C中的原型是可选的，但在C++中，原型必不可少。</br>
在C++中，括号为空与在括号中使用关键字void是等效的——意味着函数没有参数。在ANSI C中，括号为空意味着不指出参数——这意味着将在后面定义参数列表。在C++中，不指定参数列表时应使用省略号。
```c++
void say_bye(...);
```

##### 向函数传递数组及长度

```c++
//函数头 需要一个形参声明为数组名
int sum_arr(int arr[], int n);
//arr实际上并不是数组，而是一个指针
int sum_arr(int * arr, int n);

//C++中，当且仅当用于函数头或函数原型中，
//int *arr和int arr[]的含义才是相同的，都意味着arr是一个int指针
arr[i] == *(ar+i);
&arr[i] == ar+i;
```

*传递常规变量时，函数将使用该变量的拷贝</br>
但传递数组时，函数将使用原来的数组*

### ZAZA

- if else语句本身是一条语句

替代if else语句的运算符</br>
条件运算符（ ? : ）
```
//如果e1为true，则整个条件表达式的值为e2的值；否则整个表达式的值为e3的值。
expression1 ? expression2 : expression3;
```


- 许多程序员将更直观的表达式variable == value反转为value == variable，以此来捕获将相等运算符误写为赋值运算符的错误。

- 获取函数的地址，使用函数名（后面不跟参数）即可。
