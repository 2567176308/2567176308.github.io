---
title: 搭建cs起源服务器
date: 2023-01-15 00:13:59
tags: 服务器
---

欢迎来学习搭建cs起源，搭建cs服务器主要分为三部分：

1、服务器选择

2、steamcmd安装

3、登录并安装CS起源服务器

注意：在这里，我默认了你有Linux基础，能够看懂并处理一些问题

## Quick Start

### 一、选择一款合适的轻量级服务器。

我选择的是国内轻量级云服务器，各大商家其实卖的都不贵，大家可以去多对比，选择折扣力度最大的，也可以先找个免费的试试水。一定要选择国内的服务器，毕竟作为游戏服务器延迟太高懂得都懂，除非你在国外，那选择你自己所在区域就好了。

#### 操作系统选择：Centos或Ubuntu或Debian

这些都可以，区别有一点点但是不大这里我选择的是CentOS7.6然后Ubuntu和Debian因为同根所以方法也是相同的

当然也可以用docker安装，而且更加方便有兴趣的小伙伴，我会将官网地址贴在最后面

#### 登录方式：我选择的xshell这款工具，其他工具一样

#### 开放端口：一定要在服务器厂商那->控制台->防火墙->添加规则，开放端口，默认27015（TCP和UDP都开放）

### 二、steamcmd安装

首先连接到Linux系统后首先创建个steam用户

```bash
useradd -m steam
```

进入用户目录

```bash
cd /home/steam
```

以上步骤各个Linux操作系统相同

接下来我会分操作系统打印命令

#### CentOS安装：

###### 安装环境：

若你的操作系统不是64位，那只需要执行上面这条

```bash
yum install glibc libstdc++
```

```bash
yum install glibc.i686 libstdc++.i686
```

###### CentOS安装screen管理工具

```bash
yum install -y screen
```



#### Ubuntu/Debain安装:

###### 环境安装

注意：root用户不用加sudo

```bash
sudo apt-get install lib32gcc1
```

###### Ubuntu/Debain安装screen管理工具

```bash
sudo apt-get install screen
```



注意：以下操作相同

切换用户：默认以root用户登录切换到steam用户

```bash
su - steam
```

为 SteamCMD 创建目录并切换至该目录。

```bash
mkdir ~/Steam && cd ~/Steam
```

下载并解压缩适用于 Linux 的 SteamCMD。

```bash
curl -sqL "https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz" | tar zxvf -
```

ls查看一下是不是有个steamcmd.sh文件，并运行

```bash
ls
```

```bash
./steamcmd.sh
```

吐槽一句:第一次加载可能有点慢，看运气，如果下载实在很慢的话可以ctrl＋c退出，然后将整个Steam文件夹干掉（删除）然后会到前面创建Steam文件那重来就好

### 三、登录steamcmd并安装CS起源

如果出现Steam>这个就证明你成功安装了，接下来在这个界面我们要登录，并安装cs起源

注意：在Steam>里面不小心输入错了也删不了的话，没关系，回车一下再重新输入就好

#### 选择路径:

```bash
force_install_dir ./cs_source/
```

#### 登录SteamCMD：

注意：要先选择路径后登录

这里采用匿名方式登录,省事

```bash
login anonymous
```

#### 下载cs起源服务器：

```bash
app_update 232330 validate
```

然后你只需要等待，或者泡杯茶，或者先去打开steam准备测试

这个下载速度客观，而且不会像cs1.6那样报错

等他出现```Success! App '232330' fully installed.```就输入```quit```

#### 配置文件：

现在就已经完成cs起源安装了

接下来需要稍稍配置一下就好了,将一下内容复制粘贴到一个文本文件内容，然后重命名为```server.cfg```上传到目录```/home/steam/Steam/cs_source/cstrike/cfg```中，当然这是我的目录，如果你前面有更改的话会不同，但核心就是将文件放入cstrike下面的cfg文件中

