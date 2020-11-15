
<!--more-->

> 首发 [https://zhanghao1github.github.io/](https://zhanghao1github.github.io/)

# 油猴脚本小功能

### 点击一个按钮

```
$('.btn-wrap a')[0].click();
```

**注意**

```
$('.btn-wrap a').click();
```

在 chrome console 中可以触发 vuejs 的 click 事件，但是在 tampermonkey 中无法触发。

修改成

```
$('.btn-wrap a')[0].click();
```

即可。

##### 直接模拟点击比修改属性好在哪里

例如，勾选一个 checkbox 勾选框，可以这样做

```
$($('input[name=qa]')[0]).prop('checked', true);
```

但是，如果目标网站是用的 vuejs 之类的，在 input 上绑定了各种奇怪的 data，那么直接修改属性是不行的。想象一下，如果 vuejs 的 on click 里如果有 data 的操作，那么这些操作是无法由修改属性触发的。所以，模拟点击更省心一些。