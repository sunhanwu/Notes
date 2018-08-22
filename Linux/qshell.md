# Linux/Mac OS 下七牛云同步工具qshell的配置与使用

@TOC

## 下载与安装

+ 在官方下载页面下载即可，[qshell](https://developer.qiniu.com/kodo/tools/1302/qshell)
+ 下载后解压，并将系统所对应版本重命名为qshell

![](http://pdt3s257u.bkt.clouddn.com/%E6%B7%B1%E5%BA%A6%E6%88%AA%E5%9B%BE_%E9%80%89%E6%8B%A9%E5%8C%BA%E5%9F%9F_20180821191839.png)

## 配置环境变量

+ 编辑～/.zshrc 或者～/.bashrc文件将qshell路径添加到环境变量中，我的路径为

  ```bash
  export PATH=$PATH:/home/sun/文档/tools/qiniu
  ```

+ 使配置文件生效

  ```bash
  source ~/.zshrc
  ```

## 登录账户

```bash
qshell account ak sk
```

马赛克位置分别填写个人的ak 和sk

![](http://pdt3s257u.bkt.clouddn.com/%E6%B7%B1%E5%BA%A6%E6%88%AA%E5%9B%BE_%E9%80%89%E6%8B%A9%E5%8C%BA%E5%9F%9F_20180821192733.png)

## qupload的使用

1. 配置文件qupload.json,每个参数的具体作用请参考[官方文档](https://github.com/qiniu/qshell/blob/master/docs/qupload.md)

   ```json
   {
      "src_dir"            :   "/home/sun/图片",
      "bucket"             :   "ydm-ng",
      "up_host"            :   "http://upload-z1.qiniu.com",
      "ignore_dir"         :   false,
      "overwrite"          :   false,
      "check_exists"       :   true,
      "check_hash"         :   false,
      "check_size"         :   false,
      "rescan_local"       :   true,
      "log_file"           :   "upload.log",
      "log_level"          :   "info",
      "log_rotate"         :   1,
      "log_stdout"         :   false,
      "file_type"          :   0
   }
   ```

2. 执行命令为

   ```bash
   qshell qupload [<ThreadCount>] <LocalUploadConfig>
   ```

   + 第一个为可选参数，一般选10，第二个为配置文件路径

3. 一般为了节省操作时间，在zshrc配置别名

   ```bash
     alias qupload="qshell qupload 10 /Users/sun/Documents/tools/qshell/qupload.json"
   ```

   在生效source ~/.zsh即可

   ![](http://pdt3s257u.bkt.clouddn.com/%3CKey%20Prefix%3E2018-08-21/%E6%B7%B1%E5%BA%A6%E6%88%AA%E5%9B%BE_%E9%80%89%E6%8B%A9%E5%8C%BA%E5%9F%9F_20180821194833.png)

