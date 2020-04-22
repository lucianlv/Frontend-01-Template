## 写一个 UTF-8 Encoding 的函数

### 基本思想

* 对于一个字符串中的每个字符，首先将它的Unicode值转换为二进制，然后通过对二进制按照UTF-8的编码规则进行转换，最后得到UTF-8的编码。



### 源代码

```javascript

// 接受一个字符串，返回UTF-8编码
function Unicode2UTF8(string) {
    // result 用于记录最后的结果
    let result = '';
    // 将string的每个字符都转为二进制再进行Encode操作
    for (let ch of string) {
        // 下面开始编码操作, 为了方便查看，结果用16进制显示
        result += "0x" + parseInt(getUTF8(ch.charCodeAt().toString(2)), 2).toString(16);
    }
   
    return result;
}

// 接收一个字符串的Unicode值（二进制），转换成UTF8（二进制）并返回
function getUTF8(string) {
    // 通过字符串的不同长度判断施加何种操作
    const length = string.length
    if (length <= 7) {
        // ASCII码
        return string;
    } else if (length <= 11) {
        // 字符串前面填6个0，再从后六位抽两次
        const tempString = '000000' + string;
        const subString1 = tempString.slice(-13, -6);
        const subString2 = tempString.slice(-6);
        return '110' + subString1 + '10' + subString2;
    } else if (length <= 16) {
        // 字符串前面填6个0，再从后六位抽三次
        const tempString = '000000' + string;
        const subString1 = tempString.slice(-16, -12);
        const subString2 = tempString.slice(-12, -6);
        const subString3 = tempString.slice(-6);
        return '1110' + subString1 + '10' + subString2 + '10' + subString3;
    } else {
        // 字符串前面填6个0，再从后六位抽四次
        const tempString = '000000' + string
        const subString1 = tempString.slice(-21, -18);
        const subString2 = tempString.slice(-18, -12);
        const subString3 = tempString.slice(-12, -6);
        const subString4 = tempString.slice(-6);
        return '11110' + subString1 + '10' + subString2 + '10' + subString3 + '10' + subString4;
    }
}

Unicode2UTF8('你好');
```