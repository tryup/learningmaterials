http://doc.qt.io/qt-4.8/examples-webkit.html



##一些记录
###QTWEBKIT URL双重URLENCODE问题
··通过QTWEBKIT在发送请求URL参数时，自动进行了一次URLENCODE。
通过QURL(QString) 构造函数来初始化QURL，其中QString已经经过URLENCODE，故发出去的数据实际经过了双重URL。
由于对QT不熟，GOOGLE之，发现有若干网友有相同问题。
http://stackoverflow.com/questions/19605510/disable-url-encoding-of-the-query-string-in-qtkwebit/
查询QT文档之后，发现有几个接口可以使用
http://doc.qt.io/qt-4.8/qurl.html#setEncodedUrl
QURL.setEncodedUrl 故解决，并且回答了下问题。。一个做服务器的人竟然要搞QT ╮(╯▽╰)╭··

