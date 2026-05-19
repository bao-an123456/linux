# Linux 常用命令速查表

---

## 目录

- [1. 文件与目录操作](#1-文件与目录操作)
- [2. 文件查看与编辑](#2-文件查看与编辑)
- [3. 权限管理](#3-权限管理)
- [4. 文本处理三剑客](#4-文本处理三剑客)
- [5. 查找与搜索](#5-查找与搜索)
- [6. 进程管理](#6-进程管理)
- [7. 系统信息与监控](#7-系统信息与监控)
- [8. 磁盘与存储](#8-磁盘与存储)
- [9. 网络管理](#9-网络管理)
- [10. 压缩与解压](#10-压缩与解压)
- [11. 用户与权限](#11-用户与权限)
- [12. 软件包管理](#12-软件包管理)
- [13. 其他实用命令](#13-其他实用命令)
- [14. 快捷键速查](#14-快捷键速查)
- [15. 管道与重定向](#15-管道与重定向)

---

## 1. 文件与目录操作

| 命令 | 说明 | 常用示例 |
|------|------|----------|
| `ls` | 列出目录内容 | `ls -la` (详细列表，含隐藏文件) |
| `cd` | 切换目录 | `cd /var/log` / `cd ~` / `cd -` |
| `pwd` | 显示当前路径 | `pwd` |
| `mkdir` | 创建目录 | `mkdir dir` / `mkdir -p a/b/c` |
| `rm` | 删除文件/目录 | `rm file` / `rm -rf dir` (强制递归删除) |
| `cp` | 复制 | `cp file1 file2` / `cp -r dir1 dir2` |
| `mv` | 移动/重命名 | `mv old new` / `mv file /tmp/` |
| `touch` | 创建空文件或更新时间戳 | `touch file.txt` |
| `ln` | 创建链接 | `ln -s target link` (软链接) |
| `tree` | 树状显示目录结构 | `tree -L 2` (显示2层) |
| `rmdir` | 删除空目录 | `rmdir empty_dir` |

---

## 2. 文件查看与编辑

| 命令 | 说明 | 常用示例 |
|------|------|----------|
| `cat` | 查看文件内容 | `cat file` / `cat -n file` (显示行号) |
| `less` | 分页查看（可向前翻页） | `less file` |
| `more` | 分页查看（仅向后翻页） | `more file` |
| `head` | 查看文件头部 | `head -n 20 file` |
| `tail` | 查看文件尾部 | `tail -f log.txt` (实时追踪) |
| `nl` | 带行号显示 | `nl file` |
| `wc` | 统计行数/词数/字节 | `wc -l file` (行数) |
| `vim` / `vi` | 文本编辑器 | `vim file.txt` |
| `nano` | 简易文本编辑器 | `nano file.txt` |

---

## 3. 权限管理

| 命令 | 说明 | 常用示例 |
|------|------|----------|
| `chmod` | 修改文件权限 | `chmod 755 file` / `chmod u+x script.sh` |
| `chown` | 修改所有者 | `chown user:group file` |
| `chgrp` | 修改所属组 | `chgrp developers file` |
| `umask` | 设置默认权限掩码 | `umask 022` |

### 权限数字对照

| 数字 | 权限 | 说明 |
|------|------|------|
| 7 | `rwx` | 读+写+执行 |
| 6 | `rw-` | 读+写 |
| 5 | `r-x` | 读+执行 |
| 4 | `r--` | 只读 |
| 0 | `---` | 无权限 |

---

## 4. 文本处理三剑客

### grep — 文本过滤

    grep "pattern" file.txt          # 基础搜索
    grep -i "pattern" file.txt       # 忽略大小写
    grep -r "pattern" /var/log       # 递归搜索目录
    grep -v "pattern" file.txt       # 反向匹配（排除）
    grep -n "pattern" file.txt       # 显示行号
    grep -E "a|b" file.txt           # 扩展正则（等同于 egrep）

### sed — 流编辑器

    sed 's/old/new/g' file.txt       # 全局替换
    sed -i 's/old/new/g' file.txt    # 直接修改文件
    sed '2d' file.txt                # 删除第2行
    sed -n '5,10p' file.txt          # 只打印5-10行

### awk — 文本分析

    awk '{print $1}' file.txt        # 打印第一列
    awk -F: '{print $1}' /etc/passwd # 指定分隔符
    awk 'NR==5' file.txt             # 打印第5行
    awk '{sum+=$1} END {print sum}' file.txt  # 求和第一列

---

## 5. 查找与搜索

| 命令 | 说明 | 常用示例 |
|------|------|----------|
| `find` | 文件查找 | `find / -name "*.log"` |
| `find` | 按类型查找 | `find . -type f -size +100M` |
| `find` | 执行命令 | `find . -name "*.tmp" -delete` |
| `locate` | 快速定位（基于数据库） | `locate nginx.conf` |
| `which` | 查找命令路径 | `which python3` |
| `whereis` | 查找二进制/源码/手册 | `whereis gcc` |
| `type` | 判断命令类型 | `type ls` |

### find 常用组合

    find . -name "*.py" -mtime -7       # 7天内修改过的py文件
    find /var/log -name "*.log" -size +1G -exec rm {} \;  # 删除大于1G的日志

---

## 6. 进程管理

| 命令 | 说明 | 常用示例 |
|------|------|----------|
| `ps` | 查看进程快照 | `ps aux` / `ps -ef` |
| `top` | 动态进程监控 | `top` |
| `htop` | 增强版 top（需安装） | `htop` |
| `kill` | 终止进程 | `kill -9 PID` (强制终止) |
| `killall` | 按名称终止 | `killall nginx` |
| `pkill` | 按模式终止 | `pkill -f python` |
| `pgrep` | 按名称查 PID | `pgrep sshd` |
| `nohup` | 后台运行，忽略挂起 | `nohup ./app &` |
| `&` | 后台运行 | `./script.sh &` |
| `jobs` | 查看后台任务 | `jobs -l` |
| `fg` | 前台恢复 | `fg %1` |
| `bg` | 后台恢复 | `bg %1` |

---

## 7. 系统信息与监控

| 命令 | 说明 | 常用示例 |
|------|------|----------|
| `uname` | 系统内核信息 | `uname -a` |
| `uptime` | 系统运行时长与负载 | `uptime` |
| `free` | 内存使用情况 | `free -h` (人类可读) |
| `df` | 磁盘空间 | `df -h` |
| `du` | 目录/文件大小 | `du -sh /var/log` |
| `vmstat` | 系统整体性能 | `vmstat 1 5` |
| `iostat` | IO 统计 | `iostat -x 1` |
| `netstat` | 网络连接（传统） | `netstat -tlnp` |
| `ss` | 网络连接（现代替代） | `ss -tlnp` |
| `lsof` | 查看打开的文件 | `lsof -i :8080` |
| `dmesg` | 内核日志 | `dmesg | tail` |
| `journalctl` | systemd 日志 | `journalctl -u nginx` |

---

## 8. 磁盘与存储

| 命令 | 说明 | 常用示例 |
|------|------|----------|
| `fdisk` | 分区表操作 | `fdisk -l` |
| `parted` | 分区管理 | `parted /dev/sda` |
| `mkfs` | 格式化文件系统 | `mkfs.ext4 /dev/sdb1` |
| `mount` | 挂载 | `mount /dev/sdb1 /mnt` |
| `umount` | 卸载 | `umount /mnt` |
| `df` | 查看挂载点空间 | `df -Th` |
| `lsblk` | 块设备信息 | `lsblk` |
| `blkid` | 查看 UUID | `blkid /dev/sda1` |
| `dd` | 磁盘复制/备份 | `dd if=/dev/sda of=backup.img` |

---

## 9. 网络管理

| 命令 | 说明 | 常用示例 |
|------|------|----------|
| `ip` | 现代网络配置（替代 ifconfig） | `ip addr` / `ip link` / `ip route` |
| `ifconfig` | 网络接口配置（传统） | `ifconfig eth0` |
| `ping` | 测试连通性 | `ping -c 4 baidu.com` |
| `curl` | 数据传输/请求 | `curl -I https://api.github.com` |
| `wget` | 下载文件 | `wget -O file.zip URL` |
| `ssh` | 远程登录 | `ssh user@host` |
| `scp` | 安全复制文件 | `scp file user@host:/path` |
| `rsync` | 增量同步 | `rsync -avz src/ dest/` |
| `netstat` / `ss` | 查看端口 | `ss -tlnp` |
| `traceroute` | 路由追踪 | `traceroute baidu.com` |
| `mtr` | 网络诊断（ping+traceroute） | `mtr baidu.com` |
| `nslookup` / `dig` | DNS 查询 | `dig @8.8.8.8 baidu.com` |
| `tcpdump` | 抓包分析 | `tcpdump -i eth0 port 80` |
| `nc` / `netcat` | 网络瑞士军刀 | `nc -zv host 22` |

---

## 10. 压缩与解压

| 命令 | 说明 | 常用示例 |
|------|------|----------|
| `tar` | 归档工具 | `tar -czvf archive.tar.gz dir/` |
| `tar` | 解压 | `tar -xzvf archive.tar.gz` |
| `gzip` | gzip 压缩 | `gzip file` / `gunzip file.gz` |
| `zip` | zip 压缩 | `zip -r archive.zip dir/` |
| `unzip` | zip 解压 | `unzip archive.zip` |
| `bzip2` | bzip2 压缩 | `bzip2 file` |
| `xz` | xz 压缩 | `xz file` |

### tar 常用选项记忆

    -c  创建归档
    -x  解压归档
    -z  通过 gzip 压缩/解压
    -j  通过 bzip2 压缩/解压
    -v  显示过程
    -f  指定文件名
    -C  指定解压目录

---

## 11. 用户与权限

| 命令 | 说明 | 常用示例 |
|------|------|----------|
| `whoami` | 当前用户 | `whoami` |
| `who` | 登录用户 | `who` |
| `w` | 登录用户及负载 | `w` |
| `id` | 用户/组 ID | `id username` |
| `useradd` | 添加用户 | `useradd -m -s /bin/bash newuser` |
| `userdel` | 删除用户 | `userdel -r olduser` |
| `passwd` | 修改密码 | `passwd` / `passwd username` |
| `usermod` | 修改用户 | `usermod -aG sudo username` |
| `groupadd` | 添加用户组 | `groupadd developers` |
| `su` | 切换用户 | `su - root` |
| `sudo` | 以 root 执行 | `sudo apt update` |
| `last` | 登录历史 | `last` |

---

## 12. 软件包管理

### Debian/Ubuntu (apt)

    apt update                  # 更新软件源
    apt upgrade                 # 升级已安装包
    apt install nginx           # 安装软件
    apt remove nginx            # 卸载软件
    apt purge nginx             # 彻底卸载（含配置）
    apt search nginx            # 搜索软件包
    apt show nginx              # 查看包详情
    apt autoremove              # 清理无用依赖
    dpkg -i package.deb         # 安装本地 deb 包

### RHEL/CentOS/Fedora (yum/dnf)

    yum update                  # 更新
    yum install nginx           # 安装
    yum remove nginx            # 卸载
    yum search nginx            # 搜索
    yum info nginx              # 详情
    rpm -ivh package.rpm        # 安装本地 rpm 包
    # Fedora 推荐用 dnf 替代 yum
    dnf install nginx

### Arch Linux (pacman)

    pacman -Sy                  # 同步软件库
    pacman -S nginx             # 安装
    pacman -R nginx             # 卸载
    pacman -Ss nginx            # 搜索
    pacman -Syu                 # 全面升级

---

## 13. 其他实用命令

| 命令 | 说明 | 常用示例 |
|------|------|----------|
| `echo` | 输出文本 | `echo $PATH` / `echo "hello" > file` |
| `date` | 日期时间 | `date "+%Y-%m-%d %H:%M:%S"` |
| `cal` | 日历 | `cal 2026` |
| `history` | 命令历史 | `history` / `!42` (执行第42条) |
| `clear` | 清屏 | `clear` |
| `alias` | 命令别名 | `alias ll='ls -alF'` |
| `export` | 设置环境变量 | `export PATH=$PATH:/usr/local/bin` |
| `env` | 查看环境变量 | `env` / `env | grep PATH` |
| `crontab` | 定时任务 | `crontab -e` |
| `at` | 一次性定时任务 | `at now + 1 hour` |
| `watch` | 定时执行并刷新显示 | `watch -n 1 'ps aux'` |
| `xargs` | 参数传递 | `cat list.txt | xargs rm` |
| `tee` | 输出到屏幕并保存 | `echo "test" | tee file.txt` |
| `cut` | 按列切割 | `cut -d: -f1 /etc/passwd` |
| `sort` | 排序 | `sort -n file.txt` |
| `uniq` | 去重 | `sort file | uniq -c` |
| `diff` | 文件对比 | `diff file1 file2` |
| `screen` / `tmux` | 终端复用 | `tmux new -s session` |
| `base64` | 编解码 | `echo "text" | base64` |
| `md5sum` / `sha256sum` | 校验文件 | `sha256sum file.iso` |
| `chroot` | 切换根目录 | `chroot /mnt/sysimage` |
| `systemctl` | systemd 服务管理 | `systemctl status nginx` |
| `service` | 传统服务管理 | `service nginx restart` |

---

## 14. 快捷键速查

| 快捷键 | 作用 |
|--------|------|
| `Ctrl + C` | 终止当前进程 |
| `Ctrl + Z` | 挂起当前进程（放入后台） |
| `Ctrl + D` | 退出终端 / EOF |
| `Ctrl + L` | 清屏（等同于 `clear`） |
| `Ctrl + A` | 光标移到行首 |
| `Ctrl + E` | 光标移到行尾 |
| `Ctrl + U` | 删除光标前所有内容 |
| `Ctrl + K` | 删除光标后所有内容 |
| `Ctrl + R` | 历史命令反向搜索 |
| `Tab` | 自动补全 |
| `!!` | 执行上一条命令 |
| `!$` | 上一条命令的最后一个参数 |

---

## 15. 管道与重定向

    command > file          # 标准输出覆盖写入文件
    command >> file         # 标准输出追加写入文件
    command 2> file         # 标准错误写入文件
    command &> file         # 标准输出+错误写入文件
    command1 | command2     # 管道：将 command1 的输出作为 command2 的输入
    command < file          # 从文件读取输入

---

