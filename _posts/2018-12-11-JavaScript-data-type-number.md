---
layout: post
title: JavaScript数据类型之数值类型
---

# JavaScript数据类型之数值类型

## 整数

在ECMAScript中，Number类型是使用[IEEE754](https://zh.wikipedia.org/wiki/IEEE_754)格式来表示整数和浮点数值。最基本的数值字面量格式是十进制整数，例如：
```javascript
var intNum = 55;
```
另外，整数还可以通过八进制或十六进制表示。其中八进制字面值的第一位必须是零（0），然后是八进制字符序列（0-7）。如果字面值中的数值超出了范围，则前导零将被忽略，后面的数值被当做十进制数值解析。如下：
```javascript
var octalNum1 = 070; // 八进制的56
var octalNum2 = 079; // 无效的八进制数值-解析为79
var octalNum3 = 08;  // 无效的八进制数值-解析为8
```
八进制字面量在严格模式下是无效的。十六进制字面量的前两位必须是0x，后跟任何十六进制的数字（0-9 a-f），其中字母a-f可大写也可小写，例：
```javascript
var hexNum1 = 0xA;  // 十六进制的10
var hexNum2 = 0x1f; // 十六进制的31
```
在进行算数计算时，所有以八进制和十六进制表示的数值最终都会被转换为十进制数值。

## 浮点数值

浮点数值即是指该数值中必须包含一个小数点，且小数点后面必须至少有一位数字。由于保存浮点数值需要的内存空间是整数值的两倍，所以当小数点后没有跟任何数字或者浮点数值本身就是一个整数（如1.0）时，该值将被转换为整数。

默认情况下，小数点后带有6个0以上的浮点数值将被转换为以科学计数法表示的数值（例如：0.0000003会被转换为3e-7）。浮点数值的的最高精度是17位小数。

但是由于IEEE754的缺陷，在ECMAScript中，`0.1+0.2 = 0.30000000000000004`,而不是我们期望的0.3，所以，在ECMAScript中，永远不要比较某个特定的浮点数值。

## NaN

NaN有两个特点：
* 任何涉及NaN的操作（例NaN/10）都会返回NaN
* NaN与任何值都不相等，包括NaN本身

针对以上特点，ECMAScript提供了isNaN()函数。isNaN()在接收到一个值之后，会尝试将这个值转化为数值。某些不是数值的值会直接转换为数值，例如字符串'10'或者Boolean值。而任何不能被转换为数值的值都会导致这个函数返回true。

## 数值转换

Number()，parseInt()，parseFloat()三个函数都可以用来做数值转换，但Number()适用于任何数据类型，但后两者则专门用于把字符串转换成数值。

### Number()函数的转换规则
* 如果是Boolean值，true和false分别转换为1和0；
* 如果是数字值，简单的传入和返回；
* 如果是null，返回0；
* 如果是undefined，返回NaN；
* 如果是字符串，遵循下列规则：
  * 如果字符串中只包含数字（包括正负号的情况），则转换为十进制的数值（前导零会被忽略）
  * 如果字符串中包含浮点格式，则转换为对应的浮点数值（忽略前导零）
  * 如果字符串中包含有效的十六进制格式，则转换为相同大小的十进制整数值
  * 如果字符串是空的，则转换为0；
  * 如果字符串中包含除上述格式之外的字符，则转换为NaN
* 如果是对象，则调用对象的valueOf()方法，然后依照前面的规则转换返回的值。如果转换的结果是NaN，则调用对象的toString()方法，然后再次依照前面的规则转换返回的字符串值。

### parseInt()函数的转换规则

忽略字符串前面的空格，直至第一个非空格字符：
如果第一个字符不是数字字符或者负号，返回NaN；
如果第一个字符是数字字符，继续解析第二个字符，直到解析完所有字符或者遇到一个非数字字符；
如果第一个字符是数字字符，parseInt()也能够识别出各种整数格式（如八进制、十六进制）。

但由于在ECMAScript5标准中，parseInt()已不具备解析八进制数值的能力，书中建议使用此函数时总是传入第二个参数：转换时使用的基数。例如：
```javascript
var num1 = parseInt('0xAF',16);
```
另外，如果像上例那样指定了第二个参数，字符串可以不带'0x',就像下面这样：
```javascript
var num2 = parseInt('AF',16);
```

### parseFloat()的转换规则

与parseInt()类似，从第一个字符开始解析每一个字符，直到字符串末尾，或者遇到一个无效的浮点数字字符为止。字符串中的第一个小数点是有效的，第二个开始就是无效的了，其后的字符会被忽略。

如果字符串包含的是一个可以被解析为整数的数，parseFloat()会返回整数。



*注：以上内容摘录或节选自《JavaScript高级程序设计（第3版）》page：27-32*

[返回](https://www.icenzhao.com/)