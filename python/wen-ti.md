# 问题

## `scrapy crawl quotes`报错

```
ModuleNotFoundError: No module named 'win32api'
```

解决方法
```
pip install pypiwin32
```

## pip安装pygame遇到`ValueError: path is on mount 'F:', start on mount 'C:'
`

```py
Exception:
Traceback (most recent call last):
  File "f:\python-project\python-start-programming\venv\lib\site-packages\pip-10.0.1-py3.7.egg\pip\_internal\basecommand.py", line 228, in main
    status = self.run(options, args)
  File "f:\python-project\python-start-programming\venv\lib\site-packages\pip-10.0.1-py3.7.egg\pip\_internal\commands\install.py", line 335, in run
    use_user_site=options.use_user_site,
  File "f:\python-project\python-start-programming\venv\lib\site-packages\pip-10.0.1-py3.7.egg\pip\_internal\req\__init__.py", line 49, in install_given_reqs
    **kwargs
  File "f:\python-project\python-start-programming\venv\lib\site-packages\pip-10.0.1-py3.7.egg\pip\_internal\req\req_install.py", line 748, in install
    use_user_site=use_user_site, pycompile=pycompile,
  File "f:\python-project\python-start-programming\venv\lib\site-packages\pip-10.0.1-py3.7.egg\pip\_internal\req\req_install.py", line 961, in move_wheel_files
    warn_script_location=warn_script_location,
  File "f:\python-project\python-start-programming\venv\lib\site-packages\pip-10.0.1-py3.7.egg\pip\_internal\wheel.py", line 346, in move_wheel_files
    clobber(source, dest, False, fixer=fixer, filter=filter)
  File "f:\python-project\python-start-programming\venv\lib\site-packages\pip-10.0.1-py3.7.egg\pip\_internal\wheel.py", line 312, in clobber
    record_installed(srcfile, destfile, changed)
  File "f:\python-project\python-start-programming\venv\lib\site-packages\pip-10.0.1-py3.7.egg\pip\_internal\wheel.py", line 250, in record_installed
    newpath = normpath(destfile, lib_dir)
  File "f:\python-project\python-start-programming\venv\lib\site-packages\pip-10.0.1-py3.7.egg\pip\_internal\wheel.py", line 245, in normpath
    return os.path.relpath(src, p).replace(os.path.sep, '/')
  File "F:\soft\python\Lib\ntpath.py", line 562, in relpath
    path_drive, start_drive))
```

将python安装在C盘，并且项目也建在C盘安装成功了

## 升级pip

```py
python -m pip install --upgrade pip
```

```py
Exception:
Traceback (most recent call last):
  File "C:\Users\Administrator\Documents\pyproject\venv\lib\site-packages\pip-10.0.1-py3.7.egg\pip\_internal\basecommand.py", line 228, in main
    status = self.run(options, args)
  File "C:\Users\Administrator\Documents\pyproject\venv\lib\site-packages\pip-10.0.1-py3.7.egg\pip\_internal\commands\install.py", line 335, in run
    use_user_site=options.use_user_site,
  File "C:\Users\Administrator\Documents\pyproject\venv\lib\site-packages\pip-10.0.1-py3.7.egg\pip\_internal\req\__init__.py", line 49, in install_given_reqs
    **kwargs
  File "C:\Users\Administrator\Documents\pyproject\venv\lib\site-packages\pip-10.0.1-py3.7.egg\pip\_internal\req\req_install.py", line 748, in install
    use_user_site=use_user_site, pycompile=pycompile,
  File "C:\Users\Administrator\Documents\pyproject\venv\lib\site-packages\pip-10.0.1-py3.7.egg\pip\_internal\req\req_install.py", line 961, in move_wheel_files
    warn_script_location=warn_script_location,
  File "C:\Users\Administrator\Documents\pyproject\venv\lib\site-packages\pip-10.0.1-py3.7.egg\pip\_internal\wheel.py", line 431, in move_wheel_files
    generated.extend(maker.make(spec))
  File "C:\Users\Administrator\Documents\pyproject\venv\lib\site-packages\pip-10.0.1-py3.7.egg\pip\_vendor\distlib\scripts.py", line 403, in make
    self._make_script(entry, filenames, options=options)
  File "C:\Users\Administrator\Documents\pyproject\venv\lib\site-packages\pip-10.0.1-py3.7.egg\pip\_vendor\distlib\scripts.py", line 307, in _make_script
    self._write_script(scriptnames, shebang, script, filenames, ext)
  File "C:\Users\Administrator\Documents\pyproject\venv\lib\site-packages\pip-10.0.1-py3.7.egg\pip\_vendor\distlib\scripts.py", line 243, in _write_script
    launcher = self._get_launcher('t')
  File "C:\Users\Administrator\Documents\pyproject\venv\lib\site-packages\pip-10.0.1-py3.7.egg\pip\_vendor\distlib\scripts.py", line 382, in _get_launcher
    result = finder(distlib_package).find(name).bytes
AttributeError: 'NoneType' object has no attribute 'bytes'
```

```py
pip install -U --force-reinstall pip  # 运行这个命令解决了
```

## 如何导入不同目录下的模块

```py
import sys
sys.path.append('../1/helloworld.py') # 添加要引入的模块文件的路径

from helloworld import Helloword

```

## 如何写入中文到文件中

```py
with open(file_name, 'w',encoding='utf8') as file_object:
```

## 判断文件是否存在

```py
import os
os.path.exists(path)
```
