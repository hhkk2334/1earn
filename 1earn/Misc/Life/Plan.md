# Plan
[TOC]

---

# 激活
注意：Windows系统和Micrsoft Office软件都必须是VOL版本。
**激活Windows**
用管理员权限运行CMD或PowerShell，输入如下命令：
```powershell
slmgr /skms xxx.xxx.xxx.xxx
slmgr /ato
slmgr /xpr
```
验证一下是否激活：
`slmgr.vbs -dlv`

**激活Office**
用管理员权限运行CMD或PowerShell，输入如下命令：
```powershell
# 进入office安装目录
cd “C:\Program Files(x86)\Microsoft Office\Office16”
# 注册kms服务器地址
cscript ospp.vbs /sethst:xxx.xxx.xxx.xxx
# 执行激活
cscript ospp.vbs /act
# 查看状态
CSCRIPT OSPP.VBS /DSTATUS
```

# DNS
**软件方案**
- DnsJumper（windows下快速配置DNS）
- Pcap_DNSProxy（本地自定义分割DNS解析请求）
    ```ini
    [DNS]
    Outgoing Protocol = IPv4 + TCP

    [Addresses]
    IPv4 Main DNS Address = 208.67.220.222:443
    IPv4 Alternate DNS Address = 208.67.220.220:53|208.67.222.222:5353
    IPv4 Local Main DNS Address = 119.29.29.29:53
    IPv4 Local Alternate DNS Address = 114.114.115.115:53
    ```

**服务器推荐**
- 国内:110.6.6.6、14.114.114.114
- 全球:208.67.222.222、208.67.220.220

---

# 各种代理/源
## git
```git
// 查看当前代理设置
git config --global http.proxy

// 设置当前代理为 http://127.0.0.1:1080 或 socket5://127.0.0.1:1080
git config --global http.proxy 'http://127.0.0.1:1080'
git config --global https.proxy 'http://127.0.0.1:1080'
git config --global http.proxy 'socks5://127.0.0.1:1080'
git config --global https.proxy 'socks5://127.0.0.1:1080' 

// 删除 proxy git config --global --unset http.proxy
git config --global --unset https.proxy
```

## node&js
```bash
npm install -g nrm
nrm ls
nrm use taobao
nrm test
或
npm config set proxy=http://127.0.0.1:8087
```

## pip源
常用的国内镜像包括：
1. 阿里云 http://mirrors.aliyun.com/pypi/simple/
2. 豆瓣http://pypi.douban.com/simple/
3. 清华大学 https://pypi.tuna.tsinghua.edu.cn/simple/
4. 中国科学技术大学 http://pypi.mirrors.ustc.edu.cn/simple/
5. 华中科技大学http://pypi.hustunique.com/

- 临时使用：
可以在使用pip的时候，加上参数-i和镜像地址`https://pypi.tuna.tsinghua.edu.cn/simple`
例如：`pip install -i https://pypi.tuna.tsinghua.edu.cn/simple pandas`，这样就会从清华镜像安装pandas库。

- 永久修改，一劳永逸：
    1. Linux下，修改 ~/.pip/pip.conf (没有就创建一个文件夹及文件。文件夹要加“.”，表示是隐藏文件夹)
    ```vim
    mkdir -p ~/.pip/
    vim ~/.pip/pip.conf
        [global]
        index-url = https://pypi.tuna.tsinghua.edu.cn/simple
        [install]
        trusted-host = https://pypi.tuna.tsinghua.edu.cn
    ```

    2. windows下，直接在user目录中创建一个pip目录，如：C:\Users\xx\pip，然后新建文件pip.ini，即 %HOMEPATH%\pip\pip.ini，在pip.ini文件中输入以下内容（以豆瓣镜像为例）：
    ```vim
    [global]
    index-url = https://pypi.tuna.tsinghua.edu.cn/simple
    [install]
    trusted-host = https://pypi.tuna.tsinghua.edu.cn
    ```

## 终端
先鸽着

---

