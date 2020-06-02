# Java_Learning
Java基础   参考书籍---Java核心技术 卷1
@[TOC](Java基础板块--持续更新)
## 3.Java的基本程序设计结构
### 3.1一个简单的Java应用程序
下面是一个最简单的Java应用程序，它只发送一条消息到控制台中。
```java
public class example {
    public static void main(String[] args) {
        System.out.println("Hello Word");
    }
}

```
**要点**

 - Java区分大小写。
 - 关键字public成为访问修饰符，用于控制程序其他部分对这段代码的访问级别。
 - Java类名定义：必须以字母开头，后面可以跟字母和数字的任意组合。长度基本没有任何限制，但不能使用Java保留字。
 - Java类命名规范：以大写字母开头的名词。若由多个单词组成，每个单词首字母大写。（驼峰命名法 camel case）。
 - 源代码的文件名必须与公共类名字相同，并用.java作为扩展名。 Java中任何方法的代码都用 “{” 开始，用 “}” 结束。

### 3.2注释
**三种方式**

```java
//这是单行注释

/*
* 这是多行注释
*/

/**
* 这是多行注释，可用来自动生成文档
*/
```

### 3.3数据类型
#### 3.3.1整型
整型用于表示没有小数部分的数值，允许是负数。Java提供了4种类型：
|类型|存储空间  |取值范围
|--|--|--|
| int  | 4Byte |$$-2^{31} 到2^{31} - 1$$
|short|2Byte|$$-2^{16} 到 2^{16} - 1$$
| long|8Byte|$$-2^{64} 到 2^{64} - 1$$
| byte| 1Byte|$$-2^{8} 到 2^{8} - 1$$

 - 长整型数值有一个后缀L或l（例如40000000L或4000000l）。
 - 十六进制数值有一个前缀0x或0X（如0x18AE）
 - 从Java7开始，加上前缀0b或0B可以写二进制数（如0b11001）
 - 从Java7开始，还可以为数字字面量加下划线，如1_000_000或（0b1111_0100_0100_0100_0000）表示100万。这些下划线只是为了代码更加易读，Java编译器会去除下划线。

#### 3.3.2浮点类型
浮点类型用于表示有小数部分的数值。Java提供了2种类型：
|类型|存储空间  |取值范围
|--|--|--|
| float| 4Byte|大约正负3.402 823 47E+38F(有效位数为6~7位)
| double|8Byte |大约正负1.797 693 134 862 315 70E+308（有效位数为15位）

 - double的数值精度是float的两倍，实际上很少情况使用float。
 - float数值有一个后缀F或f（如3.14F），没有后缀F或f的浮点数值默认为double类型。
 - Java中的E/e表示10的幂次，(2E+3表示 2*10^3,2E-3 表示 2 * 10^-2)
 - 所有浮点数值计算都遵循IEEE 754规范。具体来说可用下面三个特殊数值表示溢出和出错的情况：
 1.正无穷大
 2.负无穷大
 3.NaN（不是一个数字）
 例如：一个整数除以0的结果为正无穷大，计算0/0或负数的平方根结果为NaN。
> **注释：**
> 常量Double.POSITIVE_INFINITY,Double.NEGATIVE_INFINITY,Double.NaN(以及对应的Float类型常量)分别表示这三个特殊值，但在实际中很少遇到。
> **特别说明：**
> 不能用 
> if (x == Double.NaN) //is never true
> 所有NaN都是不相同的。
> 可以使用
> if (Double.isNaN(x)) //check x is NaN

**警告：**
浮点数值不适用与无法接受舍入误差的金融计算。如 2.0-1.1 将为0.8999999999 而不是希望的0.9.原因是浮点数值用二进制系统表示，在二进制中无法精确表示分数1/10,应使用BigDecimal类。

#### 3.3.3char类型
char类型原本用于表示单个字符，如今有些Unicode字符可以用一个char值描述，另外一些Unicode字符则需要两个char字符。char类型字面量要用单引号括起来。
| 转义序列 |名称  |
|--|--|
|  \b| 退格 |
| \t|制表
| \n|换行
| \r|回车
| \\"|双引号
| \\'|单引号
| \\\ | 转义
#### 3.3.4Unicode和char类型
**码点：**指与一个编码表中的某个字符对应的代码值。
#### 3.3.5boolean类型
两个值：true和false。整形与布尔值之间不可相互转换。
### 3.4变量与常量
#### 3.4.1声明变量
先指定变量类型，然后是变量名。
如下：
```java
int a;
```
变量名必须是一个以字母开头并有字母和数字构成的序列。
**注意**
Java中的字母和数字范围更大。字母包括“A-Z”、“a-z”、“_”、“$”或在某种语言中表示字母的任何Unicode字符。

> **提示：**如果想要知道哪些Unicode字符属于Java中的“字母”，可以使用Character类的isJavaIdentifierStart和isJavaIdentifierPart方法来检查。
> **提示：**尽管$是一个合法的Java字符，但不要在你的代码中使用这个字符，它只用在Java编译器或其他工具生成的名字中。
#### 3.4.2变量初始化

 - 声明一个变量后必须用赋值语句对变量进行初始化。
 - Java可以将声明的代码放在任何地方。
 - 变量的声明尽量靠近变量第一次使用的地方，这是一种良好的编程习惯。

> **注释：**从Jav10开始，对于局部变量，如果可以从初始值推断出他的类型，就无须声明变量类型，只需要用关键字var。
#### 3.4.3常量
在Java中用关键字final指示常量。final表示这个变量只能被赋值一次，不能被修改。
#### 3.3.4枚举类型
定义：

```java
enum Size{SMALL, MEDIUM, LARGE};
Size s = Size.SMALL;
```
Size类型的变量只能为枚举中的值。
### 3.5运算符
#### 3.5.1算数运算符
\+ \- * / 表示加减乘除。%表示求余数。
#### 3.5.2数学函数和常量
Math类的常用函数：

