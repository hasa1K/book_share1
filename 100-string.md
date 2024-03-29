### 1.什么是rune
在Unicode中，使用一个概念代码点去表示一个单值。在Go中，rune就是一个代码点。所以在Go中，一个rune就是int32的别名。
由于Go语言中采用的是统一的UTF-8编码，英文字母在底层占1个字节，特殊字符和中文汉字则占用1～3个字节，在Go语言中文的计数和截取并不如其他语言（比如Python）那么容易，所以Go提供了 rune 类型来处理中文的计数和分割问题，以支持国际化多语言。


### 2. 为什么用s1[:5]这种形式来切割字符串可能会造成内存泄漏

```golang
s1 := "aaaaa bbbbb"
s2 := s1[:5] // aaaaa
```
如果s2一直被引用，则s1永远无法被gc回收。
可以采取string([]byte(s1[:5])), go1.18之后可以采取strings.Clone函数方式

![image](https://github.com/hasa1K/book_share1/assets/53266479/9f215960-2066-440e-b18c-3f3f5b4dc37b)
