# JavaScript高级程序设计
想把书里面的代码都练习一下，并做个总结，包名按书的版本。

## 第2章 在HTML中使用JavaScript

### 2.1<script>元素

#### 2.1.1 标签的位置

```
<!DOCTYPE html>
<html>
	<head>
		<title>Example HTML Page</title>
		<script type="text/javascript" scr="example.js"></script>
	</head>
	<boby>
		<!-- 这里放内容 -->
	</boby>
</html>
```

#### 2.1.2 延迟脚本

------

在XHTML文档中，要把defer属性设置为defer="defer"

------

### 2.4 <noscript>元素

​	符合任一条件：

1. 浏览器不支持脚本

2. 浏览器支持脚本，但脚本被禁用

   浏览器就会显示<noscript>内容

```
<!DOCTYPE html>
<html>
	<head>
		<title>Example HTML Page</title>
		<script type="text/javascript" scr="example.js"></script>
	</head>
	<boby>
		<!-- 这里放内容 -->
		<noscript>
			<p>本页面需要浏览器支持（启用）JavaScript。
		</noscript>
	</boby>
</html>
```

## 第3章 基本概念

### 3.1 语法

#### 3.1.1 区分大小写

​	ECMAScript中的一切（变量、函数名和操作符）都区分大小写。

#### 3.1.2 标识符

​	指变量、函数、属性的名字，或者函数的参数。

​	规则：

1. 第一个字符必须是一个字母、下划线（_）、或者一个美元符号（$）;

2. 其他字符可以是字母、下划线、美元符号或数字。

   ​	ECMAScript标识符采用驼峰大小格式。（第一个单词的首字母小写，剩下的单词首字母大写）例如：firstSecond、myCar

------

​	不能把关键字、保留字、true、false和null用作标识符

------

#### 3.1.3 注释

```
// 单行注释
/*
* 这是一个多行
* （块级）注释
*/
```

#### 3.1.4 严格模式

​	在顶部添加: "use strict";

​	也可以在指定函数内执行。

### 3.2 关键字和保留字

**关键字：**

​	break 			do 				instanceof 		typeof 

​	case				else 		 	new					var 

​	catch		   	finally 		 return 			   void 

​	continue		 for 			   switch 			  while 

​	debugger*	 function   	this 				   with 

​	default			if 				  throw 

​	delete 			in 				 try 

**保留字：**

​	abstract 		enum		 	int 					short 

​	boolean 		export 		   interface 		 static 

​	byte 			   extends		  long 				 super 

​	char 			   final 			   native 			  synchronized 

​	class 			  float 			    package  		throws 

​	const 			 goto 			    private 		   transient 

​	debugger 	  implements	protected 	  volatile 

​	double 		  import 			 public 

 

第5 版把在非严格模式下运行时的保留字缩减为下列这些：

​	class 				enum 			extends 			super 

​	const 			   export 		   import 

在严格模式下，第 5 版还对以下保留字施加了限制：

​	implements     package 		public 

​	interface 		  private 		  static 

​	let 					 protected	   yield 

### 3.4 数据变量

#### 3.4.1 typeof操作符

- "undefined" —— 如果这个值未定义；
- "boolean" —— 如果这个值是布尔值；
- "string" —— 如果这个值是字符串；
- "number" —— 如果这个值是数值；
- "object" —— 如果这个值是对象或者null；
- "function" —— 如果这个值是函数；
- 

#### 3.4.2 undefined类型

#### 3.4.3 Null类型

#### 3.4.4 Boolean类型

| 数据类型  | 转换为true的值                                 | 转换为false的值 |
| --------- | ---------------------------------------------- | --------------- |
| Boolean   | true                                           | false           |
| String    | 任何非空字符串                                 | ""              |
| Number    | 任何非零数字值（包括无穷大）                   | 0和NaN          |
| Obiect    | 任何对象                                       | null            |
| Undefined | n/a<!--not applicable的缩写，意思是“不适用”--> | undefined       |

#### 3.4.5 Number类型

##### 2. 数值范围

​	-Infinity（负无穷）、Infinity（正无穷）

##### 3. NaN

​	非数值（Not a Number）

​	NaN与任何值都不相等，包括NaN本身。

