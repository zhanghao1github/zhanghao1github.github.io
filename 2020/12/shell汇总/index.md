
<!--more-->

> 首发 [https://zhanghao1github.github.io/](https://zhanghao1github.github.io/)

```shell
# 当前应用小窗化的命令
a=$(dumpsys window|grep mFocusedWindow|grep -o "[^ ]*/[^}]*")
input keyevent 3
am start --windowingMode 5 -n $a

```

