
<!--more-->

> 首发 [https://zhanghao1github.github.io/](https://zhanghao1github.github.io/)

## 【Python】获取文件夹下的所有文件路径（包括子目录下的文件路径）

```python
def get_all_path(open_file_path):
    rootdir = open_file_path
    path_list = []
    list = os.listdir(rootdir)  # 列出文件夹下所有的目录与文件
    for i in range(0, len(list)):
        com_path = os.path.join(rootdir, list[i])
        #print(com_path)
        if os.path.isfile(com_path):
            path_list.append(com_path)
        if os.path.isdir(com_path):
            path_list.extend(get_all_path(com_path))
    #print(path_list)
    return path_list
```

