# Linux/Mac OS下安装oh my zsh并配置主题和插件

## 安装oh my zsh

1. 安装git 、zsh

   + Linux(Ubuntu16.04)

   ```bash
   sudo apt-get install zsh git
   ```

   + Mac OS

   ```bash
   #先自行百度安装homebrew
   brew install git
   ```

   

2. 安装oh my zsh(两种系统命令相同)

   ```bash
   sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
   ```

3. 修改主题：vim ～/.zshrc

   ```bash
   #找到对应行改为
   ZSH_THEME="agnoster"
   ```

   + source ~/.zshrc

## 配置插件

1. wd 

   + 它的作用就是能够快速的切换到常用的目录。 ​			
   + 我们用命令行时经常会遇到这样一种情况， 我们常用的目录就那么几个，而这些目录有时候会再很深的层级中。 使用 cd 命令在这些深层级目录中切换就比较耗费时间了。 ​			
   + 例如 Nginx的wwwroot目录/usr/share/nginx/html  ,我们进入这个目录，输入wd add html   #这个html这个名称是可以随便取的. 下次再进入这个目录就可以直接输入 wd thml
   + wd用法：

   ```
   Usage: wd [command] [point]
   
   Commands:
       add <point>     Adds the current working directory to your warp points
       add             Adds the current working directory to your warp points with current directory's name
       add! <point>    Overwrites existing warp point
       add!            Overwrites existing warp point with current directory's name
       rm <point>      Removes the given warp point
       rm              Removes the given warp point with current directory's name
       show <point>    Print path to given warp point
       show            Print warp points to current directory
       list            Print all stored warp points
       ls  <point>     Show files from given warp point (ls)
       path <point>    Show the path to given warp point (pwd)
       clean!          Remove points warping to nonexistent directories
   
       -v | --version  Print version
       -d | --debug    Exit after execution with exit codes (for testing)
       -c | --config   Specify config file (default ~/.warprc)
       -q | --quiet    Suppress all output
   
       help            Show this extremely helpful text
   ```

2. sudo

   + 连按两次Esc添加或去掉sudo

3. zsh-syntax-highlighting ​	#高亮可用命令

   1. Linux

      ```bash
      git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
      ```

   2. Mac OS

      ```bash
      brew install zsh-syntax-highlighting
      source /usr/local/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
      ```

4. zsh-autosuggestions ​	#记录上一条命令，并自动建议

   ```bash
   git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
   ```

5. 安装

+ 在～/.zshrc下配置

```bash
# Add wisely, as too many plugins slow down shell startup.
plugins=(
  git
  zsh-autosuggestions
  zsh-syntax-highlighting
  wd
  sudo
)
```

+ 最后source ~/.zshrc
