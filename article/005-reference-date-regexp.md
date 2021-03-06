## JavaScript 引用数据类型

本章内容较多，
引用类型的值（对象）是引用类型的一个实例。引用类型是一种数据结构，用于将数据和功能组织在一起。
ECMAScript 提供了很多原生引用类型。

### 1、Date类型

ECMAScript 中的 Date 类型是在早期 Java 中的 java.util.Date 类基础上构建的。为此，Date 类型使用自 UTC（国际协调时间）1970年1月1日午夜（零时）开始经过的毫秒数来保存日期。
    要创建一个对象，使用 new 操作符和 Date 构造函数即可，如下：
    
`var now = new Date();`

#### 日期/时间组件方法
    
| 方法 | 说明 |
| :-: | :-: |
| getTime() | 返回表示日期的毫秒数；与valueOf()方法返回的值相同 |
| setTime(毫秒) | 以毫秒数设置日期，会改变整个日期 |
| getFullYear() | 获取4位数的年份如：2018 |
| getMouth() | 获取日期中的月份，0表示一月，11表示十二月 |
| getDate() | 获取日期月份中的天数（1～31） |
| getDay() | 获取日期中的星期几（0表示星期日，6表示星期6） |
| getHours() | 获取日期中的小时数（0～23） |
| getMinutes() | 获取日期中的分钟数（0～59） |
| getSeconds() | 获取日期中的秒数（0～59） |
| getMilliseconds() | 获取日期中的毫秒数 |



### 2、RegExp类型

ECMAScript 通过 RegExp 类型来支持正则表达式。如下创建一个正则表达式。

`var expression = / pattern / flags ; `

一个正则包含两部分：模式（pattern）和 标志（flags）

正则表达式的匹配模式支持三个标志：

- g：全局模式（global），即模式将被应用于所有字符串，在发现第一个匹配项后继续查找。
- i：不区分大小写模式（case-insensitive），在确定匹配项是忽略模式与字符串的大小写。
- m：多行模式（multiline），在到达一行文本末尾时还会继续查找下一行中是否存在与模式匹配的项。

正则表达式就是一个模式与上述3个标志的组合体。不同组合产生不同结果，如下例子：

```javascript
// 字面量形式定义正则表达式
var pattern1 = /[bc]at/i;

// 构造函数定义正则
var pattern2 = new RegExp("[bc]at", "i");
```

pattern1 与 pattern2 是完全等价的两个正则表达式。

**⚠️ 传递给构造函数的两个参数时字符串（不能吧字面量传递给 RegExp 构造函数）。由于 RegExp 构造函数的模式参数时字符串，所以在某些情况下要对字符串进行双重转义。 _所有字符串都必须双重转义_ 那些已经转义过的字符也是如此。**


| 字面量模式 | 等价的字符串 |
| :-: | :-: |
| /\[bc\]at/ | “\\[bc\\]at” |
| /\.at/ | “\\.at” |
| /name\/age/ | “name\\/age” |
| /\d.\d{1,2}/ | “\\d.\\d{1,2}” |

使用字面量和使用 RegExp 构造函数 区别：**使用字面量始终会共享同一个 RegExp 实例，而使用构造函数创建的每一个新 RegExp 实例都是一个新实例。**

#### RegExp 实例属性

RegExp 的每个实例都具有下列属性，通过这些属性可以去的有关模式的各种信息。

- global： boolean，表示是否设置了 g 标志。
- ignoreCase：boolean，表示是否设置了 i 标志。
- lastIndex：int，表示开始搜索下一个匹配项的字符位置，从0算起。
- multiline：boolean，表示是否设置了 m 标志。
- source： 正则表达式的字符串表示，按照字面量形式而非传入构造函数中的字符串模式返回。

### 3、Function类型

在 ECMAScript 中每个函数都是 Function 类型的实例，而且都与其他引用类型一样具有属性和方法。**函数都是对象，函数名实际上也是一个指向函数对象的指针，不会与某个函数绑定。**

函数通常使用函数声明语法定义。如下：


```javascript
function sum(num1, num2) {
    return num1 + num2;
}

// 等价于
let sum = function(num1, num2) {
    return num1 + num2;
}
```

#### 3.1、函数没有重载

在 Java 中函数方法都有重载的概念，而在 ECMAScript 中没有函数重载的概念，将函数名想象为指针更好理解。声明同名函数，相当于为同一个变量重复赋值，


#### 3.2、函数声明与函数表达式

函数声明和函数表达式实际上，解析器在向执行环境中加载数据时，解析器会率先读取函数声明，并使其在执行任何代码之前可用；函数表达式，必须等到解析器执行到他所在的代码行，才会真正被解释执行。


```javascript
console.log(sum(10, 20));       // => 30
function sum(num1, num2) {
  return num1 + num2;
}

//-上下对比---⬆-函数声明----⬇-函数表达式---

console.log(sum2(10, 20));      // => TypeError: sum2 is not a function
var sum2 = function (num1, num2) {
  return num1 + num2;
}
```

由以上示例可以看出，下面的函数，在执行到函数所在的语句之前，变量 sum2 不会保存对函数的引用，所以会报语法错误；而上面的函数声明因为存在变量提升（function declaration hoisting），所以可以正常运行。

#### 3.3、作为值的函数

因为函数名本身就是变量，所以函数也可以作为值来使用。

1. 函数可当作参数传递给另一个函数；
2. 函数可作为另一个函数的结果返回。

```javascript
function callSomeFunction(someFunc, someArgs) {
    return someFunc(someArgs);
}
```


### 4、基本包装类型


















### 5、单体内置对象


















