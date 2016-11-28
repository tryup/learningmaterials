### 0.背景

目前在做的一个项目中用到了qtwebkit用于检测domxss。其中一个Attack Vector是 
```
xxxx.com/?s=<xxx>ssss<xxx>
```
形式。在IE中<>不会进行urlencode进行GET请求，而在webkit中<>会被urlencode成

%3C%3E。故在某些情况下playload失效。


查询[RFC](https://www.w3.org/html/ig/zh/wiki/URL#.E5.90.88.E6.B3.95.E7.9A.84_URL)、[STD68](https://www.ietf.org/rfc/std/std68.txt)中说明。

[QT-QURL](http://doc.qt.io/qt-4.8/qurl.html#ParsingMode-enum)文档setEncodedUrl接口中说道。

>In TolerantMode, the parser corrects the following invalid input:
>Spaces and "%20": If an encoded URL contains a space, this will be replaced with "%20". If a decoded URL contains "%20", this will be replaced with a single space before the URL is parsed.
>Single "%" characters: Any occurrences of a percent character "%" not followed by exactly two hexadecimal characters (e.g., "13% coverage.html") will be replaced by "%25".
>Reserved and unreserved characters: An encoded URL should only contain a few characters as literals; all other characters should be percent-encoded. In TolerantMode, these characters will be automatically percent-encoded where they are not allowed: space / double-quote / "<" / ">" / "[" / "" / "]" / "^" / "`" / "{" / "|" / "}"

###1.解决方案
只能hacking使`<>`合法，仅仅针对本次事件进行hack，不具备太大的参考价值。PS: 本项目QT版本是4.8，QT5应该已经移除(deprecated)下面的接口，可以使用相同方法修改。
1. 修改Qurl.cpp。
```C++
void QUrl::setEncodedUrl(const QByteArray &encodedUrl, ParsingMode parsingMode)
{
=====================省略部分代码==================

// Reserved and unreserved characters are fine
//         unreserved    = ALPHA / DIGIT / "-" / "." / "_" / "~"
//         reserved      = gen-delims / sub-delims
//         gen-delims    = ":" / "/" / "?" / "#" / "[" / "]" / "@"
//         sub-delims    = "!" / "$" / "&" / "'" / "(" / ")"
//                         / "*" / "+" / "," / ";" / "="
        // Replace everything else with percent encoding
        //static const char doEncode[] = " \"<>[\\]^`{|}";  原始代码
        //static const char doEncodeHost[] = " \"<>\\^`{|}";
        static const char doEncode[] = " \"[\\]^`{|}";
        static const char doEncodeHost[] = " \"\\^`{|}";
        for (int i = 0; i < tmp.size(); ++i) {
            quint8 c = quint8(tmp.at(i));
            if (c < 32 || c > 127 ||
                strchr(hostStart <= i && i <= hostEnd ? doEncodeHost : doEncode, c)) {
                char buf[4];
                buf[0] = '%';
                buf[1] = toHex(c >> 4);
                buf[2] = toHex(c & 0xf);
                buf[3] = '\0';
                tmp.replace(i, 1, buf);
                i += 2;
            }
        }
    }

    d->encodedOriginal = tmp;
}
```
上面修改之后还要通过IsVaild验证，故修改。
```C++
// pchar         = unreserved / pct-encoded / sub-delims / ":" / "@"
static bool QT_FASTCALL _pchar(const char **ptr)
{
    char c = *(*ptr);

    switch (c) {
    case '!': case '$': case '&': case '\'': case '(': case ')': case '*':
    case '+': case ',': case ';': case '=': case ':': case '@':
    case '-': case '.': case '_': case '~': case '<': case '>'://  <=增加 <>
        ++(*ptr);
        return true;
    default:
        break;
    };
    //省略代码
}
```
修改完毕之后需要重新编译qtcore。

2. 修改webkit/webcore/kurl.cpp将characterClassTable表中的`<>`映射改为SchemeChar(原来为BadChar)通过kurl `parse`时的验证，从而不执行`appendEscapingBadChars`。
```C++
static const unsigned char characterClassTable[256] = {
    /* 0 nul */ PathSegmentEndChar,    /* 1 soh */ BadChar,
    /* 2 stx */ BadChar,    /* 3 etx */ BadChar,
    /* 4 eot */ BadChar,    /* 5 enq */ BadChar,    /* 6 ack */ BadChar,    /* 7 bel */ BadChar,
    /* 8 bs */ BadChar,     /* 9 ht */ BadChar,     /* 10 nl */ BadChar,    /* 11 vt */ BadChar,
    /* 12 np */ BadChar,    /* 13 cr */ BadChar,    /* 14 so */ BadChar,    /* 15 si */ BadChar,


    /* 60  < */ SchemeChar,    /* 61  = */ UserInfoChar,
    /* 62  > */ SchemeChar,    /* 63  ? */ PathSegmentEndChar | BadChar,
```
重新编译webkit。
3. 重新编译项目工程， 成功~~~。

###2.总结
其实修改很快，充分利用代码阅读工具和callstack即可找到目标，然后理解流程。其实这次修改花时间最多的还是相关RFC的查找，以及修改之后影响的评估。