```java
//算术计算
Math.sqrt() : //计算平方根
Math.cbrt() : //计算立方根
Math.pow(a, b) : //计算a的b次方
Math.max( a,b ) : //计算最大值
Math.min( a,b ) : //计算最小值
Math.abs() : //取绝对值
//进位运算
Math.ceil(): //天花板的意思，就是逢余进一
Math.floor() : //地板的意思，就是逢余舍一
Math.rint(): //四舍五入，返回double值。注意.5的时候会取偶数
Math.round(): //四舍五入，float时返回int值，double时返回long值
//随机数
Math.random(): //取得一个[0, 1)范围内的随机数
```
#### 3.5.3数值类型之间的转换
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200527113409381.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMjAyNTM5,size_16,color_FFFFFF,t_70)
图中的实线箭头表示无信息丢失的转换。虚线箭头表示可能有精度损失的转换。
当用一个二元运算符连接两个值时（例如a + b ，a为整形，b为浮点型），先要将两个操作数转换为同一种类型然后计算。转换顺序如下：

 - 如果两个数其中有一个数是double，另一个操作数会转为double；
 - 否则，其中一个是float，另一个转为float；
 - 否则，其中一个是long，另一个转为long；
 - 否则，两个操作数都被转为int。
#### 3.5.4强制类型转换
语法格式：

```java
double x = 9.997;
int a = (int) x;
```
> **警告：**在强制转换时，如果超出了目标类型的表示范围，结果就会截断成一个完全不同的值。如：（byte）300 的实际值是44. 

#### 3.5.5结合赋值和运算符
```java
x += 4;
//等价于
x = x + 4;
```
一般来说，要把运算符放在=左边，如*=，+=，-=等。

> **注释：** 
> int x=0;
> x += 3.5;
> 会发生强制类型转换，把x设置为（int）（x+3.5）
#### 3.5.6自增和自减运算符
++，--。
要注意自增或自减出现的位置
```java
int m = 7;
int n = 7;
int a = 2 * ++m; //now, a is 16,m is 8
int b = 2 * n++; //now b is 14,n is 8
```
建议不要在表达式中使用++，这样的代码容易让人困惑，产生bug。
#### 3.5.7关系和boolean运算符
关系：==、！=、<、>、<=、>=
逻辑：&&-与、||-或。
> **注释：**&&和||是按照“短路”的方法来求值的，如果第一个操作数已经能够确定表达式的值，第二个操作数就不必计算。

Java支持三元运算符 ？：

```java
a>0 ? a : 0;//如果a大于0，则a=a；否则，a=0；
```
#### 3.5.8位运算符
& 按位与
| 按位或
^ 异或
~ 非

> **注释：**&和|应用在布尔值上，结果也是布尔值。不过&和|不采用短路运算。

<<      :     左移运算符，num << 1,相当于num乘以2

\>>      :     右移运算符，num >> 1,相当于num除以2

\>>>    :     无符号右移，忽略符号位，空位都以0补齐

#### 3.5.9运算符优先级
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200527120425160.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMjAyNTM5,size_16,color_FFFFFF,t_70)
### 3.6字符串
从概念上讲，Java字符串就是Unicode字符序列。
#### 3.6.1子串

```java
String s = "Hello";
s.subString(0,2); //He
```
subString方法的第二个参数是不想复制的第一个位置。s.subString(a,b)子串长度为b-a。
#### 3.6.2拼接

```java
String s1 = "Hel";
String s2 = "lo";
s1 + s2; //"Hell0"
s1.concat(s2); //"hello"

//静态方法join，把对个字符串放在一起，用一个定界符分隔。
String all = String.join("/","s","m","L") //all = "s/m/l";

//在Java11中，提供了repeat方法。
String repeated = "Java".repeat(3); //"JavaJavaJava"
```
#### 3.6.3不可变性
String类对象不可变。
原因：底层是用final修饰的char数组保存。
#### 3.6.4检测字符串是否相等
使用equals方法。
**注意**一定不要使用==检测字符串是否相等。这只能检测两个字符串是否放在同一位置上。
#### 3.6.5空串和Null串
空串“”是长度为0的字符串。空串是一个Java对象。有自己的串长度和内容。
检测空串：

```java
if(s.equals("")){}
if(s.length() == 0){}
```
Null串检测：

```java
if(s == null){}
```
检测不是空串也不是null串：

```java
if(s.length() != 0 && s != null){}
```
#### 3.6.6String API
p49~p51
#### 3.6.7构建字符串

```java
	StringBuilder builder = new StringBuilder();
    builder.append(s1);
    builder.append(s2);
    builder.toString();
```
StringBuilder API：p54~p55
### 3.7输入与输出
#### 3.7.1读取输入

```java
Scanner in = new Scanner(System.in);
```
Scanner API:
p56~p57。
#### 3.7.2格式化输出

```java
System.out.printf("hello,%s",name);
```
每一个以%字符开始的格式说明符都用相应的参数替换。f表示浮点数，s表示字符串，d表示十进制数。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200527144827618.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMjAyNTM5,size_16,color_FFFFFF,t_70)
 #### 3.7.3文件输入与输出
 

```java
//读文件
Scanner in = new Scanner(Path.of("myfile.txt"),StandardCharsets.UTF_8);

//写文件
PrintWriter out = new PrintWriter("myfile.txt",StandardCharsets.UTF_8);
```
### 3.8控制流程
与其他程序设计语言一样，Java使用条件语句和循环语句确定控制流程。
#### 3.8.1块作用域
块是指由若干Java语句组成的语句，并用一对大括号括起来。块确定了变量的作用域。一个块可以嵌套另一个快。
**注意**：不能在嵌套的两个块中声明同名的变量。
#### 3.8.2条件语句

