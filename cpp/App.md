### 模板类vector

效率较低</br>
一种动态数组，可在运行阶段设置vector对象的长度</br>
vector类确实使用new和delete来管理内存，但是自动完成的

**头文件vector**，在名称空间std中

```c++
//模板使用不同的语法指出它存储的数据类型
vector<int> vi;
//vector类使用不同的语法指定元素数
int n;
cin >> n;
vector<double> vd(n);
//创建一个名为vt的vector对象
//可存储n_elem个类型为typeName的元素
//n_elem可以是整型常量，也可以是整型变量
vector<typeName> vt(n_elem);
```


### 模板类array（C++）

**头文件array**,位于名称空间std中

与数组一样，array对象的长度是固定的，使用栈（静态内存分配），效率与数组相同，但更方便安全。

```c++
array<int, 5> ai;
array<double, 4> ad = {1.2, 2.1, 3.43, 4.3};
//创建一个名为arr的array对象
//包含n_elem个类型为typename的元素
array<typeName, n_elem> arr;
//与创建vector对象不同的是，n_elem不能是变量。
```

在C\++11中，可将列表初始化用于vector和array对象，但在C++98中，不能对vector对象这样做。


#### at()

将信息存储到数组的外面。与C语言一样，C++也不检查这种越界错误。

```c++
//vector和array对象的成员函数at()
a2.at(1) = 2.3;
```

中括号表示法和成员函数at()的差别在于，使用at()时，将在运行期间捕获非法索引，而程序默认将中断。这种额外检查的代价是运行时间更长。


### 基于范围的for循环

C++新增的一种循环</br>
简化了一种任务：对数组（或容器类，如vector和array）的每个元素执行相同的操作

```c++
double prives[5] = {4.99, 10.99, 6.87, 7.99, 8.49};
for (double x : prices)
    cout << x << std::endl;

//要修改数组元素，需要使用不同的循环变量语法
for (double &x : prices)
    x = x*0.80;
//符号&表面x是一个引用变量

//还可结合使用基于范围的for循环和初始化列表
for (int x : {3, 5, 2, 8, 6})
    cout << x << " ";
cout << '\n';
```


### 文件

##### 检测文件尾(EOF)

检测到EOF后，cin将两位（eofbit和failbit）都设置为1。可以通过成员函数eof()来查看eofbit是否被设置；如果检测到EOF，则cin.eof()将返回bool值true，否则返回false。同样，如果eofbit或failbit被设置为1，则fail()成员函数返回true，否则返回false。</br>
注意，eof()和fail()方法报告最近读取的结果；也就是说，它们在事后报告，而不是预先报告。因此应将cin.eof()或cin.fail()测试放在读取后。

设置标记后，cin将不读取输入，再次调用cin也不管用</br>
**cin.clear()方法**</br>
清除EOF标记，使输入继续进行

```c++
//直到遇到EOF的输入循环
cin.get(ch);
while (cin.fail() == false)
{
    ...
    cin.get(ch);
}

//while(!cin.fail())

//while (cin)
//这比!cin.fail()或!cin.eof()更通用
//因为它可以检测到其他失败原因，如磁盘故障

//由于cin.get(char)的返回值为cin，因此可以精简成
while (cin.get(ch))
{...}
```

<font color=gray size=1>方法cin.get(char)的返回值是一个cin对象。然而，istream类提供了一个可以将istream对象（如cin）转换为bool值的函数；当cin出现在需要bool值的地方时，该转换函数将被调用。另外，如果最后一次读取成功了，则转换得到的bool值为true；否则为false。</font>

#### 写入到文本文件中

*将cout用于控制台输出*

- 必须包含头文件iostream。
- 头文件iostream定义了一个用处理输出的ostream类。
- 头文件iostream声明了一个名为cout的ostream变量（对象）。
- 必须指明名称空间std。
- 可以结合使用cout和运算符<<来显示各种类型的数据。

*文件输出与此极其相似*

- 必须包含++头文件fstream++。
- 头文件fstream定义了一个用于处理输出的ofstream类。
- 需要++声明一个或多个ofstream变量++（对象），并以自己喜欢的方式对其进行命名，条件是遵守常用的命名规则。
- 必须指明名称空间std。
- 需要++将ofstream对象与文件关联起来++。为此方法之一是使用++open()方法++。
- 使用完文件后，应使用++方法close()++将其关闭。
- 可结合使用ofstream对象和运算符<<来输出各种类型的数据。

