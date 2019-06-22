

centos6.9 多版本 python 环境安装 

### 安装 pyenv ###

https://github.com/pyenv/pyenv-installer

```shell
curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer | bash
```

在 ~/.bashrc 中添加如下环境变量

``` 
export PATH="/root/.pyenv/bin:$PATH"    
eval "$(pyenv init -)"    
eval "$(pyenv virtualenv-init -)"    
```

### 安装 Python ### 

**查看可安装的版本**

```shell
pyenv install --list
```

 2.7.15 和 3.6.1 这种只有数字形式的版本号为 Python 官方版本，其他的 anaconda2-4.1.0 这种既有名称-版本的属于 “衍生版” 或发行版。

 
**安装 Python 的依赖**  

```shell
yum install -y readline readline-devel readline-static \ 
               openssl openssl-devel openssl-static  \
               sqlite-devel  \
               bzip2-devel bzip2-libs  \
``` 

 

**安装指定版本**

使用 pyenv install 安装指定版本的 python。

```shell
pyenv install 2.7.15
pyenv install 2.7.15

pyenv: /root/.pyenv/versions/2.7.15 already exists
continue with installation? (y/N) y
Downloading Python-2.7.15.tar.xz...
-> https://www.python.org/ftp/python/2.7.15/Python-2.7.15.tar.xz
Installing Python-2.7.15...
Installed Python-2.7.15 to /root/.pyenv/versions/2.7.15

```
 
**更新数据库**

安装 Python 或者其他带有可执行文件的模块之后，需要对数据库进行更新：

```shell
pyenv rehash
``` 

**查看已安装版本**
```
pyenv versions

* system (set by /root/.pyenv/version)  
  2.7.15  
```
注：星号表示当前正在使用的是系统自带版本的 python。


**全局版本设置**

```shell
pyenv global 3.6.1
pyenv versions
```

**切换回系版本**
```
pyenv global system
```

pyenv local 或 pyenv shell 设置临时 python 版本。

**安装 3.7.0 错误**

```
BUILD FAILED (CentOS 6.9 using python-build 1.2.6)

Inspect or clean up the working tree at /tmp/python-build.20181221103507.10604
Results logged to /tmp/python-build.20181221103507.10604.log

Last 10 log lines:
    import pip._internal
  File "/tmp/tmptyqpus56/pip-10.0.1-py2.py3-none-any.whl/pip/_internal/__init__.py", line 42, in <module>
  File "/tmp/tmptyqpus56/pip-10.0.1-py2.py3-none-any.whl/pip/_internal/cmdoptions.py", line 16, in <module>
  File "/tmp/tmptyqpus56/pip-10.0.1-py2.py3-none-any.whl/pip/_internal/index.py", line 25, in <module>
  File "/tmp/tmptyqpus56/pip-10.0.1-py2.py3-none-any.whl/pip/_internal/download.py", line 39, in <module>
  File "/tmp/tmptyqpus56/pip-10.0.1-py2.py3-none-any.whl/pip/_internal/utils/glibc.py", line 3, in <module>
  File "/tmp/python-build.20181221103507.10604/Python-3.7.0/Lib/ctypes/__init__.py", line 7, in <module>
    from _ctypes import Union, Structure, Array
ModuleNotFoundError: No module named '_ctypes'
make: *** [install] 错误 1
[root@oracle ~]#  pyenv install 3.7.0
Downloading Python-3.7.0.tar.xz...
-> https://www.python.org/ftp/python/3.7.0/Python-3.7.0.tar.xz
Installing Python-3.7.0...
```

yum install libffi-devel -y


```  
Installing Python-3.7.0...
ERROR: The Python ssl extension was not compiled. Missing the OpenSSL lib?

Please consult to the Wiki page to fix the problem.
https://github.com/pyenv/pyenv/wiki/Common-build-problems


BUILD FAILED (CentOS 6.9 using python-build 1.2.6)

Inspect or clean up the working tree at /tmp/python-build.20181221111627.13364
Results logged to /tmp/python-build.20181221111627.13364.log

Last 10 log lines:
			install|*) ensurepip="" ;; \
		esac; \
		 ./python -E -m ensurepip \
			$ensurepip --root=/ ; \
	fi
Looking in links: /tmp/tmpk8n_i0qi
Collecting setuptools
Collecting pip
Installing collected packages: setuptools, pip
Successfully installed pip-10.0.1 setuptools-39.0.1
```

根据官方 wiki<sup>2</sup> 描述：

Python 3.7.0 will not compile on RHEL6 because it requires OpenSSL 1.0.2 or 1.1 and RHEL6 provides 1.0.1e

看来是无法安装 3.7.0 以上的版本了，只能退而求其次，安装 3.6.x 最新版本

附：
1.[https://github.com/pyenv/pyenv](https://github.com/pyenv/pyenv "pyenv")
2.[https://github.com/pyenv/pyenv/wiki/Common-build-problems](https://github.com/pyenv/pyenv/wiki/Common-build-problems "Common-build-problems")
