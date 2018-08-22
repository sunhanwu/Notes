# Linux服务器配置jupyter-notebook实现远程访问

## 下载anaconda
在[清华镜像](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/)上下载anaconda对应版本
```bash
wget https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/Anaconda3-5.2.0-Linux-x86_64.sh

sudo chmod +x Anaconda*
```
> 注意安装过程中配置环境变量并且是环境变量生效

## 生成配置文件
```bash
jupyter notebook --generate-config
```

## 生成秘钥
> 进入ipython 
```python
1.  In  [1]:  from notebook.auth import passwd
2.  In  [2]: passwd()
3.  Enter password:
4.  Verify password:
5.  Out[2]:  'sha1:ce23d945972f:34769685a7ccd3d08c84a18c63968a41f1140274'
```

复制秘钥，后面要用
![](http://pdt3s257u.bkt.clouddn.com/Snip20180822_4.png)

## 修改配置文件
+ vim ~/.jupyter/jupyter_notebook_config.py
```bash
1.  c.NotebookApp.ip='服务器IP'
2.  c.NotebookApp.password = u'sha:ce...刚才复制的那个秘钥'
3.  c.NotebookApp.open_browser =  False
```

## 后台启动jupyter-notebook
```bash
```bash
nohup jupyter notebook > jupyter.log &
```


## 后台启动jupyter-lab

```bash
nohup jupyter-lab >> ./jupyter-notebook/jupyter-lab.log &
```
> 后台运行并且生成配置文件

![](http://pdt3s257u.bkt.clouddn.com/20180822/Snip20180822_7.png)