```java
if(){}else{}
```
#### 3.8.3循环语句

```java
while(){}

do{}while()

for(){}

switch(){
	case:
}
```
#### 3.8.6中断控制流程的语句
break；//跳出当前循环
continue;//中断当前循环，跳入下一步骤。
带标签的break语句：

```java
read_data:
while(){
	for(){
		if(){
			break read_data;	
		}
	}
}
```
执行break，直接跳出while循环。
### 3.9大数
#### 3.9.1BigInteger
实现任意精度的整数运算。
#### 3.9.2BigDecimal
实现任意精度的浮点数运算。
[https://blog.csdn.net/qq_41202539/article/details/106150338](https://blog.csdn.net/qq_41202539/article/details/106150338)
### 3.10数组
#### 3.10.1数组声明

```java
int[] a;

int[] a = new int[100];

int[] a = {1,2,3,4};
```
#### 3.10.2访问数组元素

```java
int[] a = {1,2,3,4};
a[0];
```
创建一个数字数组时，所有元素初始化为0.boolean数组，初始化为false。对象数组初始化为null。
#### 3.10.3for each循环

```java
int b[] = {1,0,3}
for(int a : b){
System.out.print(a);
}
```
还可以利用Arrays.toString()打印数组：

```java
int a = {0,1,2};
System.out.print(Arrays.toString(a));//[0,1,2]
```
#### 3.10.4数组拷贝

```java
int[] a = {0,1,2,3,4};
int[] b = Arrays.copyOf(a,a.length);
```
第二个参数是新数组的长度，通常用这个函数实现数组扩容。
#### 3.10.6数组排序

```java
int[] a = {0,1,2,3,4};
Arrays.sort(a);
```
这个方法使用了优先快速排序的方法。
Arrays API p85

## 4.对象和类
### 4.1面向对象程序设计概述
#### 4.1.1类
类是构造对象的蓝图或模板。由类构造对象的过程称为创建类的实例。
**封装**就是将数据和行为组合在一个包中，并对对象的使用者隐藏具体的实现方式。对象中的数据称为**实例字段**，操作数据的过程称为**方法**。作为一个类的实例，特定对象都有一组特定的实例对象值，这些值得集合就是当前对象的**状态**。
实现封装的关键在于，决不能让类中的方法直接访问其他类的实例字段。程序只能通过对象的方法与对象数据进行交互。
在Java中所有类都拓展自Object类。在拓展一个已有类是，拓展后的新类会拥有被拓展的类的所有属性和方法。
#### 4.1.2对象
对象的三个主要特性：

 - 对象的行为
 - 对象的状态
 - 对象的标识--每个对象都有一个唯一的标识符。
#### 4.1.4类之间的关系
 - 依赖 - 即“uses-a”关系
 - 聚合 - 即“has-a”关系
 - 继承 - 即“is - a”关系
### 4.2使用预定类
#### 4.2.1对象与对象变量
在Java中要使用构造器构造新实例。构造器是一种特殊的方法，用来构造并初始化对象。
对象变量并没有实际包含一个对象，他只是引用一个对象。在Java中，任何对象变量的值都是存储在另一个地方的某个对象的引用。new操作符的返回值也是一个引用。
#### 4.2.2LocalDate类
API p103
#### 4.2.3更改器和访问器方法
更改器方法：更改对象的状态（Setter是一个更改器方法）
访问器方法：只访问对象而不修改对象的方法。（Getter是一个访问器方法）

> **注意**不要编写返回可变对象引用的访问器方法。
> 如果需要返回一个可变对象的引用，首先应该对他进行克隆。

### 4.3用户自定义类
**构造器：**
 - 与类名同名
 - 每个类可以有一个以上的构造器
 - 构造器可以有0个、1个或多个参数
 - 构造器没有返回值
 - 构造器总是伴随着new操作符一起使用。
**注意**：不要在构造器中定义与实例字段同名的局部变量。

**var关键字：**
 - 只能在局部变量中使用
 - 不对数值类型使用，如int、long或double，这样就不用担心0,0L，0.0之间的区别。

**使用null引用：**
对于构造器中传入的参数如果为null，在Java9中提供了两种解决办法：
**宽容型：**
```java
public Employee(String n){
	//将null引用替换为unkown
	this.name = Object.requireNonNullElse(n,"unkown");
}
```
**严格型：**
```java
public Employee(String n){
	//抛出空指针异常
	this.name = Object.requireNonNull(n,"the name can not be null");
}
```

> **注释：**当构造器不希望接受可有可无的值时，用严格型更加合适。

**隐式参数和显示参数**

```java
Employee employee = new Employee();
employee.setName(name);
```
在setName方法中有两个参数，第一个为在方法之前的employee对象为隐式参数，括号中的name为显示参数。
在每一个方法中，关键字this指示隐式参数。

**final实例字段**
定义为final的字段必须初始化，相当于一个常量。
### 4.4静态字段和静态方法
#### 4.4.1静态字段
一个字段定义为static，那么他就是静态字段。他属于类而不属于实例。调用方式为 类名.字段名。
#### 4.4.2 静态常量

```java
public class Math{
	*************
	public static final double PI = 3.1419926535897932386;
	*************
}
```
前面提过，由于每个对象都可以修改公共字段，所以最好不要有公共字段。然后，公共常量是没有问题的。因为被声明为final，所以不可被修改。
#### 4.4.3静态方法
可以认为静态方法时没有this参数的方法。静态方法只可以访问静态字段，不能访问实例字段。
建议使用类名而不是实例名来调用静态方法。
以下两种情况可以使用静态方法：

 - 方法不需要访问对象的状态，因为他所需要的参数都是通过显示参数提供。
 - 方法只需要访问静态字段。
#### 4.4.4工厂方法
#### 4.4.5main方法
在启动程序时还没有任何对象。静态的main方法将执行并构造所需要的对象。
Object API：p120
### 4.5方法参数
 - 按值调用：表示方法接受的是调用者提供的值
 - 按引用调用：表示方法接受的是调用者提供的变量地址。
 **方法可以修改按引用调用传递的变量的值，而不能修改按值传递的变量的值。**
 **Java采用的是按值传递**
 
方法的参数有两种：
 - 基本数据类型
 - 对象引用

**用例：**
**传入基本数据类型**
 

```java
int a = 10;
int b = 20;

public void swap(int x, int y){
	int temp;
	temp = x;
	x = y;
	y = temp;
	Sys.out.print("x="+x+"y="+y);
}

//调用
swap(a,b);//结果是x=20,y=10,但是a=10，b=20；
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200528121817477.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMjAyNTM5,size_16,color_FFFFFF,t_70)
**传入引用类型**

```java
public void changeName(Employee e){
	e.setName("MyName");
}

Employee employee = new Employee("Luo");

changeName(employee);//此时employee.getName = "MyName"
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200528122421787.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMjAyNTM5,size_16,color_FFFFFF,t_70)
employee和e指向同一个对象。

