<!--more-->

## 关于 schedule

```
┌───────────── minute (0 - 59)
│ ┌───────────── hour (0 - 23)
│ │ ┌───────────── day of the month (1 - 31)
│ │ │ ┌───────────── month (1 - 12 or JAN-DEC)
│ │ │ │ ┌───────────── day of the week (0 - 6 or SUN-SAT)
│ │ │ │ │
│ │ │ │ │
│ │ │ │ │
* * * * *
```

例如我想每天早晨 9：00 运行，`0 1 * * *`，注意这里是`UTC`时间，换成成咱们的东八区，所以就是 9：00。

**schedule 延迟 4 分钟左右**

### 首先在 git 项目下创建一个 workflow

GitHub Actions 术语。

1. workflow （工作流程）：持续集成一次运行的过程，就是一个 workflow。
2. job （任务）：一个 workflow 由一个或多个 jobs 构成，含义是一次持续集成的运行，可以完成多个任务。
3. step（步骤）：每个 job 由多个 step 构成，一步步完成。
4. action （动作）：每个 step 可以依次执行一个或多个命令（action）。

```bash
# .github/workflow/文件名.yml
# 这是基础模板
# 这个 workflow 的名字，可以随意命名
name: Node.js CI

# on触发条件
on: [push]
# 1.push事件触发workflow
# 2.如果多个事件（on: [push,pull]）
# 3.指定触发事件，可以限定分支、tag、指定文件路径（on.<push|pull_request>.<tags|branches|paths>）
#  在master分支push时触发
#   push：
#     branches:
#       - master
#     tags:
#       - v1.0.0 # 指定tags版本更新
#       - v1.*.*  #指tags版本为1.n.n都会更新
#    paths:
#       - '**.js' # 所有的js文件更新时提交触发
#       - 'doc/**'  # doc下文件发生改动触发
# 4.忽略分支、tag、某一文件    branches-ignore、tags-ignore  、paths-ignore
#    branches-ignore:
#      - dev #当提交时分支为dev 不触发
#    tags-ignore:
#      - v2   #tag为v2时不触发
# 5. 计划的工作流在默认或基本分支上的最新提交上运行。可以运行计划的工作流程的最短间隔是每5分钟一次
#   schedule:
#      - cron:  '*/5 * * * *'
#   #  * * * * * (minute (0 - 59)、hour (0 - 23)、day of the month (1 - 31)、month (1 - 12 or JAN-DEC)、day of the week (0 - 6 or SUN-SAT))
#  # *   任何值               * * * * * 每天每一分钟运行。
#  # ， 值列表分隔符      2,10 4,5 * * * 在每天的第4和5小时的第2分钟和第10分钟运行。
#  # --  取值范围              0 4-6 * * * 在第4、5和6小时的第0分钟运行。
#  # /   步长值               20/15 * * * * 从20分钟到59（每20、35和50分钟）开始，每15分钟运行一次。

jobs:
  # 所有的 job 都是并行的，但往往会有依赖关系
  # test:
  # link:
  #   needs: test link依赖test
  # 一个名为 build 的 job
  build:
    # runs-on指定运行所需要的虚拟机环境，必填
    # ubuntu-latest指定Ubuntu GitHub托管的运行程序的最新版本。
    # 也可以自己定义托管环境[self-hosted, linux, ARM32]
    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [8.x, 10.x, 12.x]

    steps:
    # 获取源码
      - name: Checkout
        uses: actions/checkout@master # 获取master代码
        with:
          persist-credentials: false
      - name: Install and Build
        run: | #执行多个命令
          npm install
          npm run build
      - name: Deploy
        uses: JamesIves/github-pages-deploy-action@releases/v3 # 写好的action
        with:
          ACCESS_TOKEN: ${{ secrets.DEPLOY_KEY }} #自定义生成key 生成步骤在下面
          BRANCH: gh-pages #操作应部署到的分支。
          FOLDER: dist #操作应部署的文件夹。
```
