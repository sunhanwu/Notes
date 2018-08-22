# ubuntu16.04配置vsftp服务器

## 安装vsftpd

+ 安装

  ```bash
  sudo apt-get install vsftpd
  ```

+ 配置 /etc/vsftp.conf

  ```python
  # 允许匿名用户和本地用户登录，本地用户即/etc/passwd中的用户
  anonymous_enable=YES
  local_enable=YES
  
  # 禁止全局写命令
  write_enable=YES
  
  # 禁止匿名用户上传和创建文件夹
  anon_upload_enable=NO
  anon_mkdir_write_enable=NO
  
  # 只允许userlist的用户登录
  userlist_enable=YES
  userlist_deny=NO
  userlist_file=/etc/vsftpd.user_list
  
  # 注意：使用了vsftpd.user_list后，要在其中加入anonymous才能使用匿名用户登录，如以下内容，表示只有匿名用户和名为ftp的用户，以及本地用户ubuntu可以登录
  anonymous
  ftp
  ubuntu
  ```

+ 创建/etc/vsftpd.user_list文件

  ```
  ubuntu
  root
  ```

## 基本操作

+ 启动、重启、关闭

  ```bash
  sudo /etc/init.d/vsftpd start
  sudo /etc/init.d/vsftpd stop
  sudo /etc/init.d/vsftpd restart
  ```

  
