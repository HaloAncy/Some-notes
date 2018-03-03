### String类

用string类型的变量（对象）存储字符串</br>
提供了将字符串作为一种数据类型的表示方法</br>
**头文件string**</br>
string类位于名称空间std中

- 可以使用C-风格字符串来初始化string对象
- 可以使用cin来将键盘输入存储到string对象中
- 可以使用cout来显示string对象
- 可以使用数组表示法来访问存储在string对象中的字符

类设计让程序能够自动处理string的大小。

可以将char数组视为一组用于存储一个字符串的char存储单元，而string类变量是一个表示字符串的实体。


![3](https://github.com/HaloAncy/HelloHalo/blob/master/3.jpg)


### 字符流

**头文件<sstream>**

使用**stringstream对象**简化类型转换</br>
<sstream>库中声明的标准类就利用了这一点，自动选择所必需的转换。而且，转换结果保存在stringstream对象的内部缓冲中。你不必担心缓冲区溢出，因为这些对象会根据需要自动分配存储空间。

<sstream>库定义了三种类：istringstream、ostringstream和stringstream，分别用来进行留的输入、输出和**输入输出**操作。</br>
<sstream>使用****string对象来代替字符数组****。这样可以避免缓冲区溢出的危险。而且，传入参数和目标对象的类型被自动推导出来，即使使用了不正确的格式化符也没有危险。

![9](https://github.com/HaloAncy/HelloHalo/blob/master/9.png)


### 字符操作

##### string的子串

```c++
//返回pos开始的n个字符组成的字符串
string substr(int pos=0,int n=npos) cconst;

str.substr(startpos,length);
//startpos是起始字符的序号
//length是[从startpos开始]取的字符串长度(包括startpos)。

//如果要取得str中序号m到n之间(不包括n)的子字符串需要用
str.substr(m,n-m);
```

##### 确定字符是否为大写字母、数字、标点符号等

头文件cctype
```c++
//判断是否为数字
isdigit();
//判断是否为字母
isalpha();
```

##### string类的删除函数

```c++
//删除pos开始的n个字符，返回修改后的字符串
string &erase(int pos=0,int n=npos);
```

##### string类的查找函数

```c++
//从pos开始查找字符c在当前字符串的位置
int find(char c,int pos=0);
```

##### 获取字符串的长度

**length() size()**

![10](https://github.com/HaloAncy/HelloHalo/blob/master/10.png)

const char *c_str();

![11](https://github.com/HaloAncy/HelloHalo/blob/master/11.png)