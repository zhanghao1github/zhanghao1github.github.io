
<!--more-->

> 首发 [https://zhanghao1github.github.io/](https://zhanghao1github.github.io/)



```python
import subprocess
import os
import time
```



```python
class Git:
    def __init__(self, filePath='./'):
        self.filePath = filePath

    def runCmd(self, cmd):
        SECONDS_TIMEOUT = 10000
        p = subprocess.Popen(
            cmd, shell=True, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
        try:
            p.wait(timeout=SECONDS_TIMEOUT)
        except Exception as e:
            p.kill()
            print("===== process timeout ======")
            print(e)
            print("===== process timeout ======")
            return None
        result = p.communicate()
        try:
            res = result[0].decode(encoding='gbk', errors='strict')
        except:
            try:
                res = result[0].decode(encoding='utf-8', errors='strict')
            except:
                res = result[0]
        print(res)
        return res

    def getBranchFromFileConfig(self):
        with open('.git/config') as fp:
            content = fp.read()
            return content[content.index('[branch "') + 9:content.find('"]', content.index('[branch "'))]

    def update(self):
        text = "python自动更新" + \
            str(time.strftime("%Y-%m-%d-%H:%M:%S", time.localtime()))
        branch = self.getBranchFromFileConfig()
        self.runCmd('git add .')
        self.runCmd('git commit -m '+text)
        self.runCmd('git pull --rebase origin '+branch)
        self.runCmd('git push origin '+branch)

```

