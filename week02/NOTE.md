# 第二周总结

## 编程语言通识

### 语言按语法分类

- 非形式语言
- 形式语言（乔姆斯基谱系）
	* 0型 无限制文法
		+ ?::=?
	* 1型 上下文相关文法
		+ ?<A>?::=?<B>?
		+ {
			+ get a{return 1}
			+ get:1
		}
	* 2型 上下文无关文法
		+ <A>::=?
		+ 2 ** 1 ** 2
	* 3型 正则文法
		+ <A>::=<A>? 左递归
		+ <A>::=?<A> 有递归 不符合
- 产生式
	* 用尖括号括起来的名称表示语法结构名
	* 语法结构分成基础结构和需要用其他语法结构定义的复合结构
		+ 基础结构称终结符
		+ 符合结构称非终结符
	* 引号和中间的字符表示终结符
	* 可以有括号
	* *表示重复多次
	* |表示或
	* +表示至少一次

### 图灵完备性
- 图灵完备性
	* 世界上的一切，并不是都可以通过计算得出结果
	* 命令式 - 图灵机
		+ goto
		+ if while
	* 声明式 - lambda
		+ 递归

### 动态与静态
- 动态
	* 在用户的设备/在线服务器上
	* 产品实际运行时
	* Runtime
- 静态
	* 在程序员的设备上
	* 产品开发时
	* Compiletime

### 类型系统
- 动态类型系统与静态类型系统
- 强类型与弱类型
	* String + Number
	* String == Boolean
- 复合类型
	* 结构体
	* 函数签名
- 子类型
	* 逆变/协变
	* 凡是能用 Array<Parent>的地方，都能用 Array<Child>
	* 凡是能用 Function<Child>的地方，都能用 Function<Parent>


### Unicode
- 范围非常广，几乎世界各国的字符都有
- JS 使用的时 Unicode 字符集

- block
	* 前 128 位，兼容 ASCII 字符  U+0000 U+007F
	* String.fromCharAt(65)		// a
	* BMP 字符  U+FFFF 之前的字符
	* 中文  \u 转移
	* "厉害".codePointAt(0).toString(16)		// 5389
	* "厉害".codePointAt(1).toString(16)		// 5bb3
	* charCodeAt
	* fromCharCode
	* \u5389\u5bb3  相当于 "厉害"

- category
	* Separator,Space
	* U+0020 space


### InputElement
##### WhiteSpace
- <TAB>	U+0009
- <SP>
- <NBSP>		no break 作用，两个单词一起换行
- <ZWNBSP>	zero width	U+FEFF
- <FF>		Form Feed 换页
- <VT>		纵向制表符（没什么用）
##### LineTerminator
- <LF>	line feed  U+000A
- <CR>	carriage return U+000D
- \r\n 历史遗留问题，换页、换行
##### Comment
- //
- /**/
##### Token
- 有效的东西都是token
- Punctuator	符号
- IdentifierName	变量名 属性名
	* keywords		关键词
	* Identifier
	* Future reserved keywords : emun
- Literal
	* Number
		+ IEEE 754 Double Float
		+ Sing（1）
		+ Exponent（11）
		+ Fraction（52）
		+ 0o10 == 8
		+ 0x10 == 16
		+ 0b10 == 2
		+ 0
		+ 0.
		+ .0
		+ 1e3
		+ Safe Integer  Number.MAX_INTEGER.toString(16)  1fffffffffffff
		+ Float Compare Math.abs(0.1+0.2-0.3) <= Number.EPSILON
		+ 97 .toString(2)  	加空格原因	97. 是合法的Number
	* String
		+ ASCII
		+ Unicode UTF-8 超出ASCII三个字节；UTF-16 两个字节
		+ UCS 	U+0000 - U+FFFF
		+ GB - GB2312 GBK(GB13000) GB18030  只有ASCII和大部分中文
		+ IOS-8859	欧洲文字
		+ BIG5 繁体中文
		+ "abc"
		+ 'abc'
		+ \ 转义  n r t f \ ' " v(垂直制表，大部分没用) b(退格，大部分没用)
		+ `ab${ s }c` 模板字符串拆成了三个部分
	* Boolean
		+ true false
	* Null
	* Undefined
	* Object
	* Symbol

> ps: undefined 局部作用域可以修改值
> ps: / 能为除号就是除号，之后才会判断是否是正则

### 一般命令式编程语言

- Atom
	* Identifier
	* Literal

- Expression
	* Atom
	* Operator
	* Punctuator

- Statement
	* Expression
	* Keyword
	* Punctuator

- Structure
	* Function
	* Class
	* Process
	* Namespace
	* ...

- Program
	* Program
	* Module
	* Package
	* Library



