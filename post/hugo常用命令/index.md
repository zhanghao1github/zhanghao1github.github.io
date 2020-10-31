
# 使用方法:
```shell
  hugo
  hugo [flags]
  hugo [command]
  hugo [command] [flags]
```

# 查看版本
```shell
hugo version
```

# 版本和环境详细信息
```shell
hugo env
```

# 创建新站点
```shell
hugo new site "$mysite"
```

# 创建文章
```shell
hugo new index.md  
hugo new /post/hugo常用命令.md

#在content/文件夹可以看到，此时多了一个markdown格式的文件index.md，打开文件可以看到时间和文件名等信息已经自动加到文件开头，包括创建时间，页面名，是否为草稿等。
#编译生成静态文件
hugo

#Hugo将编译所有文件并输出到public目录     
```

# 编译生成静态文件并启动web服务
```shell
hugo server
```

