## 第一部分 JavaScript 编程语言

## 02 JavaScript 基础知识

### `<script>` 标签

- 使用独立文件的好处是浏览器会下载它，然后将它保存到浏览器的缓存中
- 如果设置了 src 属性，script 标签内的内容将被忽略

### 代码结构

- 语句
- 分号
  - 错误例子
  ```js
  alert("hello")
  [1,2].forEach(alert);
  ```
- 注释

### `"use strict"` 模式

- 请确保`"use strict"` 出现在脚本的最顶部，否则严格模式可能均未启用。只有注释可以出现在 `"use strict"` 的上面
- 开发者控制台默认不启动 `"use strict"`
- 现代 JavaScript 支持 `class` 和 `module`，它们会默认启用 `use strict`

### 变量

- 变量声明、变量赋值
- `let`, `const`, `var`
- 标识符（变量命名）
- 保留字
- 常量

### 数据类型

- 动态类型：定义后的变量，并不会被限制为某一固定类型
- 8 种基本数据类型（7 和原始类型 + 1 种引用类型）
  - Number: 用于任何类型的数字：整数或浮点数，在 +-（2**53 - 1）范围
    - 特殊值：Infinity, -Infinity, NaN
      - 如果在数学表达式中有一个 `NaN`，最终结果也会是 `NaN`。只有一个例外：`NaN ** 0 结果为 1`
  - BigInt: 表示任意长度的整数。通过将 `n` 附加到整数的末尾来创建 `BigInt` 的值
  - String
    - 字符串必需被括在引号内（双引号、单引号、反引号）
  - Boolean: true 或 false
  - null: 用于未知的值。代表无，空或者值未知的特殊值
  - undefined：未被赋值。如果一个变量已经声明，但未被赋值，那么它的值就是 undefined
  - Object
  - Symble: 用于唯一的标签符

**typeof 运算符**

语法：typeof x 与 typeof(x) 相同。typeof 是一个操作符，不是一个函数。这里的括号还是 typeof 的一部分，它是数学运算分组的括号。

```js
typeof undefined  // "undefined"
typeof 0          // "number"
typeof 10n        // "bigint"
typeof true       // "boolean"
typeof "foo"      // "string"
typeof Symbol('id') // "symbol"
typeof Math       // "object"
typeof null       // "object"
typeof alert      // "function"
```

### 交互：alert, prompt, confirm

```js
// 显示一条信息，并等待用户按下 "OK"
alert('Hello')
// 显示一个带有文本消息的窗口，还有 input 框和确定取消按钮。取消返回 null
// title 显示组用户的文件，default 可选的第二个参数，指定 input 的初始值
let result = prompt(title, [defult])
// 显示一个带有 question 以及确定和取消按钮的窗口，确定返回 true，取消取回 false
let result = confirm(question)

这些方法是模态的：它们暂停脚本的执行，并且不允许用户与该页面的其余部分进行交互，直到窗口被解除。

```

### 类型转换

> 字符串转换

- 显示调用 String(value)，false 变成 "false"，null 变成 "null"
- alert(value) 会直接将 value 转变为字符串

> 数字型转换

- 在算术函数和表达式中，会自动进行 number 类型转换。比如 `alert("6" / "2")` 结果为 3
- 显示调用 Number(value)。 如果 value 不是一个有效的数字，转换结果为 NaN。如 `alert(Number("Hello"))`
- 转换规则

| 值   | 变成    |
|--------------- | --------------- |
| undefined   | NaN   |
| null   | 0   |
| true 和 false   | 1 and 0   |
| string   | 读取字符串，两端的空白字符（空格，换行符 \n，制表符 \t 等）会被忽略。空字符串变成 0。转换出错则输出 NaN   |

> 布尔类型转换

- 它发生在逻辑运算中，也可以通过显示调用 Boolean(value) 来进行转换
- 转换规则如下
  - 直观上为空值（如0，空字符串，null，undefined, 和 NaN）将变为 false
  - 其它值变成 true

### 基础运算符，数学运算

- 运算元：运算符应用的对象。比如 5 * 2，有两个运算元。如果一个运算符对应的只有一个运算元，那么它是一个一元运算符。

> 数学运算符

`+, -, *, /, 取余 %, 示幂 **`


> 连接字符串，二元运算符 +

- 只要任意一个运算元是字符串，那么另一个运算元也将被转化为字符串
- 二元 + 是支持字符串的运算符。其它算术运算符只对数字起作用，并且总是将其它运算元转换为数字。
- 例子
  ```js
  alert(2 + 2 + '1'); // '41'，不是 '221'
  alert('1' + 2 + 2); // '122'，不是 '14'
  alert(6 - '2');     // 4
  alert('6' / '2');   // 3
  ```