​	ECMAScript 定义了 **isNaN()** 函数，帮我们确定这个参数是否“不是数值”。

------

​		在基于对象调用 **isNaN()**函数时，会首先调用对象的 **valueOf()**方法，然后确定该方法返回的值是否可以转换为数值。如果不能，则基于这个返回值再调用 **toString()**方法，再测试返回值。

------

##### 4. 数值转换

###### 	**Number()** 函数转换规则：

- Boolean：true和false被分别转换为1和0。

  ```
  Number(true);			//1
  Number(false);			//0
  ```

- null：返回0。

  ```
  Number(null);			//0
  ```

- undefined：NaN。

  ```
  Number(undefined)			//NaN
  ```

- 字符串：

  - 字符串中只包含数字，则将其转换为十进制值。

    ```
    Number("123")				//123
    ```

  - 字符串中只包含有效的浮点格式，则转换为对应的浮点数值。

    ```
    Number("1.23")				//1.23
    ```

  - 空字符串，则转换为0。

    ```
    Number("")					//0
    ```

  - 字符中包含有效的十六进制格式，则转换为十进制整数值。

    ```
    Number("0xf")				//15
    ```

  - 包含除上述格式之外的字符，则将其转换为NaN。

    ```
    Number("123a")				//NaN
    Number("1.23a")				//NaN
    Number("0xfg")				//NaN
    ```

- object：调用valueOf()方法。如果是NaN，则调用toString()，返回字符串。

  ###### parseInt() 转换规则：

  ```
  /**
    * @param s A string to convert into a number.
    * @param radix A value between 2 and 36 that specifies the base of the number in numString.
    */
  parseInt("1234blue"); 			// 1234 
  parseInt("");				 	// NaN 
  parseInt("0xA"); 				// 10（十六进制数）
  parseInt(22.5); 				// 22 
  parseInt("070"); 				// 56（八进制数）
  parseInt("70"); 				// 70（十进制数）
  parseInt("0xf"); 				// 15（十六进制数）
  
  /*
   * 字符串以"0x"开头且后跟数字字符，就会将其当作一个十六进制整数；
   * 字符串以"0"开头且后跟数字字符，则会将其当作一个八进制数来解析。
   */
   
  parseInt("0xAF", 16); 			//175
  parseInt("AF", 16); 			//175
  parseInt("AF"); 				//NaN
  
  parseInt("10", 2);              //2 （按二进制解析）
  parseInt("10", 8);              //8 （按八进制解析）
  parseInt("10", 10);             //10 （按十进制解析）
  parseInt("10", 16);             //16 （按十六进制解析）
  ```

  ###### parseFloat() 转换规则：

  ```
  parseFloat("1234blue");                 //1234 （整数）
  parseFloat("0xA");                      //0 
  parseFloat("22.5");                     //22.5 
  parseFloat("22.34.5");                  //22.34 
  parseFloat("0908.5");                   //908.5 
  parseFloat("3.125e7");                  //31250000
  ```

#### 3.4.6 String 类型

##### 1. 字符字面量

##### 2. 转换为字符串

###### 	**toString()**

```
var found = ; 
found.toString();               // 字符串"true"
var num = 10; 
num.toString();                 // "10" 
num.toString(2);                // "1010" 
num.toString(8);                // "12" 
num.toString(10);               // "10" 
num.toString(16);               // "a"
```

###### 	String()

```
var value; 
String(10);                     // "10" 
String(true);                   // "true" 
String(null);                   // "null" 
String(undefined);              // "undefined" 
String(value);                  // "undefined"
```

数值和布尔值的转换结果与调用**toString()**方法得到的结果相同。因为 null 和 undefined 没有toString()方法，所以 **String()**函数就返回了这两个值的字面量。

#### 3.4.7 Object

​	Object的每个实例都具有下列属性和方法:

- constructor
- hasOwnproperty(propertyName)：用于检查给定的属性在当前对象实例中（而不是在实例的原型中）是否存在。
- isPrototypeOf(object)：用于检查传入的对象是否是传入对象的原型。
- toLocaleString()
- toString()
- valueOf()

### 3.5 操作符

#### 3.5.1 一元操作符