# 搜索引擎语法
- 包含关键字:`intitle:关键字`
- 包含多个关键字:`allintitle:关键字 关键字2`
- 搜索特定类型的文件:`关键字 filetype:扩展名` 例如`人类简史 filetype:pdf`
- 搜索特定网站的内容:`关键字 site:网址`
- 排除不想要的结果:`关键字 - 排查条件`,例如搜索 “运动相机”，但只想看 GoPro 品牌以外的产品`运动相机 -GoPro`
- 双引号的用处:例如：`"how to write a code"` 如果没有引号，搜索的大部分结果是以 `write code` 为关键字。包含引号后，会确保将完整的字符串做为期望的检索结果提交给搜索引擎。

---

# vscode 配置
```yml
"editor.fontFamily": "Fira Code Retina, 'Microsoft YaHei UI', Arial Black"
"editor.fontLigatures": true
```

---

# 虚拟机建议
linux虚拟机建议
- Centos
- Kali-xfce
- Manjaro-kde

windows虚拟机建议
- [commando-vm](https://github.com/fireeye/commando-vm)
- Win10-日用

## linux虚拟机定制建议
1.统一账号:
账号 root 密码 略
账号 略 密码 略

2.预装软件(持续更新)
```bash
bzip2
vim
python2
python3
make
gcc*gcc-c++
curl
git
SSH
lrzsz

Centos
  "Development Tools"
```

3.桌面需求
```bash
设定屏幕超时时间永不超时
换个不辣眼睛的壁纸(然并卵,反正日常在ssh下使用)
默认终端 fish 或 on my zsh
终端配置 powerline-shell
```

4.网络设置
```bash
dns:208.67.222.222 114.114.114.114
软件包换源:aliyun源或163、tuna源
pip换源
终端看情况走代理
```

5.硬件设施
```bash
CPU:1-2核
mem:1-2-4G
disk:40G
```

## windows定制建议
1.统一账号:
```bash
账号 administrator
密码 略
```

2.预装软件(持续更新)
```bash
Dism+
7zip
notepad++
chrome
Clover
geek
aio-runtimes
java

win10 2019 Ltsc
  TIM
  GlassWire
  360杀毒(虚拟机运行,就当养蛊了)
  360浏览器(为了兼容IE、flash)
```

3.桌面需求
```bash
屏幕超时时间永不超时
换个不辣眼睛的壁纸
```

4.网络设置
```bash
dns:208.67.222.222 114.114.114.114
```

5.硬件设施
```bash
CPU:1-2-4核
mem:2-4-8G
disk:60G
```

6.功能要求
```bash
开启 RDP
开启 ssh，telnet 功能(客户端、服务端)

win10
  更新到最新版本，打好补丁
```

---

# Reference
- [Wind4/vlmcsd: KMS Emulator in C (currently runs on Linux including Android, FreeBSD, Solaris, Minix, Mac OS, iOS, Windows with or without Cygwin)](https://github.com/Wind4/vlmcsd)
- [基于 vlmcsd 搭建 KMS 服务器 - 简书](https://www.jianshu.com/p/11d51983852e)
- [chengr28/Pcap_DNSProxy: Pcap_DNSProxy, a local DNS server based on packet capturing](https://github.com/chengr28/Pcap_DNSProxy)
- [git 配置代理命令 - 阿兴的平凡世界 - 博客园](https://www.cnblogs.com/gx1069/p/6840413.html)
- [npm 配置镜像、设置代理 - MockingBird 博客 - SegmentFault 思否](https://segmentfault.com/a/1190000002589144)
- [将 pip 源更换到国内镜像 - LittleBee的博客 - CSDN博客](https://blog.csdn.net/sinat_21591675/article/details/82770360)
- [你真的会使用搜索引擎吗？](https://mp.weixin.qq.com/s/le_zYcDfhSLvbuu99LprMQ)
- [VSCode 好看字体](https://blog.csdn.net/s1124yy/article/details/82315988)
- [tonsky/FiraCode](https://github.com/tonsky/FiraCode)