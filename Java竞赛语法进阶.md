# Java竞赛语法进阶

这里面的东西都挺好：[Java 进阶 - OI Wiki (oi-wiki.org)](https://oi-wiki.org/lang/java-pro/#biginteger-与数论)

## math包

### BigInteger类

> 这里整理的相当详细：[Java 进阶 - OI Wiki (oi-wiki.org)](https://oi-wiki.org/lang/java-pro/#biginteger-与数论)
>
> 先看看都每个方法有个大概的印象，基本的记下，难记的靠编译器提示。



> 详细的自己看最上面的那些资料**这里仅仅是补充说明**

- **导入包**：`import java.math.BigInteger;`【忘了就自动导包`ctrl+shift+o`】

#### 构造方式：

```java
		BigInteger a=new BigInteger("0");
		BigInteger b=sc.nextBigInteger();
		BigInteger c=new BigInteger("16",8);//指明前面的字符串"16"为8进制(任意个进制都行)，并转为十进制
```

> 几乎所有的基本也有对应的构造函数
>
> `new BigInteger("数字",任意进制)`:将这个进制的数转为十进制



> 
>
> 补充一下（跟上面其实关系不大，可以跳）：
>
> 常见进制的表示方法及其对应的十进制值：
>
> - 二进制（base 2）：以 "0b" 或 "0B" 开头，后接二进制数字序列。例如，"0b1010" 表示十进制的 10。
> - 八进制（base 8）：以 "0" 开头，后接八进制数字序列。例如，"077" 表示十进制的 63。
> - 十进制（base 10）：直接使用数字序列表示。例如，"123" 表示十进制的 123。
> - 十六进制（base 16）：以 "0x" 或 "0X" 开头，后接十六进制数字序列。例如，"0xFF" 表示十进制的 255。

#### 基本运算

> 最好把常用的单词记住，剩下的看提醒





> 绝对值，取负
>
> 加减乘除，c++版取模remainder和数学取模mod，幂，
>
> （二进制位运算）与 或 非 取反 异或 左|右移位，（一个了解版，用到的应该特少）二进制中**不包括符号位**的1个数 |  长度 | 最右边1的位置，
>
> 两数取大 | 小值，
>
> 比较大小(-1表示小)，转为字符串（通用）
>
> `toString(int radix)`:返回 this 的 raidx 进制字符串表示形式

**都是返回副本，不会改变这个对象**



#### 基本运算



> 取最大公约数
>
> 是否为素数，下一个素数（`ProbablePrime`）
>
> > 是否为质数需要传个`val`置信度，越高越准确，但是越慢
> >
> > 一般传个50就够了
>
> 带模数的幂(`modPow`)
>
> 乘法逆元(`modInverse`)



> 这些幂的底层很复杂，反正挺快的，不仅仅是快速幂的一些东西



### BigDecimal类

[java中BigDecimal的介绍及使用，BigDecimal格式化，BigDecimal常见问题-CSDN博客](https://blog.csdn.net/weixin_49114503/article/details/129056256?ops_request_misc=%7B%22request%5Fid%22%3A%22171055997616777224454939%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=171055997616777224454939&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-129056256-null-null.142^v99^pc_search_result_base8&utm_term=BigDecimal&spm=1018.2226.3001.4187)

> 很多东西跟上面类似

**这种一般都不能是`NULL`**



#### 高精度构造

```java
BigDecimal a=new BigDecimal("0.1255");
BigDecimal b2= BigDecimal.valueOf(0.1);//不能用上面在用这个，但是不要new BigDecimal(0.1)，这是精度已经丢失了，上面这个是先转为字符串在构造的
```



- **最好直接用==字符串==构造方法，否则一开始就有精度误差**

- **如果无法满足用`valueOf(浮点数)`**



#### 等值比较

**用`a.compareTo(BigDecimal类型)`**

> 别用`equals`

#### 输出：

##### 输出模式

> 有挺多的，只写下常用的

```java
		BigDecimal a=new BigDecimal("0.1255");
		System.out.println(a);//默认：ROUND_UNNECESSARY(精确模式)
		System.out.println(a.setScale(3,BigDecimal.ROUND_DOWN));//直接舍掉后面的小数
		System.out.println(a.setScale(3,BigDecimal.ROUND_HALF_UP));//四舍五入
```

##### 表示形式：

`toString()`:超出一般的精度一般科学计数法输出

`toPlainString()`:十进制输出



> 还有很多注入像一些格式化输出的就不写了



#### 除不尽

```java
public static void main(String[] args){
   BigDecimal b1 = new BigDecimal("1.0");
   BigDecimal b2 = new BigDecimal("3.0");
   System.out.println(b1.divide(b2,2, RoundingMode.HALF_UP));//0.33
}
```

如果用除`divide`，除不尽要约掉，否则会爆异常

## Math库（默认包中的）

> 看自动提示吧，记不住

`Math.PI`:返回圆周率



## 日期操作

> [Java中的日期时间类详解（Date、DateFormat、Calendar）_java date-CSDN博客](https://blog.csdn.net/sc179/article/details/108687144)

> 平年：365天，二月：28
>
> 闰年：366天，二月：29
>
> > 一三五七八十腊，三十一天永不差，四六九冬三十日，平年二月二十八，闰年二月把一加。

**日期大小的比较：**字典序即可

### 日期差值

[3498. 日期差值 - AcWing题库](https://www.acwing.com/problem/content/3501/)

有两个日期，求两个日期之间的天数，如果两个日期是连续的我们规定他们之间的天数为两天。

**数据范围：**年份范围 [1,9999]，保证输入日期合法。测试数据的组数不超过 $100$。

---

#### `java`包方法

> `LocalDate`：存下日期
>
> 静态构造方法：
>
> - `LocalDate.parse(字符串,DateTimeFormatter formatter)`：解析成这个类型
> - `LocalDate.of(年,月,日整型)`
>
> 方法：
>
> - `format(DateTimeFormatter formatter)`:输出字符串
>
> `DateTimeFormatter`：格式化日期
>
> - `ofPattern(字符串)`:指定日期格式
>
> `ChronoUnit`：算各种日期差值

> 这个花的时间，还会比下面的多一点点

```java
//1.Date+SimpleFormat包，不行有问题
//2.LocalDate+DateTimeFormatter+Periord有问题
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.time.temporal.ChronoUnit;
import java.util.Scanner;
public class Main{
	public static void main(String[] args) {
		Scanner sc=new Scanner(System.in);
		DateTimeFormatter df=DateTimeFormatter.ofPattern("yyyyMMdd");
		while(sc.hasNext()) {
			LocalDate d1=LocalDate.parse(sc.next(),df);
			LocalDate d2=LocalDate.parse(sc.next(),df);
			long res=Math.abs(ChronoUnit.DAYS.between(d1, d2))+1;
			System.out.println(res);
		}
	}
}
```

> 资料：(有的详细的过头了，大概看看)
>
> [JDK8中的新时间API:Duration Period和ChronoUnit介绍 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/274295453)
>
> [【Java 8 新特性】Java LocalDate 详解-CSDN博客](https://blog.csdn.net/qq_31635851/article/details/117880835)

参考：[AcWing 3498. 日期差值（每日一题） - AcWing](https://www.acwing.com/activity/content/code/content/7993162/)

#### 直接算

> 很优雅，`java`输入比较麻烦就不写了

> **年份是从1开始的**
>
> 思路：
>
> > 类似前缀和，都转为$[1,y]$的天数，然后算差值
> >
> > 这个是先一年年，在一月月算的

```c++
#include <iostream>
#include <cstring>
#include <algorithm>

using namespace std;

const int months[] = {
    0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31
};

int is_leap(int year)
{//不要忘了，经典判断方法，%4时不能%100 或者 能直接%400
    if (year % 4 == 0 && year % 100 || year % 400 == 0)
        return 1;
    return 0;
}

int get_days(int y, int m)
{
    if (m == 2) return 28 + is_leap(y);
    return months[m];
}

int calc(int y, int m, int d)
{
    int res = 0;
    for (int i = 1; i < y; i ++ )
        res += 365 + is_leap(i);
    for (int i = 1; i < m; i ++ )
        res += get_days(y, i);
    return res + d;
}

int main()
{
    int y1, m1, d1, y2, m2, d2;
    while (~scanf("%04d%02d%02d\n%04d%02d%02d", &y1, &m1, &d1, &y2, &m2, &d2))
        printf("%d\n", abs(calc(y1, m1, d1) - calc(y2, m2, d2)) + 1);

    return 0;
}
作者：yxc
```

### `Date`与`DateFomat`(==有问题，感觉用不了==)

> 这个比较老了，很容易有问题

> 详细内容看上面的博客，这里只是举举例子
>
> 这里只说用途：**算日期差值**
>
> > 1毫秒=/1000 秒=/1000/60 分钟 = /1000/60/60 小时 = /1000/60/60/24 天

- `java.util.Date`类:表示特定的瞬间，精确到**毫秒**。Date类的构造函数可以把**毫秒值转成日期对象**。

  **构造方法：**(不用咋看，下面赶时间了解下就行)

  > -   `public Date()`：分配Date对象并初始化此对象，以表示分配它的时间（精确到毫秒）。
  > -   `public Date(long date)`：分配Date对象并初始化此对象，以表示自从标准基准时间（称为“历元（epoch）”，即1970年1月1日00:00:00 GMT）以来的指定毫秒数。
  >
  > > tips: 由于我们处于东八区，所以我们的基准时间为1970年1月1日8时0分0秒。
  >
  > - `getTime()`方法：获取具体的毫秒值

  

- `java.text.DateFormat` 表示:日期/时间格式化子类的**抽象类**（**不能直接使用**），实现在`Date`对象与`String`对象之间进行来回转换。

  > 更类似一个工具类
  
  > **需要用子类构造**
  >
  > - `public SimpleDateFormat(String pattern)`：用给定的模式和默认语言环境的日期格式符号构造SimpleDateFormat。
  >
  >   具体的格式规则：
  >
  >   | 标识字母（区分大小写） | 含义 |
  >   | ---------------------- | ---- |
  >   | y                      | 年   |
  >   | M                      | 月   |
  >   | d                      | 日   |
  >   | H                      | 时   |
  >   | m                      | 分   |
  >   | s                      | 秒   |
  >
  > **常用方法：**
  >
  > - `public String format(Date date)`：将Date对象格式化为字符串。
  > - `public Date parse(String source)`：将字符串解析为Date对象。
  
  

下面就是运用实例了：

```java
		String str="2004 06 26";
		DateFormat df=new SimpleDateFormat("yyyy MM DD");
		Date date=df.parse(str);//解析为Date类
			//需要抛异常
		System.out.println(df.format(date));//格式化为字符串
		
		//下面这样也是行的
		str="2004 6 26";
		df=new SimpleDateFormat("y M d");
		System.out.println(df.parse(str));
```

### `Calendar`日历类

> [Java学习笔记——Calendar类-CSDN博客](https://blog.csdn.net/weixin_45666660/article/details/124544710)
>
> **这篇博客写的特别详细了**，直接看这个复习，这里只是快速过一下
>
> > 主要就是用来完成一些日期的运算（这个特别全）
>
> **大部分东西都是需要使用静态的方法来构造的，像实列化、获取和得到一个字段**

**Calendar:**

- `public static Calendar getInstance()`：实例化，使用默认时区和语言环境获得一个日历
- `public int get(int field)`：返回给定日历字段的值。
- `public void set(int field, int value)`：将给定的日历字段设置为给定值。
- `public abstract void add(int field, int amount)`：根据日历的规则，为给定的日历字段添加或减去指定的时间量。
- `public Date getTime()`：返回一个表示此`Calendar`时间值（从历元到现在的毫秒偏移量）的Date对象。

> **注意：**这里的`field`直接就是`Calendar的静态方法来获取的

![](https://img-blog.csdnimg.cn/0a6743914b634f61a3464c92c5e497ad.png)

> **注意==查询==时：**
>
> 西方**星期**的开始为周日（1）周一（2），中国开始为周一(减$1$使用)
>
> 在Calendar类中，**月份**的表示是以0-11代表1-12月（**从$0$开始**，加$1$使用）
>
> > 其取值范围是`1`到`7`，分别对应的是星期日到星期六。具体如下：
> >
> > - 1 表示星期日（`Calendar.SUNDAY`）
> > - 2 表示星期一（`Calendar.MONDAY`）
> > - 3 表示星期二（`Calendar.TUESDAY`）
> > - 4 表示星期三（`Calendar.WEDNESDAY`）
> > - 5 表示星期四（`Calendar.THURSDAY`）
> > - 6 表示星期五（`Calendar.FRIDAY`）
> > - 7 表示星期六（`Calendar.SATURDAY`）



**使用时，特别注意下月份和星期很特殊就行，到时候如果忘记了，可以写下英语单词点进去看一下**

> `Calendar+对应单词`

例子：

```java
//Calendar使用
		//日期【根据字段】设置
		Calendar cal=Calendar.getInstance();
		cal.set(Calendar.YEAR, 2024);
		cal.set(Calendar.MONTH,3-1);//注意：月份从0开始计数
		cal.set(Calendar.DAY_OF_MONTH,30);
		
		//日期【根据字段】加减
		cal.add(Calendar.DAY_OF_MONTH,+14);
		cal.add(Calendar.YEAR,-1);
		
		//日期的输出
		 // 获取年
        int year = cal.get(Calendar.YEAR);
         // 获取月
        int month = cal.get(Calendar.MONTH) + 1;//注意是从1开始的
         // 获取日
        int dayOfMonth = cal.get(Calendar.DAY_OF_MONTH);
        System.out.println(year + "年" + month + "月" + dayOfMonth + "日");

```







