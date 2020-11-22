
<!--more-->

> 首发 [https://zhanghao1github.github.io/](https://zhanghao1github.github.io/)

只是加密的话，将.py源码转换成du.pyc的字节码文件就可以了。

最简单的用例是，假设自己写了个my_lib.py文件，在main.py中import，运行：

```python
# File: main.py
import my_lib
...
```

然后会发现当前目录下生成了my_lib.pyc文件。把my_lib.py文件移到别处，只保留my_lib.pyc的情况下，main.py也可以正常运行。

my_lib.pyc就是题主需要的“加密”版本。
在明白了原理以后，也可以用命令直接生成.pyc文件：

```shell
python -m compileall my_lib.py
```

就可以得到my_lib.pyc了。