## Hugo 安装配置文档地址：
```
https://blog.51cto.com/michaelkang/2364007
```
## 本文环境介绍
```
#hugo 版本
version
Hugo Static Site Generator v0.54.0 linux/amd64 BuildDate: 2019-02-22T08:11:04Z
#go 版本
go version go1.11.5 linux/amd64
#系统版本
more /etc/redhat-release 
CentOS Linux release 7.6.1810 (Core) 
 
#版本和环境详细信息
hugo env
 
Hugo Static Site Generator v0.54.0 linux/amd64 BuildDate: 2019-02-22T08:11:04Z
GOOS="linux"
GOARCH="amd64"
GOVERSION="go1.11.5"
```
## 初始化站点
### 始化一个站点目录
www.datals.com
```
hugo new site /www.datals.com
```
## 目录结构介绍：
```
cd /www.datals.com/
ll
 
  ▸ archetypes/ #包括内容类型，在创建新内容时自动生成内容的配置
  ▸ content/    # 网站内容，全部使用markdown格式
  ▸ layouts/    # 网站模板文件，决定内容如何呈现
  ▸ static/     # 图片、css、js 等静态资源
  ▸ themes/     # 存放主题
    config.toml   # 是网站的主配置文件
```
## 常用命令介绍
```
#使用方法:
  hugo
  hugo [flags]
  hugo [command]
  hugo [command] [flags]
#查看版本
hugo version
#版本和环境详细信息
hugo env
#创建新站点
hugo new site "$mysite"
#创建文章
hugo new index.md  
 
在content/文件夹可以看到，此时多了一个markdown格式的文件index.md，打开文件可以看到时间和文件名等信息已经自动加到文件开头，包括创建时间，页面名，是否为草稿等。
#编译生成静态文件
hugo
 
Hugo将编译所有文件并输出到public目录     
#编译生成静态文件并启动web服务
hugo server
```
## 常用参数介绍
```
  --bind="127.0.0.1"    服务监听IP地址；
  -p, --port=1313       服务监听端口；
  -w, --watch[=true]      监听站点目录，发现文件变更自动编译；
  -D, --buildDrafts     包括被标记为draft的文章；
  -E, --buildExpired    包括已过期的文章；
  -F, --buildFuture     包括将在未来发布的文章；
  -b, --baseURL="www.datals.com"  服务监听域名；
  --log[=false]:           开启日志；
  --logFile="/var/log/hugo.log":          log输出路径；
  -t, --theme=""          指定主题；
  -v, --verbose[=false]: 输出详细信息
```
## 常用使用参数组合
```
hugo server -t hyde --buildDrafts --baseURL=http://www.datals.com  --bind=0.0.0.0 --port=80 -w
 -t hyde        使用hyde主题，如果使用-t 选择了主题会将当前默认的主题覆盖；
 --buildDrafts参数将生成被标记为草稿的页面，是否发布：hugo 会忽略所有通过 draft: true 标记为草稿的文件。必须改为 draft: false 才会编译进 HTML 文件。
 --baseURL=http://www.datals.com   站点监听域名
 --bind=0.0.0.0   监听全部网段
 --port=80        服务监听端口
 -w               如果修改了网站内的信息，会直接显示在浏览器的页面上，不需要重新运行hugo server，方便我们进行修改。  
```
## hugo 命令使用方法详解
```
执行hugo命令，站点目录下会新建文件夹public/，生成的所有静态网站页面都会存储到这个目录，
如果使用Github pages来作为博客的Host，你只需要将public/里的文件上传就可以。
如果使用nginx作为web服务配置root dir 指向public/ 即可；
```