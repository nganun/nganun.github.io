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
| string   | 去掉首尾空白字符（空格、换行符、制表符等）后的纯数字字符串中含有的数字。如果剩余字符串为空，结果为0。否则，将从剩余字符串中读取数字。当类型转换出现 error 时返回 NaN   |

> 布尔类型转换







