

==
###标题测试


```
H1
===
H2
----
###H3
####H4
#####H5
######H6
#######H7是啥
```


H1
===


H2
----
###H3
####H4
#####H5
######H6
#######H7是啥
****
###链接测试

[内联链接带属性1](http://github.com/tryup "我的git")

[内联链接带属性2](http://www.ifobnn.com '我的博客')

[内敛链接不带属性](http://github.com/tryup)

[隐藏式][]测试

[隐藏式]: http://www.ifobnn.com

[参考式][3]

[3]: http://www.google.com "Google"

----------
###段落测试
这个是一个段落很长很**长很长很长很**长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很[长很][3]长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长，会不会自动换行。

这个是一个新段落只有一行。

这个是一个新段落，我要换行了  
换行完毕。

****
###强调测试

`__FOBNN__` : __FOBNN__
`*fobnn*` : *fobnn*
`**fobnn**` : **fobnn**

-----

###代码测试
	int main()
	{
	  std::cout<<"hello fobnn"<<std::endl;
	  return 0;
	}

```c++
int main()
{
    //代码高亮扩展
    std::cout<<"hello github.com"<<std::endl;
}
```
*****
###引用测试
>[参考式][3]
>
>[3]: http://www.google.com "Google"
>
>###段落测试
>这个是一个段落很长很长很长很**长很长很长**很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长，会不会自动换行。
>
>这个是一个新段落只有一行。
>
>这个是一个新段落，我要换行了  
>换行完毕。
>
>###强调测试
>`_FOBNN_` ：_FOBNN_
>`__FOBNN__` : __FOBNN__
>`*fobnn*` : *fobnn*
>`**fobnn**` : **fobnn**

***
###GFM测试

####表格
| *表头1* | 表头2   |
| :---: | ----- |
|  单元1  | `单元2` |

####代码高亮

```go
package main

import "fmt"

func main(){
  fmt.Println('hello fobnn')
}
```

```c++
#include<iostream>
class fobnn
{
  public:
    fobnn(){};
    friend ostream& operator<<(const ostream& os)
    {
      os << "hello fobnn"<<std::endl;
      return os;
    }
};
```
####删除线(Strikethrough)
~~我宣布！这句话被否决了！~~

####emoji
​:joy:​

####前方高能！！任务表，TODOLIST？

2016年目标如下：
-  [x] 学习分布式系统原理
-  [ ] 每天记3个单词​:joy:​
-  [ ] Golang掌握
-  [x] ​