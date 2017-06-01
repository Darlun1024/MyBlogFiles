# Kotlin的基本数据类型

标签（空格分隔）： kotlin

---

Java有8种基本数据类型分别是byte,int,long,short,float,double,char,boolean。

对应的Kotlin也有Byte,Int,Long,Short,Float,Double,Char,Boolean，不过在Kotlin种这些类型也是对象。
这些基本数据类型有着与Java基本数据类型一致的工作方式。不过也有一些区别
**1.不能自动转换类型（想象一下Java的类可以自动转换类型么）**
```
val i:Int=7
val d: Double = i.toDouble()
```
对于没一种基本数字类型 Kotlin 都提供了以下方法用于数据转换：
```
toByte(): Byte
toShort(): Short
toInt(): Int
toLong(): Long
toFloat(): Float
toDouble(): Double
toChar(): Char
```
**2. Char 不能直接当做一个数字来处理（也是对象惹得祸啊）**
```
val c:Char='c'
val i: Int = c.toInt()
```
**3. 声明方式也有所区别**
```
//Kotlin数据声明和初始化
var a:Int = 100
var b:Long = 100L
var c:Float = 100f;
var d:Double = 100.0
//Kotlin会根据赋值自动推断数据类型
var A = 100
var B = 100L
var C = 100f
var D = 100.0
//对比一下Java的声明方式
int a    = 100;
long b   = 100L;
float c  = 100f;
double d = 100.0;
//Java 装箱的基本数据类型声明
Int A     = new Int(a);
Long B    = new Long(B);
Float C   = new Float(C);
Double D  = new Double(d);
```

**5. 位运算符也不同**
一下方法之适用于 Long 和 Int 数据类型。
| Kotlin | Java | 说明 |
| ------------- |:--------:| ------:|
| shl(bits)| << | 左移 | 
| shr(bits)| \>\> | 右移  | 
| ushr(bits)|  \>\>\>  |   无符号右移 | 
| and(bits)|  & | 与 | 
| or(bits) |  \| | 或  | 
| xor(bits)|  ^ |  异或 | 
| inv(bits)  |  ！ | 取反 | 


[1]boolean是为了纪念英国数学家George Boole而命名的；