> 数字转化，一元运算符 +

+value, 放在值的前面，与 Number(value) 相同

> 运算符优先级

- 一元运算符优先级高于二元运算符

> 赋值运算符

- 链式赋值（chaining assignments)
  ```js
  let a, b, c;
  a = b = c = 2 + 2;
  ```

> 自增/自减

- 后置模式：运算符置于变量后
- 前置模式：运算符置于变量前
- ++/-- 优先级比大多数算数运算符都要高

> 位运算符

- 位运算符把运算元当作 32 位整数，并在它们的二进制表现形式上操作。
- 按位与 ( & )
- 按位或 ( | )
- 按位异或 ( ^ )
- 按位非 ( ~ )
- 左移 ( << )
- 右移 ( >> )
- 无符号右移 ( >>> )

> 逗号运算符

- 逗号运算符能让我们处理多个表达式，使用 , 将它们分开。每个表达式都运行了，但是只有最后一个的结果会被返回。
  ```js
  let a = (1 + 2, 3 + 4);
  alert(a);   // 7, (3 + 4 的结果)
  // 一行上有三个运算符
  for (a = 1, b = 3, c = a * b; a < 10; a++) {
  ...
  }
  ```

### 值的比较

> 字符串比较

- 在比较字符串大小时，JavaScript 会使用字典（dictionary）或词典(lexicographical) 顺序进行判定
- 字符串比较（首位字符大小；如果前几位相等，还有未比较字符的字符串更大）

> 不同类型间的比较

- 当对不同类型的值进行比较时，JavaScript 会首先将其转化为数字再判定大小
- 对于布尔类型，true 会被转化为 1, false 会被转化为 0
- 奇怪的现象
  ```js
  let a = 0;
  alert( Boolean(a) ); // false
  let b = "0";
  alert( Boolean(b) ); // true
  alert(a == b); // true!
  ```

> 严格相等

- 严格相等运算符 `===` 在进行比较时不会做任何的类型转换

> 对 `null` 和 `undefinec` 进行比较

```js
null == undefined   // true
null === undefined  // false
```

- 当使用数学式或其它比较方式 < > <= >= 时，null/undefined 会被转化为数字: null 被转化为 0, undefined 被转化为 NaN

```js
alert( null > 0 );  // (1) false
alert( null == 0 ); // (2) false
alert( null >= 0 ); // (3) true

```

为什么会出现这种反常结果，这是因为相等性检查 == 和普通比较符 > < >= <= 的代码逻辑是相互独立的。进行值的比较时，null 会被转化为数字，因此它被转化为了 0。这就是为什么（3）中 null >= 0 返回值是 true，（1）中 null > 0 返回值是 false。

另一方面，undefined 和 null 在相等性检查 == 中不会进行任何的类型转换，它们有自己独立的比较规则，所以除了它们之间互等外，不会等于任何其他的值。这就解释了为什么（2）中 null == 0 会返回 false。

> 特立独行的 undefined

- undefined 不应该被与其他值进行比较

```js
alert( undefined > 0 ); // false (1)
alert( undefined < 0 ); // false (2)
alert( undefined == 0 ); // false (3)

```
(1) 和 (2) 都返回 false 是因为 undefined 在比较中被转换为了 NaN，而 NaN 是一个特殊的数值型值，它与任何值进行比较都会返回 false。
(3) 返回 false 是因为这是一个相等性检查，而 undefined 只与 null 相等，不会与其他值相等。

### 条件分支： if 和三元运算符 

### 逻辑运算符

> || 或

- 或运算符返回第一个真值；如果不存在真值，就返回该链的最后一个值
  ```js
  alert( 1 || 0 ); // 1（1 是真值）
  alert( null || 1 ); // 1（1 是第一个真值）
  alert( null || 0 || 1 ); // 1（第一个真值）
  alert( undefined || null || 0 ); // 0（都是假值，返回最后一个值）
  ```
- 短路求值（short-circuit evaluation)
  - 如果操作数不仅仅是一个值，而是一个有副作用的表达式，例如变量赋值或函数调用。
  ```js
  true || alert("not printed");
  false || alert("printed");
  ```

  在第一行中，或运算符 || 在遇到 true 时立即停止运算，所以 alert 没有运行。
  有时，人们利用这个特性，只在左侧的条件为假时才执行命令。

> && 与

- 与运算寻找第一个假值；如果不存在假值，就返回第一个真值。

> ! 非
















