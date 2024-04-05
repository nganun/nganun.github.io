## 第一部分 JavaScript 编程语言

### 02 JavaScript 基础知识

> `<script>` 标签

- 使用独立文件的好处是浏览器会下载它，然后将它保存到浏览器的缓存中
- 如果设置了 src 属性，script 标签内的内容将被忽略

> 代码结构

- 语句
- 分号
  - 错误例子
  ```js
  alert("hello")
  [1,2].forEach(alert);
  ```
- 注释

> `"use strict"` 模式

- 请确保`"use strict"` 出现在脚本的最顶部，否则严格模式可能均未启用。只有注释可以出现在 `"use strict"` 的上面
- 开发者控制台默认不启动 `"use strict"`
- 现代 JavaScript 支持 `class` 和 `module`，它们会默认启用 `use strict`

> 变量

- 变量声明、变量赋值
- `let`, `const`, `var`
- 标识符（变量命名）
- 保留字
- 常量

> 数据类型

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




