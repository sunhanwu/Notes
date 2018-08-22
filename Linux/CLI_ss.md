# ubuntu 16.04配置shadowsocks+proxychains4 实现终端代理

## 安装Python-pip

+ ubuntu16.04默认安装Python2.7，所以不需要安装python，安装python的包管理工具就行了

  ```bash
  sudo apt-get install python-pip
  ```

+ 安装shadowsocks

  ```bash
  sudo pip install shadowsocks
  ```

+ 配置本地vim /home/ubuntu/shadowsocks.json

  ```json
  {
      "server":"11.22.33.44",# 你服务端的IP
      "server_port":50003, # 你服务端的端口
      "local_port":1080, #本地端口，一般默认1080
      "password":"123456", #ss服务端设置的密码
      "timeout":600, #超时设置 和服务端一样
      "method":"aes-256-cfb" #加密方法 和服务端一样
  }
  ```

+ 创建服务启动脚本shadowsocks.sh

  ```bash
  sslocal -c /home/ubuntu/shadowsocks.json
  ```

+ 可能会报错
