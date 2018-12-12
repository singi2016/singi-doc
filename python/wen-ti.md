# 问题

1. 如何导入不同目录下的模块

```py
import sys
sys.path.append('../1/helloworld.py') # 添加要引入的模块文件的路径

from helloworld import Helloword

```

2. 如何写入中文到文件中

```py
with open(file_name, 'w',encoding='utf8') as file_object:
```

3. 判断文件是否存在

```py
import os
os.path.exists(path)
```