```c++
//声明对象
ofstream outFile;
ofstream fout;
//将这种对象与特定的文件关联起来
outFile.open("fish.txt");
char filename[50];
cin >> filename;
fout.open(filename);
```

方法open()接受一个C-风格字符串作为参数，可以是一个字面字符串，可以是存储在数组中的字符串</br>
程序运行之前文件并不存在，方法open()将新建一个对应名称的文件</br>
若运行程序之前文件存在，默认情况下，open()将首先截断该文件，即将其长度截短到零——丢失其原有内容，然后将新的输出加入到该文件中

```c++
//如何使用这种对象
double wt = 125.8;
outFile << wt;
char line[81] = "Objects are closer than they appear.";
fout << line << endl;
//outFile将cout显示到屏幕上的内容写入到了文件中

//程序使用完该文件后，应该将其关闭
outFile.close();
//如果忘记关闭文件，程序正常终止时将自动关闭它。
```

声明一个ofstream对象并将其同文件关联起来后，便可以像使用cout那样使用它。</br>
用于cout的操作和方法都可用于ofstream对象。

**总之，使用文件输出的主要步骤如下**
1. 包含头文件fstream。
2. 创建一个ofstream对象。
3. 将该ofstream对象同一个文件关联起来。
4. 就像使用cout那样使用该ofstream对象。


### 文本文件输入

*cin用于控制台*

- 必须包含头文件iostream。
- 头文件iostream定义了一个用处理输入的istream类。
- 头文件iostream声明了一个名为cin的istream变量（对象）。
- 必须指明名称空间std。
- 可以结合使用cin和运算符>>来读取各种类型的数据。
- 可以使用cin和get()方法来读取一个字符，使用cin和getline()来读取一行字符。
- 可以结合使用cin和eof()、fail()方法来判断输入是否成功。
- 对象cin本身被用作测试条件时，如果最后一个读取操作成功，它将被转换为布尔值true，否则被转换为false。

*文件输入与此极其相似*

- 必须包含++头文件fstream++。
- 头文件fstream定义了一个用于处理输入的++ifstream类++。
- 需要++声明一个或多个ifstream变量（对象）++，并以自己喜欢的方式对其进行命名，条件是遵守常用的命名规则。
- 必须指明名称空间std。
- 需要++将ifstream对象与文件关联起来++。方法之一是使用++open()方法++。
- 使用完文件后，应使用++close()方法++将其关闭。
- 可++结合使用ifstream对象和运算符>>来读取各种类型的数据++。
- 可以++使用ifstream对象个get()方法来读取一个字符，使用ifstream对象和getline()来读取一行字符++。
- 可以结合使用ifstream和eof()、fail()等方法来判断输入是否成功。
- ifstream对象本身被用作测试条件时，如果最后一个读取操作成功，它将被转换为布尔值true，否则被转换为false。

```c++
//声明对象
ifstream inFile;
ifstream fin;
//将这种对象与特定文件关联
inFile.open("bowling.txt");
char filename[50];
cin >> filename;
fin.open(filename);
```
cin的操作和方法都可用于ifstream对象

如果试图打开一个不存在的文件用于输入，将导致后面使用ifstream对象进行输入时失败。检查文件是否被成功打开的首先方法是使用方法is_open()

```c++
inFile.open("bowling.txt");
if (!inFile.is_open())
{
    exit(EXIT_FAILURE);
}
//如果文件被成功打开，方法is_open()将返回true。
//函数exit()的原型在头文件cstdlib中定义，用于终止程序。
//同时还定义了一个同操作系统通信的参数值EXIT_FAILURE。

//若编译器不支持is_open()，可以用较老的方法good()
```

程序还必须能够找到这个文件。通常，++除非在输入的文件名中包含路径，否则程序将在可执行文件所属的文件夹中查找。++

##### 检查文件是否被成功打开至关重要

文件读取循环

1. 程序读取文件时不应超过EOF。如果最后一次读取数据时遇到EOF，方法eof()将返回true。程序可能遇到类型不匹配的情况。
2. 如果最后一次读取操作中发生了类型不匹配的情况，方法fail()将返回true（遇到EOF也将返回true）。
3. 可能出现意外问题，如文件受损或硬件故障。如果最后一次读取文件时发生了这样的问题，方法bad()将返回true。
4. 不要分别检查这些情况。一种更简单的方法是使用good()方法，在没有发生任何错误时返回true。

