
# Git 常用操作

## git clone命令

#####  1. git clone git@github.com:用户名/仓库名.git

```shell
git clone git@github.com:zhanghao1github/testTo1.git
```

- 不要clone空仓库，主分支不同，容易报错，未明白具体原因

## Git 更新

#####  1. 切换目录到.git文件夹内

```shell
ls
cd  文件夹名（tab）
#git remote -v  #查看远程连接
```

##### 2. git add <文件名>

```shell
git add . #更新全部
```

##### 3. git commit -m "说明日志"

```shell
git commit -m "说明日志"
```

## Git 更新到远程github

##### git push -u origin main

```shell
git push -u origin main
```

## Git 初始化命令

```shell
git init


git add .
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:zhanghao1github/test.git
git push -u origin main
```

