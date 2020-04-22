## 写一个正则表达式 匹配所有Number直接量

### 最终结果

* NumbericLiteral的正则表达式：

```
^(((0|[1-9]\d*)\.(\d+)([eE][\+\-]?\d+))|\.(\d+)([eE][\+\-]?\d+)|(0|[1-9]\d*)([eE][\+\-]?\d+))|(0[bB][01]+)|(0[oO][0-7]+)|(0[xX][0-9a-fA-F]+)$
```

### 分析过程：

**从最基础的开始，一步一步构建**

1. 首先，对于**十进制整数**有如下分析过程：

>  DecimalDigit :: one of
>
>    	 0 1 2 3 4 5 6 7 8 9

* 即 DecimalDigit：

  ```
  ^\d$
  ```

> NonZeroDigit :: one of
> 		1 2 3 4 5 6 7 8 9

* 即 NonZeroDigit：

  ```
  ^[1-9]$
  ```

> DecimalDigits ::
> 		DecimalDigit
> 		DecimalDigits DecimalDigit

* 即 DecimalDigits：

  ```
  ^\d+$
  ```

> DecimalIntegerLiteral ::
> 		0
> 		NonZeroDigit DecimalDigits

* 即 DecimalIntegerLiteral：

  ```
  ^0|[1-9]\d*$
  ```

> ExponentIndicator :: one of
> 		e E

* 即 ExponentIndicator：

  ```
  ^[eE]$
  ```

>  SignedInteger ::
>
> ​		DecimalDigits
>
> ​		\+ DecimalDigits
>
> ​		\- DecimalDigits

* 即 SignedInteger：

  ```
  ^[\+\-]?\d+$
  ```

> ExponentPart ::
> 		ExponentIndicator SignedInteger

* 即 ExponentPart：

  ```
  ^\[eE\]\[\+\\-]?\d+$
  ```

> DecimalLiteral ::
> 		DecimalIntegerLiteral . DecimalDigitsopt ExponentPartopt
> 		. DecimalDigits ExponentPartopt
> 		DecimalIntegerLiteral ExponentPart

* 综上，可得 Decimal Literal：

```
^((0|[1-9]\d*)\.(\d+)([eE][\+\-]?\d+))|\.(\d+)([eE][\+\-]?\d+)|(0|[1-9]\d*)([eE][\+\-]?\d+)$
```



2. 对于二进制整数，稍微简单一点

> BinaryDigit :: one of
> 		0 1

* 即 BinaryDigit：

  ```
  ^[01]$
  ```

> BinaryDigits ::
> 		BinaryDigit
> 		BinaryDigits BinaryDigit

* 即 BinaryDigits： 

  ```
  ^[01]+$
  ```

> BinaryIntegerLiteral ::
> 		0b BinaryDigits
> 		0B BinaryDigits

* 综上可得 BinaryIntegerLiteral：

```
^0[bB][01]+$
```



3. 对于八进制数，与二进制数的分析过程类似，有如下分析：

> OctalDigit :: one of
> 		0 1 2 3 4 5 6 7

* 即 OctalDigit： 

  ```
  ^[0-7]$
  ```

> OctalDigits ::
> 		OctalDigit
> 		OctalDigits OctalDigit

* 即 OctalDigits： 

  ```
  ^[0-7]+$
  ```

> OctalIntegerLiteral ::
> 		0o OctalDigits
> 		0O OctalDigits

* 综上可得 OctalIntegerLiteral：

```
^0[oO][0-7]+$
```



4. 对于十六进制数，与二进制和八进制的分析过程类似，有如下分析：

> HexDigit :: one of
>
> ​		0 1 2 3 4 5 6 7 8 9 a b c d e f A B C D E F

* 即 HexDigit： 

  ```
  ^[0-9a-fA-F]$
  ```

> HexDigits ::
> 		HexDigit
> 		HexDigits HexDigit

* 即 HexDigits： 

  ```
  ^[0-9a-fA-F]+$
  ```

> HexIntegerLiteral ::
> 		0x HexDigits
> 		0X HexDigits

* 综上可得 HexIntegerLiteral

```
^0[xX][0-9a-fA-F]+$
```



5. 最后，针对NumbericLiteral

> NumericLiteral ::
> 		DecimalLiteral
> 		BinaryIntegerLiteral
> 		OctalIntegerLiteral
> 		HexIntegerLiteral

* 综合以上四个步骤的分析结果，有NumbericLiteral的正则表达式：

```
^(((0|[1-9]\d*)\.(\d+)([eE][\+\-]?\d+))|\.(\d+)([eE][\+\-]?\d+)|(0|[1-9]\d*)([eE][\+\-]?\d+))|(0[bB][01]+)|(0[oO][0-7]+)|(0[xX][0-9a-fA-F]+)$
```

* **以上即为最终的结果**