# Linux下用dd命令制作U盘启动盘

> 在manjaro系统下测试

1. 查询U盘对应文件sudo fdisk -l

   ```bash
   Disk /dev/nvme0n1：238.5 GiB，256060514304 字节，500118192 个扇区
   单元：扇区 / 1 * 512 = 512 字节
   扇区大小(逻辑/物理)：512 字节 / 512 字节
   I/O 大小(最小/最佳)：512 字节 / 512 字节
   磁盘标签类型：gpt
   磁盘标识符：09CDCE5C-F487-42C9-83BF-B41ACD262434
   
   设备                起点      末尾      扇区   大小 类型
   /dev/nvme0n1p1      4097    618497    614401   300M EFI 系统
   /dev/nvme0n1p2    618498 481648510 481030013 229.4G Linux 文件系统
   /dev/nvme0n1p3 481648511 500103449  18454939   8.8G Linux swap
   
   
   Disk /dev/sda：28.7 GiB，30752000000 字节，60062500 个扇区
   单元：扇区 / 1 * 512 = 512 字节
   扇区大小(逻辑/物理)：512 字节 / 512 字节
   I/O 大小(最小/最佳)：512 字节 / 512 字节
   磁盘标签类型：dos
   磁盘标识符：0xcad4ebea
   
   设备       启动 起点     末尾     扇区  大小 Id 类型
   /dev/sda4  *     256 60062499 60062244 28.7G  c W95 FAT32 (LBA)
   ```

   发现U盘对应的是/dev/sda4

2. 使用dd命令写入iso文件

   ```bash
   sudo dd if=/home/sun/manjaro.iso of=/dev/sda4 bs=4M 
   ```