**可以看出Java采用的是按值传递的例子：**

```java
Employee e1= new Employee("Luo");
Employee e2= new Employee("Wang");

public void swap(Employee x,Employee y){
	Employee temp;
	temp = x;
	x = y;
	y = temp;
}

swap(e1.e2);//此时e1.getName="Luo",e2.getName="Wang"
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200528143558615.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMjAyNTM5,size_16,color_FFFFFF,t_70)
图中虚线为调用swap方法之前x，y的指向，实现为调用后的指向。
这个例子可以很好的说明Java是按值传递的。
### 4.6对象构造
#### 4.6.1重载
**重载：**多个方法有着相同的名字，不同的参数。Overload
Java允许重载任何方法。因此要完整的描述一个方法，必须制定方法的方法名和参数。这叫方法的签名。
#### 4.6.2默认字段初始化
如果在构造器中没有显示的为字段设置初值，就会设置默认值：数值为0，布尔为false，对象引用为null。

> **注释：**局部变量必须初始化，这是字段和局部变量的一个重要区别。
#### 4.6.3无参构造器
使用无参构造器时，对象的状态会设置为合适的默认值。
如果一个类没有编写构造器，系统会为你提供一个无参构造器，并把所有实例字段设置成默认值。
如果类中提供了至少一个构造器，而没有提供无参构造器，那么调用无参构造器就是非法的。
#### 4.6.6调用另一个构造器

```java
public Employee(String name， double salary){
	this.name = name;
	this.salary = salary;
}

public Employee(String name， double salary, int id){
	//调用了Employee(String name， double salary)构造器
	this(name,salary);
	this.id = id;
}

```
#### 4.6.7调用构造器的具体处理步骤

 1. 如果构造器第一行调用了另一个构造器，则基于所提供的的参数执行第二个构造器。
 2. 否则：
 a）所有数据字段初始化为默认值（0，false，null）
 b）按照类声明中出现的顺序，执行所有字段初始化方法和初始化块
 3. 执行构造器主体代码。

### 4.7包
使用包的主要原因是为了确定类名的唯一性。
包名一般为因特网域名的倒叙：com.baidu；
使用import导入包。
### 4.10类设计技巧

 1. 一定保证数据私有，不破坏封装性
 2. 一定要对数据进行初始化。
 3. 不要在类中使用过多的基本类型
 4. 不是所有字段都需要单独的字段访问器和字段更改器。
 5. 分解有过都职责的类
 6. 类名和方法名都要能体现他们的职责。
 7. 优先使用不可变的类。
## 5.继承
### 5.1类、超类、子类
#### 5.1.1定义子类
使用关键字**extends**定义子类

```java
public class Manger extends Employee{
}
```
子类拥有超类的所有属性和方法，所以定义子类时，只需要指出子类和超类的不同之处。
#### 5.1.2覆盖方法
假如子类要覆盖父类中的方法，子类中可用super关键字调用父类的同名方法。

```java
public class Manger extends Employee{
	private double bonus;
	public double getSalary(){
		duoble baseSalary = super.getSalary;
		return bonus + baseSalary;
	}	
}
```

> **注释：**子类中可以添加字段、添加方法、覆盖方法，但是决不允许删除任何字段或方法。
#### 5.1.3子类构造器

```java
public Manger(String name, double Salary, int year){
	super(name,Salary, yaer);
	bonus = 0;
}
```
用super关键字调用父类中的构造器，接下来在进行子类属性的初始化。

> **注意：**如果子类中没有显示的调用父类的构造器，将自动调用父类的无参构造器。如果父类中没有无参构造器，并且子类中又没有显示的调用父类的其他构造器，Java编译器就会报错。
#### 5.1.5多态
一个对象变量可以指向多种实际类型的现象称为**多态**。在运行时能够自动选择适当的方法，称为**动态绑定**。

```java
Employee e；
e = new Employee（）;
e = new Manager();
```
e既可以指向Employee，也可以指向Manager。

```java
Manager boss = new Manager();
Employee[] staff = new Employee[3];
staff[0] = boss;
```
staff[0]和boss指向同一个对象，但是编译器只把staff[0]看出是Employee对象。这就意味着：

```java
boss.setBonus(5000); //ok
staff[0].setBonus(5000); //error
```
因为staff[0]是Emloyee对象，employee对象没有setBonus方法。
**但是，不能讲超类赋值给子类。**

#### 5.1.6方法调用详细过程

 1. 编译器查看对象说明的声明类型C和方法名t。需要注意的是可能存在多个同名但是参数不一样的方法。编译器会一一列举出C类的所有名为t的方法和其父类中名为t而且可访问的方法。
 2. 编译器要确定方法中要调用的参数类型。在所有名为t的方法中找到与之匹配的方法，这个过程称为**重载解析**。至此，编译器已经知道方法名和参数类型。
 3. 如果是private、static、final方法或者构造器，那么编译器就可以准确的知道应该调用哪个方法。这成为**静态绑定**。与此对应的是，如果要调用的方法依赖于隐式参数的实际类型，就必须在运行时使用**动态绑定**。
 4. 如果使用动态绑定，，虚拟机必须调用与x所引用对象的实际类型对应的那个方法。假设x实际类型是D,他是C的子类。如果D定义了t方法，就调用差个方法。否则，在D类的父类中寻找这个方法。

> 虚拟机会预先为每个类计算一个方法表，其中列出了所有方法的签名和要调用的实际方法。将在方法表中进行搜索。
#### 5.1.7阻止继承：final类和方法
用final修饰的类不可继承，类中的所有方法也被隐式的修饰词final，而不包括字段。
用final修饰的方法不可重写。
#### 5.1.8强制类型转换
将子类引用赋值给父类是允许的不需要强制类型转换。

```java
Manager boss = new Manager();
Employee e = boss;//ok
```
将父类引用赋值给子类是允许的需要强制类型转换。
```java
Employee e = new Employee（）;
if(e instanceof Manager){
	Manager boss = (Manager) e;
}
```
综上：

 - 只能在继承层次中进行强制类型转换
 - 将超类强制转为子类之前，使用instanceof检查。
#### 5.1.9抽象类
使用abstarct修饰的类，为抽象类。
抽象类除了包含抽象方法之外，还可以包含字段和具体方法。

```java
public abstract class Person {
    private String name;

