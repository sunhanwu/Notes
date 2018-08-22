
# gitbook使用

## 本地修改
> 在本地利用 yu writer进行编辑之后使用git上传到github
```bash
git add <修改的文件名>
git commit -m "修改的简述"
git push -u github master
```

![](http://pdt3s257u.bkt.clouddn.com/Snip20180822_8.png)

## 服务器从github同步数据
```bash
git pull github master
```

![](http://pdt3s257u.bkt.clouddn.com/Snip20180822_9.png)

## 重启gitbook服务
```bash
lsof -i:4000
# 找到pid之后杀死进程
kill -9 pid
setsid gitbook serve .
```

![](http://pdt3s257u.bkt.clouddn.com/20180822/Snip20180822_10.png)

