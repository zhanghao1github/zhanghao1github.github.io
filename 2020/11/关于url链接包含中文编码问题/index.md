


<!--more-->

> 首发 [https://zhanghao1github.github.io/](https://zhanghao1github.github.io/)

有的网址进行数据爬取时需要对地址栏中文进行处理,比如(汽车之家, 爱卡汽车), 有的不需要处理(如百度知道),同时网站采取的编码方式不一样,也要注意编码的格式(utf-8, gbk), 处理后的结果是不一样的

[来源](https://blog.csdn.net/supramolecular/article/details/82149591)

[来源](https://www.liangzl.com/get-article-detail-40507.html)

```python
import urllib
import urllib.request #必须写，python3的urllib不会自动导入其under层的包，需要手动导入不引用报错
keyword = '奥迪'
kwd = urllib.parse.quote(keyword, encoding='utf-8', errors='replace')
print(kwd)#  %E5%A5%A5%E8%BF%AA
kwd = urllib.parse.quote(keyword, encoding='gbk', errors='replace')
print(kwd)#  %B0%C2%B5%CF
```

# 网址链接中的中文编码

[来源](https://blog.csdn.net/mouday/article/details/80278938)

- 中文的gbk(GB2312)编码： 一个汉字对应两组%xx，即%xx%xx
- 中文的UTF-8编码： 一个汉字对应三组%xx，即%xx%xx%xx

可以利用百度进行URL编码解码 默认gbk

```
https://www.baidu.com/s?wd=%E4%B8%AD%E5%9B%BD
```

# python3编码解码示例

```python
from urllib.request import quote, unquote

# 编码

url1 = "https://www.baidu.com/s?wd=中国"

# utf8编码，指定安全字符
ret1 = quote(url1, safe=";/?:@&=+$,", encoding="utf-8")
print(ret1)
# https://www.baidu.com/s?wd=%E4%B8%AD%E5%9B%BD

# gbk编码
ret2 = quote(url1, encoding="gbk")
print(ret2)
# https%3A//www.baidu.com/s%3Fwd%3D%D6%D0%B9%FA


# 解码
url3 = "https://www.baidu.com/s?wd=%E4%B8%AD%E5%9B%BD"

ret3 = unquote(url3, encoding='utf-8')
print(ret3)
# https://www.baidu.com/s?wd=中国
```