    public Person(String name) {
        this.name = name;
    }
    
    public abstract String getDescription();

    public String getName() {
        return name;
    }
}

```
#### 5.1.10受保护访问
protected声明的字段和方法只允许子类和本包中的类访问。
### 5.2Object类：所有类的超类
在Java中只有基本数据类型不是对象。
#### **equals方法：**
Object类的默认实现实判断两个对象的引用是否相等。
该方法具有的特性：

 - 自反性。x.equals(x)永远为true
 - 对称性。y.equals(x)和x.equals(y) 的结果都是一样的。
 - 传递性。x.equals(y),y.equals(z) --> x.equals(z)为true
 - 一致性。x和y的引用没有发生改变，反复调用x.equals(y)结果都一样。
 - 对于任何非空引用x,x.equals(null) 返回false。

编写一个完美的equals方法：

 1. 显示参数命名为otherObject，稍后强制类型转换。
 2. 检测this与otherObject是否相等
```java
if（this == otherObject） return true；
```
 3. 检测otherObject知否为null，如果为null，返回false。
```java
if（otherObject == null） return false；
```
 4. 比较this和otherObject的类，如果equals的语义可以在子类中改变，就是用getClass检测。如果所有子类的equals的语义都相同，则用instanceof检测： 
```java
if(this.getClass() != otherObject.getClass()) return false;
```
```java
if(!(otherObject instanceof ClassName)) return false;
```
 5. 将otherObject 强制类型转换。
```java
ClassName other = (ClassName) otherObject ;
```
 6. 根据相等性的概念要求比较字段。
#### hashCode方法
散列码（hash code）是对象导出的一个整型值。
如果像个对象相等，那么他们的hashCode一定相等。反之，不然。
**如果重新定义了equals方法，就必须为用户可能插入散列表的对象重新定义hashCode方法。**
理由：equals与hashCode的定义必须相容，如果x.equals(y)返回true，那么x.hashCode()和y.hashCode()必须相等。
#### toString方法
只要对象与另一个字符串通过 “+” 连接起来，Java编译器就会自动调用toString方法。
**强烈建议，给每个对象添加toString方法**
### 5.3泛型数组列表
ArrayList稍后详细介绍。
### 5.4对象包装器和自动装箱
[详见另一篇博客](https://blog.csdn.net/qq_41202539/article/details/105933642)
### 5.5参数数量可变的方法

```java
public PrintStream printf(String format, Object ... args) {
        return format(format, args);
    }
```
这里的 ... 省略号是Java代码的一部分，表明可以接受任意数量的对象。
实际上，printf方法接受两个参数，一个格式化字符串，一个Objec[]数组，其中保存所有其他参数（如果调用者提供的是基本数据类型，会进行自动装箱）。
### 5.6枚举类

```java

public enum Size {
    SMALL("s"),
    MEDIUM("m"),
    LARGE("l");

    private Size(String size) {
        this.size = size;
    }

    public String getSize() {
        return size;
    }

    private String size;
}