```txt
hostname "全CS区最靓的服务器"                   //服务器的名称
Rcon_password ""			// 远程控制密码, 没设即不需要密码
sv_password ""					// 进入服务器所需的密码设定, 没设即不需要密码
sv_region "4"					// 设定服务器的所在区域, 4 为亚洲
sv_allowdownload "1"				// 允许下载档案 (如: 新地图)
sv_allowupload "1"				// 允许上传档案
sv_alltalk "0"					// 公麦 (0/1 - 关/开)
sv_cheats "0"					//作弊功能
tv_enable "1"					// 开启 Source TV (0/1 - 关/开)
sv_downloadurl "http://css.xxx.com/"	//设置地图下载，域名需要绑定在 cstrike 目录上，否则将无法下载地图，可以把地图压缩城.b2z格式提高下载速度
sv_gravity "800"				// 地心引力设定值, 预设 800 重力
sv_voiceenable "1"				// 是否允许玩家使用 mic (0/1 - 关/开)
sv_rcon_maxfailures "2"				//试图取得治理员权限失败凌驾几次，CDKEY即被BAN
sv_maxrate "0"				//限制网络传输的资料最大值
sv_minrate "0"				//限制网络传输的资料最小值
sv_maxupdaterate "66"				//服务器发送至客户端的最大每秒更新次数
sv_minupdaterate "66"				//服务器发送至客户端的最小每秒更新次数
mp_playerid "0"					// 是否显示敌人及队友名字, 1:不显示敌人 2:皆不显示
mp_flashlight "1"				// 是否允许手电筒 (0/1 - 关/开)
mp_timelimit "0"				//多少时间后换地图
mp_maxrounds "0"				//多少回合后换地图4
mp_allowspectators "1"				// 是否允许观察者 (0/1 - 关/开) 
mp_footsteps "1"				// 是否允许脚步声 (0/1 - 关/开)
mp_falldamage "1"				// 高处落下杀伤
mp_autokick "0"					// 是否将闲置及TKer自动踢出服务器 (0/1 - 关/开)
mp_startmoney "16000"				//开局金钱设置
mp_winlimit "0"					//任意一队杀多少回合后换地图
mp_fraglimit "0"　				// 某玩家获得多少 frag 后换地图 (0 无限制) 
mp_freezetime "0"				// 回合开始前的冻结时间 (单位: 秒, 0 为无冻结时间) 
mp_buytime "0.25"				//设置购买武器的时间（单位秒）
mp_forcecamera "0"				// 玩家死后是否只能看到同队画面 (0/1 - 关/开) 
mp_fadetoblack "0"				// 玩家死后画面是否为黑幕 (0/1 - 关/开) 
mp_friendlyfire "0"				//设定会不会杀伤队友。1是会，0是关闭
mp_autoteambalance "1"　　　　　		// 是否启动自动队伍平衡功能 (0/1 - 关/开) 
mp_limitteams "1"　　　　　　 　		// 队伍人数最大可相差几人 
mp_roundtime "3"				// 回合时间 (单位: 分钟) 
log "0"						//设定是否启用日志 0 不启用 1启用
mp_logdetail "0"				// 是否启用详细 log 功能 (0/1 - 关/开
mp_tkpunish "0"					// 是否开启 TK 惩罚 (0/1 - 关/开) 
mp_c4timer "35"					//C4炸弹引爆时间
sv_airaccelerate "5"				//空中停留时间 (默认 10)
sv_enablebunnyhopping "0"			//是否开启连跳相关
```

#### 启动服务器

进入目录

```bash
/home/steam/Steam/cs_source
```

创建一个启动脚本（如果报错显示没有vim可以用vi代替）

```bash
vim strat.sh
```

输入i进入插入模式并粘贴脚本

```bash
#!/bin/sh
echo "Starting CS:Source Server"
sleep 1
screen -A -dm -S css-server ./srcds_run -console -game cstrike -tickrate 66 -pingboost 3  +sv_lan 0 -port 27015 +map de_inferno +maxplayers 10
screen -x css-server

```

可以更改脚本内容，我这里是最大十个玩家，然后地图是小镇，你可以修改成自己想要比如de_dust_2

启动后键盘```Ctrl+a+d```，这样我们就可以安心退出，程序会执行下去

可以通过screen -ls 命令查看会话窗口

也可以用```ps -u```查看进程，关闭的话用```kill PID```

#### 连接服务器：

进入cs起源后```~```键打开控制台

输入

```bash
connect 你的ip
```

改端口了的话要加端口号

```bash
connect 你的ip:端口号
```

### 四、参考文档:

官方文档

```url
https://developer.valvesoftware.com/wiki/SteamCMD:zh-cn
```