```c++
while (inFile.good())
{
    ...
}

//其他方法
if (inFile.eof())
    cout << "End of file reached.\n";
else if (inFile.fail())
    cout << "Input terminated by data mismatch.\n";
else
    cout << "Input terminated for unknown reason.\n";
//判断循环为何终止
```


### 内联函数

为了提高程序运行速度(c++)

主要区别：在于c++编译器如何将它们组合到程序

<font color=gray size=1>常规函数调用使程序跳到另一个地址（函数的地址），并在函数结束时返回。</br>
执行到函数调用指令时，程序将在函数调用后立即存储该指令的内存地址，并将函数参数复制到堆栈（为此保留的内存块），跳到标记函数起点的内存单元，执行函数代码（也许还需将返回值放入到寄存器中），然后跳回到地址被保存的指令处。来回跳跃并记录跳跃位置意味着以前使用函数时，需要一定的开销。</font>

编译器将++使用相应的函数代码替换函数调用++。对于内联代码，程序无需跳到另一个位置处执行代码，再跳回来。因此，++内联函数的运行速度比常规函数稍快，但代价是需要占用更多内存++。

<font color=gray size=1>应有选择地使用内联函数。如果执行函数代码的时间比处理函数调用机制的时间长，则节省的时间将只占整个过程的很小一部分。如果代码执行之间很短，则内联调用就可以节省非内联调用使用的大部分时间。另一方面，由于这个过程相当快，因此籍贯节省了该过程的大部分时间，但节省的时间绝对值并不大。</font>

除非该函数经常被调用。

要使用这项特性，必须采取下述措施之一：
- 在**函数声明**前加上**关键字inline**；
- 在**函数定义**前加上**关键字inline**。

通常的做法是**省略原型，将整个定义（即函数头和所有函数代码）放在本应提供原型的地方。**</br>
程序员请求将函数作为内联函数时，++编译器并不一定会满足这种要求++。它可能认为该++函数过大++或注意到函数调用了自己（++内联函数不能递归++）。因此不将其作为内联函数；而有些编译器没有启用或实现这种特性。

<font color=gray size=1>inline工具是c++新增的特性。C语言使用预处理器语句#define来提供宏——内联代码的原始实现。</font>


### 引用变量

c++新增了一种复合类型——引用变量。</br>
引用是已定义的变量的别名。

```c++
//c++给&符号赋予了另一个含义，将其用来声明引用
int rats;
int & rodents = rats;
//int&指的是指向int的引用
//上述引用声明允许将rats和rodents互换——它们指向相同的值和内存单元。
```

必须在声明引用时将其初始化，而不能像指针那样先声明再赋值。</br>
引用更接近const指针。

```c++
int & rodents = rats;
//实际上是下述代码的伪装表示
int * const pr = &rats;
```

引用经常被用作函数参数，++使得函数中的变量名成为调用程序中的变量的别名++。</br>
这种传递参数的方式叫做**按引用传递**。</br>
按引用传递++允许被调用的函数能够访问调用函数中的变量++。

<font color=gray size=1>如果程序员的意图是让函数使用传递给它的信息，而不对这些信息进行修改，同时又想使用引用，则应使用常量引用。
```c++
//应在函数原型和函数头中使用const
double refcube(const double &ra);
//当编译器发现代码修改了ra的值时，将生成错误信息。
```
传递引用的限制更严格。</br>
如果ra是一个变量的别名，则实参应是该变量。
```c++
double z=refcube(x+3.0);
//代码不合理，因为表达式x+3.0并不是变量
//报错或警告
//早期允许是因为创建了临时变量，调用后删除
```
</font>

##### 应尽可能使用const

将引用参数声明为常量数据的引用的理由：
- 使用const可以避免无意中修改数据的编程错误
- 使用const使函数能够处理const和非const实参，否则将只能接受非const数据
- 使用const引用使函数能够正确生成并使用临时变量

##### 使用const引用参数

与复制原始结构的拷贝相比，使用引用可节省时间和内存

返回引用时最重要的一点是，应避免返回函数终止时不再存在的内存单元引用