```
如上，枚举定义的是一个类，他只有三个实例，不能构造新对象。
枚举的构造器总是private的，否则会报错。
所有枚举类型都是Enum的子类。

### 5.7反射*
能够分析类能力的程序成为反射。
反射可以用来：

 - 在运行时分析类能力
 - 在运行时检查对象
 - 实现泛型数组操作代码
 - 利用Method对象
#### 5.7.1Class类
在程序运行期间。Java运行时系统始终为所有对象维护一个**运行时类型标识**。这个信息会跟踪每个对象所属的类，虚拟机利用运行时类型信息选择要执行的正确方法。保存这些信息的类就是Class类。

虚拟机为每个类型管理一个唯一的Class对象，因此可以用 == 实现两个对象的比较。
**API：**
**获取一个类对应的Class类的方法**

 1. 使用Object.getClass ()方法----引用类型的对象的获取方式。如果我们已经拿到了一个对象，可以使用这个对象的 getClass 方法获得一个 Class 对象(不过这仅限于引用类型的对象)
 2. 使用类的class成员属性。如果我们当前没有某个类的对象，无法使用 getClass() 方法来获取Class对象，那还可以使用 类名.class 来获取 Class对象
 3. 使用Class类的forName("类完整路径")方法获取。如果我们有一个类的完整路径，就可以使用 Class.forName(“类完整的路径”) 来得到相应的 Class，这个方法只能用于引用类型，所谓类的完整路径是：包名.类名 例如：java.lang.String。

**返回Class类对应的实体类的相关的Class类的方法**

 1. 返回当前Class类对应的实体类的父类的Class类：
```java
public Class<? super T> getSuperclass()
```
 2. 返回类定义的公共的内部类,以及从父类、父接口那里继承来的内部类
```java
public Class<?>[] getClasses()
```
 3. 返回类中定义的公共、私有、保护的内部类
```java
public Class<?>[] getDeclaredClasses()
```
 4. 返回一个成员内部类/属性/方法/构造器所在的类的Class，这些方法是上面那两个方法的逆操作
```java
java.lang.reflect.Class.getDeclaringClass()    ;//返回一个成员内部类所在的类的Class
java.lang.reflect.Field.getDeclaringClass()      ;//返回一个字段所在的类的Class
java.lang.reflect.Method.getDeclaringClass()    ;//返回一个方法所在的类的Class
java.lang.reflect.Constructor.getDeclaringClass() ;//返回一个构造器所在的类的Class
```
 5. 获取Class对应类(或者接口)的修饰符：Class.getModifiers().Class.getModifiers() 获得调用类的修饰符的二进制值，然后使用 Modifier.toString(int modifiers) 将获取到的二进制值转换为字符串。
```java
public int getModifiers()；//返回此类或接口以整数编码的 Java 语言修饰符。
/**
修饰符由 Java 虚拟机的 public、protected、private、final、static、abstract 和 interface 对应的常量组成；
它们应当使用 Modifier 类的方法来解码。
*/
```
 6. 获取Class对应的类或者接口的成员Member(成员有：属性，方法,构造方法)
（1）获取构造函数
```java
Constructor<?>[] getDeclaredConstructors();//返回所有的构造方法的Constructor对象的数组的Constructor对象的数组
 Constructor<?>[] getConstructors();        //返回所有共有的构造方法的Constructor对象的数组
```
	(2)获取成员变量
```java
Field[] getFields() 
          返回此 Class 对象所表示的类或接口的所有公有字段数组(Field 对象数组)
Field[] getDeclaredFields() 
          返回此 Class 对象所表示的类或接口中所有声明的字段数组(Field对象数组)。 
```
	（3）获取成员方法
```java
 Method[] getMethods() 
          返回一个包含某些 Method 对象的数组，这些对象反映此 Class 对象所表示的类或接口
          （包括那些由该类或接口声明的以及从超类和超接口继承的那些的类或接口）的公共 member 方法 
 Method[] getDeclaredMethods() 
          返回 Method 对象的一个数组，这些对象反映此 Class 对象表示的类或接口声明的所有方法，
           包括公共、保护、默认（包）访问和私有方法，但不包括继承的方法。 
```
 
 7. 返回字符串(String)的方法
```java
 String getCanonicalName() 
          返回 Java Language Specification 中所定义的底层类的规范化名称。 
 String getName() 
          以 String 的形式返回此 Class 对象所表示的实体（类、接口、数组类、基本类型或 void）名称（全限定名：包名.类名）。
 String getSimpleName() 
          返回源代码中给出的底层类的简称。 
 String toString() 
          将对象转换为字符串。 
```
 8. 返回boolean的方法：
```java
boolean isLocalClass()     ;//判断是不是局部类，也就是方法里面的类 
boolean isMemberClass()    ;//判断是不是成员内部类，也就是一个类里面定义的类
boolean isAnonymousClass() ;//判断当前类是不是匿名类，匿名类一般用于实例化接口
```
#### 5.7.4利用反射分析类的能力
在java.lang.reflect包中有三个类Field、Method、Constructor分别用于描述类的字段、方法、构造器。
这三个类都有getName方法返回项目的名称

Field类的getType方法可返回描述域所属类型的Class对象

Method和Constructor类都有报告参数的方法，Method类还有报告返回类型的方法

这三个类还有getModifiers方法返回整数数值，用不同的位开关描述public和static这样的修饰符的使用状况。还可以使用java.lang.reflect.Modifier类的静态方法分析getModifiers返回的整数数值，如isPublic、isFinal、isPrivate

Class类中的getFields、getMethods和getConstructors方法返回类提供的public域、方法和构造器数组，其中包括超类的公有成员

Class类中的getDeclareFields、getDeclareMethods和getDeclaredConstructors方法将返回类中声明的所有域、方法和构造器，不包括超类的成员
**实例：**
```java
import java.lang.reflect.*;
import java.util.Scanner;

public class Mian2 {
    public static void main(String[] args) throws ClassNotFoundException {
        String name;
        if (args.length > 0) name = args[0];
        else {
            Scanner in = new Scanner(System.in);
            name = in.next();
        }

        Class<?> aClass = Class.forName(name);
        Class<?> superclass = aClass.getSuperclass();
        String s = Modifier.toString(aClass.getModifiers());
        if (s.length() > 0) {
            System.out.print(s + " ");
        }
        System.out.print("class " + name);
        if (superclass != null && superclass != Object.class) System.out.print(" extends" + superclass.getName());
        System.out.print(" {\n");
        printConstructor(aClass);
        System.out.println();
        printMethods(aClass);
        System.out.println();
        printFields(aClass);
        System.out.print("}");
    }

    public static void printConstructor(Class cl) {
        Constructor[] declaredConstructors = cl.getDeclaredConstructors();
        for (Constructor c : declaredConstructors) {
            String name = c.getName();
            System.out.print(" ");
            String modifiers = Modifier.toString(c.getModifiers());
            if (modifiers.length() > 0) System.out.print(modifiers + " ");
            System.out.print(name + "(");

            Class[] parameterTypes = c.getParameterTypes();
            for (int j = 0; j < parameterTypes.length; j++) {
                if (j > 0) System.out.print(", ");
                System.out.print(parameterTypes[j].getName());
            }
            System.out.println(");");
        }
    }

