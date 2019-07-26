一、概述
JavaScript 有七种数据类型：
* 数值（number）: 整数和小数
* 字符串（string）:  文本 （hello）
* 布尔值（boolean）: 表示真伪的两个特殊值，true(真)、false(假)
* symbol：待补充...
* 未定义（undefined）: 没有被定义的值
* 空（null）：值为空
* 对象（object）: 各种值组成的集合，可以是数值、字符串、布尔值等的组合。<br/>
**1、一般来说 number、string、boolean、symbol、null、undefined 属于简单数据类型，而对象（object）则属于复杂数据类型**
**2、对象又可以分成三个子类型：**
*狭义的对象（object）*
*数组（array）*
*函数（function）*
狭义的对象和数组是两种不同的数据组合方式,函数其实是处理数据的方法，JavaScript 把它当成一种数据类型，可以赋值给变量，这为编程带来了很大的灵活性，也为 JavaScript 的“函数式编程”奠定了基础。<br/>
**JavaScript 有三种方法来确定一个值到底是什么类型 :**
* *typeof运算符*
* *instanceof运算符*
* *Object.prototype.toString方法*<br/>
**typeof运算符可以返回一个值的数据类型。数值、字符串、布尔值分别返回number、string、boolea。**
```
typeof 123 // "number"
typeof '123' // "string"
typeof false // "boolean"
```
**函数返回function。**
```
function f() {}
typeof f   // "function"
```
**undefined返回undefined。**
```
typeof undefined
// "undefined"
```
**对象返回object。**
```
typeof window // "object"
typeof {} // "object"
typeof [] // "object"
```
上面代码中，空数组（[]）的类型也是object，这表示在 JavaScript 内部，数组本质上只是一种特殊的对象。<br/>
**null返回object。**
```
typeof null // "object"
```
**instanceof运算符可以区分数组和对象。**
```
var o = {};
var a = [];
o instanceof Array // false
a instanceof Array // true
```
#二、null 、undefined 、boolean 简介
**null和undefined** : 在if语句中，它们都会被自动转为false，相等运算符（==）甚至直接报告两者相等。
```
if (!undefined) {
  console.log('undefined is false');
}
// undefined is false

if (!null) {
  console.log('null is false');
}
// null is false

undefined == null
// true
```
**两者的含义和用法虽然差不多，但是，JavaScript 的设计者 Brendan Eich认为他们的区别是这样的：null是一个表示“空”的对象，转为数值时为0；undefined是一个表示"此处无定义"的原始值，转为数值时为NaN。**
```
Number(undefined) // NaN
5 + undefined // NaN
```
**boolean:**如果 JavaScript 预期某个位置应该是布尔值，会将该位置上现有的值自动转为布尔值。转换规则是除了下面六个值被转为false，其他值都视为true。(五个falsy值)

* undefined
* null
* false
* 0
* NaN
* ""或''（空字符串）
#三、number
**JavaScript 内部，所有数字都是以64位浮点数形式储存，即使整数也是如此。所以，1与1.0是相同的，是同一个数。**
这就是说，JavaScript 语言的底层根本没有整数，所有数字都是小数（64位浮点数）。容易造成混淆的是，某些运算只有整数才能完成，此时 JavaScript 会自动把64位浮点数，转成32位整数，然后再进行运算。由于浮点数不是精确的值，所以涉及小数的比较和运算要特别小心。
```
0.1 + 0.2 === 0.3
// false

0.3 / 0.1
// 2.9999999999999996

(0.3 - 0.2) === (0.2 - 0.1)
// false
```
数值的进制
使用字面量（literal）直接表示一个数值时，JavaScript 对整数提供四种进制的表示方法：十进制、十六进制、八进制、二进制。
* 十进制：没有前导0的数值。
* 八进制：有前缀0o或0O的数值，或者有前导0、且只用到0-7的八个阿拉伯数字的数值。
* 十六进制：有前缀0x或0X的数值。
* 二进制：有前缀0b或0B的数值。
默认情况下，JavaScript 内部会自动将八进制、十六进制、二进制转为十进制。
#4、特殊数值：
* 正零和负零
JavaScript 内部实际上存在2个0：一个是+0，一个是-0，区别就是64位浮点数表示法的符号位不同。它们是等价的。几乎所有场合，正零和负零都会被当作正常的0。唯一有区别的场合是，+0或-0当作分母，返回的值是不相等的。
`(1 / +0) === (1 / -0)  // false`
* NaN
NaN是 JavaScript 的特殊值，表示“非数字”（Not a Number），主要出现在将字符串解析成数字出错的场合。
```
Math.acos(2) // NaN
Math.log(-1) // NaN
Math.sqrt(-1) // NaN
0 / 0    //  NaN
```
需要注意的是，NaN不是独立的数据类型，而是一个特殊数值，它的数据类型依然属于Number，使用typeof运算符可以看得很清楚。
 ```
typeof NaN // 'number'
```
NaN不等于任何值，包括它本身。
```
NaN === NaN // false
```
NaN在布尔运算时被当作false。
`Boolean(NaN) // false`
NaN与任何数（包括它自己）的运算，得到的都是NaN。
```
NaN + 32 // NaN
NaN - 32 // NaN
NaN * 32 // NaN
NaN / 32 // NaN
```