![12](https://github.com/HaloAncy/Some-notes/blob/master/cpp/picture/12.png)


### 对象 继承 引用

ofstream对象可以使用ostream类的方法</br>
这使得文件输入/输出的格式与控制台输入/输出相同</br>
使得能够将特性从一个类传递到另一个类的语言特性被称为**继承**

ostream是基类</br>
ofstream是派生类</br>
派生类继承了基类的方法

继承的另一个特征 - 基类引用可以指向派生类对象，而无需进行强制类型转换

![13](https://github.com/HaloAncy/Some-notes/blob/master/cpp/picture/13.jpg)

格式化</br>
![14](https://github.com/HaloAncy/Some-notes/blob/master/cpp/picture/14.png)


### 默认参数

指的是当函数中省略了实参时自动使用的一个值

设置默认值——通过函数原型

将值赋给原型中的参数</br>
![15](https://github.com/HaloAncy/Some-notes/blob/master/cpp/picture/15.jpg)


### 函数重载

默认参数 - 能够使用不同数目的参数调用同一个函数</br>
函数多态（函数重载）- 能够使用多个同名的函数

函数重载的关键是**函数的参数列表**——**函数特征标**。如果两个**函数的参数数目和类型**相同，同时**参数的排列顺序**也相同，则它们的特征标相同，而变量名是无关紧要的。++C\+\+允许定义名称相同的函数，条件是它们的特征标不同++。如果参数数目和/或参数类型不同，则特征标也不同。

![16](https://github.com/HaloAncy/Some-notes/blob/master/cpp/picture/16.jpg)

编译器在检查函数特征标时，将把类型引用和类型本身视为用一个特征标。</br>
匹配函数时，并不区分const和非const常量。

![17](https://github.com/HaloAncy/Some-notes/blob/master/cpp/picture/17.jpg)

![18](https://github.com/HaloAncy/Some-notes/blob/master/cpp/picture/18.png)</br>
![19](https://github.com/HaloAncy/Some-notes/blob/master/cpp/picture/19.jpg)

函数基本上执行相同的任务，但使用不同形式的数据时，应采用函数重载。

C++如何跟踪每一个重载函数：</br>
使用C++开发工具中的编辑器编写和编译程序时，C++编译器将执行一些操作——名称修饰或名称矫正，它根据函数原型中指定的形参类型对每个函数名进行加密。


### 函数模板

函数模板是通用的函数描述，它们使用泛型来定义函数，其中的泛型可用具体的类型（如int或double）替换。</br>++通过将类型作为参数传递给模板，可使编译器生成该类型的函数。++</br>
由于模板允许以泛型的方式编写程序，因此有时也被称为通用编程。由于类型是用参数表示的，因此模板特性有时也被称为参数化类型。

```c++
//第一行指出要建立一个模板，并将类型命名为AnyType。
template <typename AnyType>
void Swap(AnyType &a, AnyType &b)
{
    AnyType temp;
    temp=a;
    a=b;
    b=temp;
}
```

关键字template和typename是必需的，除非可以使用关键字class代替typename。必须使用尖括号。类型名可以任意选择。</br>
++模板并不创建任何函数，而只是告诉编译器如何定义函数++。需要交换int的函数时，编译器将按模板模式创建这样的函数，并用int代替AnyType。

在文件的开始位置提供模板函数的原型，并在main()后面提供模板函数的定义。

函数模板不能缩短可执行程序。

更常见的情形：将模板放在头文件中，并在需要使用模板的文件中包含头文件。

可以像重载常规函数定义那样重载模板定义。和常规重载一样，被重载的模板的函数特征标必须不同。</br>
并非所有的模板参数都必须是模板参数类型。

```c++
template <typename T>
void Swap(T &a, T &b);

template <typename T>
void Swap(T *a, T *b, int n);
```


### 显示具体化

当编译器找到与函数调用匹配的具体化定义时，将使用该定义，而不再寻找模板。

![20](https://github.com/HaloAncy/Some-notes/blob/master/cpp/picture/20.png)

```c++
//下面是用于交换job结构的非模板函数、模板函数和具体化的原型
void Swap(job &, job &);

template <typename T>
void Swap(T &, T &);

template <> void Swap<job>(job &, job &);
//Swap<job>中的<job>可选
//因为函数的参数类型表明，这是job的一个具体化
```

编译器使用模板为特定类型生成函数定义时。得到的是模板实例。</br>
模板并非函数定义，但使用int的模板实例是函数定义。这种实例化方式被称为隐式实例化。

**显示实例化** - 直接命令编译器创建特定的实例</br>
声明所需的种类——用<>符号指示类型，并在声明前加上关键字template

```c++
template void Swap<int>(int, int);
//编译器将使用Swap()模板生成一个使用int类型的实例
```

区别上，显式具体化在于，不要使用Swap()模板来生成函数定义，而应使用专门为int类型显式地定义的函数定义。这些原型必须有自己的函数定义。