    public static void printMethods(Class cl) {
        Method[] declaredMethods = cl.getDeclaredMethods();
        for (Method m : declaredMethods) {
            String name = m.getName();
            System.out.print(" ");
            String modifier = Modifier.toString(cl.getModifiers());
            if (modifier.length() > 0) System.out.print(modifier + " ");
            Class<?> returnType = m.getReturnType();
            System.out.print(returnType.getName() + "(");

            Class<?>[] parameterTypes = m.getParameterTypes();
            for (int i = 0; i < parameterTypes.length; i++) {
                if (i > 0) System.out.print(", ");
                System.out.print(parameterTypes[i].getName());
            }
            System.out.println(");");
        }
    }

    private static void printFields(Class cl) {
        Field[] declaredFields = cl.getDeclaredFields();
        for (Field f : declaredFields) {
            Class<?> type = f.getType();
            String name = f.getName();
            System.out.print(" ");
            String modifiers = Modifier.toString(cl.getModifiers());
            if (modifiers.length() > 0) System.out.print(modifiers + " ");
            System.out.println(type.getName() + " " + name);
        }
    }
}

```
#### 5.7.5使用反射在运行时分析对象
反射机制的默认行为受限于Java的访问控制。然而，如果一个Java程序没有受到安全管理器的控制，就可以覆盖访问控制。为了达到这个目的，需要调用 Field、Method 或constructor 对象的 setAccessible 方法。例如
```java
f.setAtcessible(true); // now OK to call f.get(harry);
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200530212108681.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMjAyNTM5,size_16,color_FFFFFF,t_70)
编写一个通用的toString方法。

```java
public class ObjectAnalyzer {
    private ArrayList<Object> visited = new ArrayList<>();

    public String toString(Object obj) {
        if (obj == null) return "null";
        if (visited.contains(obj)) return "...";
        visited.add(obj);
        Class cl = obj.getClass();
        if (cl == String.class) return (String) obj;
        if (cl.isArray()) {
            String r = cl.getComponentType() + "[]{";
            for (int i = 0; i < Array.getLength(obj); i++) {
                if (i > 0) r += ",";
                Object val = Array.get(obj, i);
                if (cl.getComponentType().isPrimitive()) r += val;
                else r += toString(val);
            }
            return r + "}";
        }

        String r = cl.getName();
        do {
            r += "[";
            Field[] fields = cl.getDeclaredFields();
            AccessibleObject.setAccessible(fields, true);
            for (Field f : fields) {
                if (!Modifier.isStatic(f.getModifiers())) {
                    if (!r.endsWith("[")) r += ",";
                    r += f.getName() + "=";
                    try {
                        Class t = f.getType();
                        Object val = f.get(obj);
                        if (t.isPrimitive()) r += val;
                        else r += toString(val);
                    } catch (Exception e) {
                        e.printStackTrace();
                    }
                }
            }
            r += "]";
            cl = cl.getSuperclass();
        }
        while (cl != null);
        return r;
    }
}
```
### 5.8继承的设计技巧

 1. 将公共操作和字段放在超类中
 2. 不要使用受保护的字段
 3. 使用继承实现is-a关系
 4. 除非所有继承的方法都有意义，否则不要使用继承
 5. 在覆盖方法时，不要改变预期的行为
 6. 使用多态，而不要使用类型信息
 7. 不要滥用反射
## 接口、Lambbda表达式与内部类
### 6.1接口
#### 6.1.1接口概念
接口不是类，而是对希望符合这个接口的类的一组要求。
接口中的所有方法都是public，因此声明方法时不用加public修饰符。
接口绝不会有实例字段。在Java8之前接口中不会有任何实现方法。但是现在可以提供一些简单的默认实现。

类实现接口：

 - 用implements 声明实现哪个接口
 - 实现接口的所有方法

在实现接口时，必须把所有方法声明为public。
#### 6.1.2接口的属性
接口不能用new来构造。
可以用instanceof来检查一个对象是否实现了摸个接口。
接口中虽然不能有示例字段，但是可以包含常量。
与接口中的方法都为public一样，接口中的字段总是为public static final。
#### 6.1.3接口与抽象类的不同

 1. 每个类只能扩展一个抽象类，但是可以实现多个接口。
 2. 接口方法都为public，且只能有默认实现。而抽象类中可以有非抽象方法。
 3. 接口的字段只有public static final。而抽象类不一定。
 4. 抽象类相当于模板设计，接口相当于行为的抽象。
#### 6.1.4静态和私有方法
在Java8中，允许接口增加静态方法。
在Java9中，接口的方法可以是private。private可以是静态方法或实例方法。
#### 6.1.5默认方法
用default修饰的方法为接口的默认实现。

```java
public interface Comparabel<T>{
	default int compareTo(T other){ return 0; }
}
```
默认方法的一个重要用法就是“**接口演化**”。
假设有一个用了很久的接口，要在接口增加一个方法。如果这个方法不是默认方法，那么之前实现接口的类就会编译失败，统统要去实现这个新方法，就会很麻烦。
#### 6.1.6解决默认方法冲突
如果现在一个接口中定义了一个默认方法，然后又在父类或另一个接口中定义了同样的方法，就会产生冲突。Java的解决方法是：

 1. 超类优先。如果超类提供了一个具体的方法，那么同名而且有相同参数的默认方法就会被忽略。
 2. 接口冲突。如果一个接口提供了一个默认方法，另一个接口提供了相同的方法，必须覆盖这个方法解决冲突。

#### 6.1.9对象克隆
**深拷贝：**对基本数据类型进行值传递，对引用数据类型，创建一个新的对象，并复制其内容，此为深拷贝。
**浅拷贝：**对基本数据类型进行值传递，对引用数据类型进行引用传递般的拷贝，此为浅拷贝。
### 6.2lambda表达式
Lambda 表达式，也可称为闭包。
**语法：**

```java
(parameters) -> expression
//或
(parameters) ->{ statements; }
```
以下是lambda表达式的重要特征:

 - **可选类型声明**:不需要声明参数类型，编译器可以统一识别参数值。
 - **可选的参数圆括号**:一个参数无需定义圆括号，但多个参数需要定义圆括号。
 - **可选的大括号**：如果主体包含了一个语句，就不需要使用大括号。
 - **可选的返回关键字**：如果主体只有一个表达式返回值则编译器会自动返回值，大括号需要指定明表达式返回了一个数值。

**实例**

```java
// 1. 不需要参数,返回值为 5  
() -> 5  
  
// 2. 接收一个参数(数字类型),返回其2倍的值  
x -> 2 * x  
  
// 3. 接受2个参数(数字),并返回他们的差值  
(x, y) -> x – y  
  
// 4. 接收2个int型整数,返回他们的和  
(int x, int y) -> x + y  
  
// 5. 接受一个 string 对象,并在控制台打印,不返回任何值(看起来像是返回void)  
(String s) -> System.out.print(s)
```
**变量作用域**
lambda 表达式只能引用标记了 final 的外层局部变量，这就是说不能在 lambda 内部修改定义在域外的局部变量，否则会编译错误。
lambda 表达式的局部变量可以不用声明为 final，但是必须不可被后面的代码修改（即隐性的具有 final 的语义）
在 Lambda 表达式当中不允许声明一个与局部变量同名的参数或者局部变量。
### 6.3内部类
内部类就是定义在另一个类中的类。
两个原因：

 - 内部类可以对同一个包中的其他类隐藏。
 - 内部类方法可以访问定义这个类的作用域中的数据，包括原本私有的数据。
#### 6.3.1使用内部类访问对象状态
内部类的对象总有一个隐式引用，指向创建他的外部类对象。
这个引用在内部类中的定义是不可见的。
可见这个博主的文章：
[内部类](https://www.cnblogs.com/chenssy/p/3388487.html)
## 7异常、断言和日志
### 7.1异常
#### 7.1.1异常分类
异常类对象都是派生与Throwable类的一个类实例。
![异常](https://img-blog.csdnimg.cn/20200531155806870.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxMjAyNTM5,size_16,color_FFFFFF,t_70)
Java将派生与Error类和RuntimeException类的所有异常成为**非检查型异常**。
其他异常均称为**检查型异常**。
在Java中只能抛出检查型异常。
#### 7.1.2抛出检查型异常
```java
public printFileName(String name) throws FileNotFoundException{
}
```
下面4种情况会抛出异常：
 - 调用一个抛出检查型异常的方法。
 - 检测到一个错误，并用throws语句抛出一个检测型异常。
 - 程序出现错误，会跑出一个非检查型错误
 - Java虚拟机或运行时库出现内部错误。

> **警告：**
> 如果子类覆盖了父类的一个方法，则子类方法中声明的检查类异常不能比超类中声明的异常更通用。如果超类方法中没有抛出检查类型异常，则子类也不能抛出任何检查型异常。
#### 7.1.3创建自定义异常类
习惯做法是，自定义异常类应该包含两个构造器，一个是默认无参构造器，一个是包含详细信息的构造器。

```java
class FileFormatException extends IOException{
	public FileFormatException(){}
	public FileFormatException(String gripe){
		super(gripe);
	}
}
```
#### 7.1.4捕获异常

```java
try{
	...
}catch(..){
	...
}catch(...){
	..
}
finally{
	...
}
```
如果try中的代码抛出了catch中的任一个异常，那么程序将跳过剩余的try子句，执行catch中的子句。如果没有抛出任何异常就跳过catch子句。如果抛出了一个catch中没有声明的异常，这个方法就会立即退出。最后不管如何，finally子句都会执行。
**注释：**
可以在catch中抛出一个异常，通常用于改变异常的类型。
```java
try{
}
catch(SQLException e){
	throw new ServeletException("Error"+d.getMessage());
}
```
更好的方法是把原始异常设置为新异常的原因：

```java
try{
}
catch(SQlexception original){
	var e = new ServeletException("error");
	e.initCause(original);
	throw e;
}
```

> **注意**：finally子句要用于清理资源，不要把改变控制流的语句（return、throw、break、continue）放在finally子句中。

**try-with-resources语句**
最简形式：

```java
try（Resource res = ...）{
	work with res...
}
```
当try语句退出时，会自动调用res.close。
**典型例子：**

```java
try(var in = new Scanner(
	new FileInputStream("/usr/txt.txt"),StandardCharsets.UTF_8)){
	while(in.hasNext){
		System.out.println(in.next());
	}
}
```
这个快正常退出时，或者存在一个异常时，都会调用in.close（）方法，都能关闭。

它还可以指定多个资源：

```java
try(var in = new Scanner(
	new FileInputStream("/usr/txt.txt"),StandardCharsets.UTF_8);
	var out = new Printer("out.txt"),StandardCharsets.UTF_8){
	while(in.hasNext){
		out.println(in.next());
	}
}
```
**总结：只要需要关闭资源，就尽量用try-with-Resources语句，相对于try-finally可以减少代码量.**
#### 7.1.5使用异常的一些小技巧

 1. 异常处理不能代替简单测试
 2. 不要过分的细化异常
 3. 充分利用异常层次结构
 4. 不要抑制异常
 5. 在检测错误时，“苛刻”要比放任更好
 6. 不要羞于传递异常

 **“5和6”可以总结为“早抛出、晚捕获”**

## 参考书籍
Java核心技术

