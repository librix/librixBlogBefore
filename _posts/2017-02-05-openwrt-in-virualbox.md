
# 2017-02-05-virualbox 里的 openwrt

用 virualbox 里的 openwrt 这个**虚拟路由器**接管宿主的所有流量, 在虚拟路由里做透明代理。就相当绑了一个 openwrt 路由在电脑上。

## 思路

让virtualbox 里的 openwrt 接管宿主的流量, 需要给虚拟机配两张网卡：

1. 一张网卡设置为桥接。虚拟机通过这张网卡从上级路由获取 IP，摇身变为和宿主同等的网络设备。
2. 另一张设为 Host-only,     宿主的网络数据从这张网卡流向虚拟路由.

设好网络后，用 **route 命令**把宿主的**默认网关**改为**虚拟路由器**, 在把 **DNS** 也设置为**虚拟路由器的地址**。That’s all.

然后通过配置路由器 openwrf 管理自己的网络。

## 安装

根据 [wiki](https://wiki.openwrt.org/doc/howto/virtualbox) 的说明 , 先把 openwrt 安装到虚拟机里 :

- 下载 [openwrt-15.05.1-x86](https://downloads.openwrt.org/chaos_calmer/15.05.1/x86/generic/openwrt-15.05.1-x86-generic-combined-ext4.img.gz)

- 解压: `gunzip openwrt-15.05.1-x86-generic-combined-ext4.img.gz`

- 将解压出来的镜像转化为 virtualbox 的原始格式: `VBoxManage convertfromraw --format VDI openwrt-15.05.1-x86-generic-combined-ext4.img openwrt.vdi`

  > 注：windows 下，VBOXManage默认没有加入环境变量，需要使用绝对路径和文件名。

- 用 virtualbox 建一个虚拟机 openwrt :

  Name: openwrt
  Type: Linux
  Memory size: 512 MB
  Use an existing virtual hard disk file: openwrt.vdi

- 打开 virtualbox 的全局设置,在网络选项卡里新建一个 Host-Only Networks :

  IPv4 Address: 192.168.100.2
  IPv4 Network Mask: 255.255.255.0
  DHCP Server: Disable

- 打开虚拟机 openwrt 的设置,在网络选项卡里对 「适配器1」进行设置 :

  Enable Network Adapter
  Attached to: Host-only Adapter
  Name: vboxnet0「这里选择在之前步骤新建的 Host- Only Networks 」

  另外再添加一张「适配器2」:

  Enable Network Adapter
  Attached to: Bridged Adapter
  Name: en0: Wi-Fi(AirPort)「这里选择宿主上网的网卡」

## 配置虚拟机网络

- 启动并进入 openwrt , 对网络进行设置 `vim /etc/config/network` :

  ```
  config interface 'loopback'
      option ifname 'lo'
      option proto 'static'
      option ipaddr '127.0.0.1'
      option netmask '255.0.0.0'
  config interface 'lan'
      option ifname 'eth0'
      option type 'bridge'
      option proto 'static'
      option ipaddr '192.168.100.1' 「将 lan 地址改为 192.168.100.1 」
      option netmask '255.255.255.0'
      option ip6assign '60'
  config interface 'wan'
      option ifname 'eth1'
      option proto 'dhcp'
  config interface 'wan6'
      option ifname 'eth1'
      option proto 'dhcpv6'
  config globals 'globals'
      option ula_prefix 'fde9:2442:ec95::/48'
  ```

- 在 openwrt 上执行: `/etc/init.d/network restart` 重启 openwrt 的网络, 在 openwrt 上执行 `ifconfig` 查看网络,应该可以看到 eth0 的 IP 是我们设定的 192.168.100.1 ,宿主这时可以通过 ssh 登录到 虚拟 openwrt . 而 eth1 网卡已经从上级路由器获取到了对应的 IP 地址, 在 openwrt 上执行 `ping baidu.com` , 不通的话再检查下哪里没做对.

  将默认网关设置为 openwrt :

  ```
  # windows 和 Linux 操作不同，不可以直接更改
  > route change 0.0.0.0 mask 0.0.0.0  192.168.100.1 
  #更改失败，先添加，再删除
  > route delete 0.0.0.0
  > route -p add 0.0.0.0 mask 0.0.0.0 192.168.100.1
  ```

  将 DNS 设置为 openwrt 

  ```
  > netsh interface ipv4 set dnsservers name="WLAN" source=static 192.168.100.1
  ```

  > 将宿主上执行 :`sudo route change default 192.168.100.1` 将默认网关设置为 openwrt , 

  > 在宿主上执行 : `sudo networksetup -setdnsservers Wi-Fi 192.168.100.1` 将 DNS 设置为 openwrt . 

  此时所有宿主的流量都被 openwrt 接管, DNS 也在 openwrt 上进行查询. 试着用宿主浏览网页, 网络不通的话再检查下:

  - openwrt 是否已经启动, 并且在 openwrt 里已经可以上网
  - 在宿主上执行 `ifconfig vboxnet0` 检查 vboxnet0 网卡是否已经准备好, 宿主的数据都是经过这个网卡流向虚拟路由器.
  - 在宿主上执行 `netstat -nr | grep default` 查看默认路由是否指向了虚拟 openwrt

- 为了方便之后的操作, 在虚拟路由上执行 `passwd` 更改密码, 然后将宿主的公钥加入 openwrt 的 /etc/dropbear/authorized_keys 中以便免密码登录. 一些常用命令:

  - 用 `VBoxManage startvm --type headless openwrt` , 可以在后台运行 openwrt

  - 需要关闭 openwrt 时, 运行命令: `VBoxManage controlvm openwrt poweroff`

  - 在宿主上的 $HOME/.ssh/config 文件内配置 openwrt , 通过 `ssh openwrt` 登录比起 `ssh root@id-address` 更方便 :

    ```
    	Host    openwrt
    HostName    192.168.100.1
    	User    root
    ```

## 透明代理

在 openwrt 上设置透明代理的方法有很多 , 个人认为最优雅的组合是 :

- 在 gfvvlist 的基础上 , 自己维护一个需要走代理的域名列表
- 用 dnsmasq 架设 DNS 服务 , 列表内的域名转发到 shadowsocks 的 ss-tunnel , 让 vps 进行 DNS 查询 , 避免污染 . 域名外的域名直接交给上级路由查询 , 可以获得 cdn 加速 .
- dnsmasq 得到列表中域名的 IP 地址后 , 加入一个 ipset 集合中 . 于是我们就得到了一个需要走代理的 IP 地址集合 .
- 用 iptables 的 ipset 功能 , 目标地址在指定集合内的数据包 , 转发到 shadowsocks 的 ss-redir , 科学上网.
- 当然 , shadowsocks 的数据全部交给 kcptun 进行加速 .

利用以上这个组合 , 就可以根据域名区分数据走向 . 以下仅仅是记录过程 , 了解更多原理请点 : [那些从墙上学会的知识](https://icymind.com/learn-from-gfw/)

### 准备相关软件

- 下载 [shadowsocks-libev for openwrt](https://github.com/shadowsocks/openwrt-shadowsocks/releases) 并在宿主上执行 `scp shadowsocks-libev*.ipk openrt:~` 传送到 openwrt 上 . 在 openwrt 上执行 `opkg update && opkg install shadowsocks-libev_2.5.6-1_x86.ipk` 进行安装 .
- 下载 [kcptun for linux](https://github.com/bettermanbao/openwrt-kcptun/releases) 并把客户端可执行文件移动到 openwrt 上的系统路径 , 在 openwrt 上执行 : `mv client_linux_x386 /usr/bin/kcptun`
- 因为只有 dnsmasq-full 才支持 ipset,卸载 dnsmasq 并安装 dnsmasq-full : `opkg remove dnsmasq && opkg install dnsmasq-full`
- 安装 ipset : `opkg install ipset`

### 配置 shadowsocks

- /etc/ss-local.json

  ```
  {
      "server":       "127.0.0.1",
      "server_port":  1070,
      "local_address": "0.0.0.0",
      "local_port":   1080,
      "password":     "paaasssword",
      "timeout":      300,
      "method":       "chacha20",
      "fast_open":    true
  }
  ```

- /etc/ss-tunnel.json

  ```
  {
      "server": "server-ip",
      "server_port": 8989,
      "local_address": "0.0.0.0",
      "local_port": 5353,
      "password": "paaasssword",
      "timeout": 300,
      "method": "chacha20",
      "fast_open": true
  }
  ```

- /etc/init.d/ss

  ```
  #!/bin/sh /etc/rc.common
  START=105
  SERVICE_USE_PID=1
  SERVICE_WRITE_PID=1
  SERVICE_DAEMONIZE=1
  start() {
      service_start /usr/bin/ss-tunnel -L 8.8.8.8:53 -c /etc/ss-tunnel.json -u
      service_start /usr/bin/ss-redir  -c /etc/ss-local.json -u
  }
  stop() {
      service_stop /usr/bin/ss-tunnel
      service_stop /usr/bin/ss-redir
  }
  ```

- 开机启动 : `/etc/init.d/ss enable` , 手动开启/关闭 : `/etc/init.d/ss start|stop`

### 配置kcptun

- /etc/kcptun-client.json

  ```
  {
      "remoteaddr": "server-ip:server-port",
      "localaddr": ":1070",
      "mode":     "fast3",
      "crypt":    "server-crypt",
      "nocomp":    true | false (must be same as server side)
  }
  ```

- /etc/init.d/kcptun

  ```
  #!/bin/sh /etc/rc.common
  # Copyright (C) 2006-2011 OpenWrt.org
  START=70
  SERVICE_USE_PID=1
  SERVICE_WRITE_PID=1
  SERVICE_DAEMONIZE=1
  start() {
      service_start /usr/bin/kcptun -c /etc/kcptun-client.json --log /var/log/kcptun.log
  }
  stop() {
      service_stop /usr/bin/kcptun
  }
  ```

- 随开机启动 : `/etc/init.d/kcptun enable` , 手动启动/停止 : `/etc/init.d/kcptun start|stop`

### 配置 iptables

- /etc/firewall.user

  ```
  #redir packages from openwrt itself
  iptables -t nat -A OUTPUT -p tcp -m set --match-set SS dst -j REDIRECT --to-port 1080
  iptables -t nat -A OUTPUT -p udp -m set --match-set SS dst -j REDIRECT --to-port 1080
  # redir packages from client
  iptables -t nat -A PREROUTING -p tcp -m set --match-set SS dst -j REDIRECT --to-port 1080
  iptables -t nat -A PREROUTING -p udp -m set --match-set SS dst -j REDIRECT --to-port 1080
  # new ipset: SS
  ipset -N SS hash:ip
  ```

- 使 iptables 规则生效 : `/etc/init.d/firewall restart`

### 配置 dnsmasq

- /etc/dnsmasq.conf

  ```
  conf-dir=/etc/dnsmasq.d/
  min-cache-ttl=3600
  cache-size=9999
  ```

- /etc/dnsmasq.d/over-gfw.conf , 可以用这个 [domains-to-dnsmasq 脚本](https://github.com/icymind/domains-to-dnsmasq) 自动生成 :

  ```
  server=/google.com/127.0.0.1#5353
  ipset=/google.com/SS
  server=/twitter/127.0.0.1#5353
  ipset=/twitter/SS
  ...
  ...
  ```

- 重启 dnsmasq , 使配置文件生效 : `/etc/init.d/dnsmasq restart`

全部配置后之后就可以上资本主义网站了 . 但是当宿主的外部网络发生变化 , 比如连接另一个 Wi-Fi 时 , 我们自定义的 iptables 规则会被系统重写而丢失 , kcptun 在没有网络的情况下也会崩溃退出 , 因此可以加一个脚本监控这些状态 , 随时恢复到可以正常使用的状态:

- /root/keep-kt-ss-alive

  ```
  #!/bin/sh
  kcptun_pid=$(pgrep kcptun)
  ss_redir_pid=$(pgrep ss-redir)
  ss_tunnel_pid=$(pgrep ss-tunnel)
  iptable_rules=$(iptables -S -t nat | grep 1080)
  # KCPTUN
  if [ -z "$kcptun_pid" ];then
      /etc/init.d/kcptun restart
  fi
  # SHADOWSOCKS
  if [ -z "$ss_redir_pid" ] || [ -z "$ss_tunnel_pid" ];then
      /etc/init.d/ss restart
  fi
  # IPTABLES
  if [ -z "$iptable_rules" ];then
      /etc/init.d/firewall restart
  fi
  ```

  别忘了给脚本添加可执行权限 : `chmod +x /root/keep-kt-ss-alive`

- 新建计划任务 , 每分钟执行 keep-kt-ss-alive 脚本 : `crontab -e`

  ```
  * * * * * /root/keep-kt-ss-alive
  ```

- 还需要让系统的 cron 服务随开机启动 , 我们的计划任务才能执行: `/etc/init.d/cron enable && /etc/init.d/cron start`

## 自动化

### 随宿主开机启动 openwrt

- `cat ~/Library/LaunchAgents/com.icymind.openwrt.sh`

  ```
  #!/bin/bash
  # iCyMind <icyminnd@gmail.com>
  function stopvm()
  {
      if [ -n "$(/usr/local/bin/VBoxManage list runningvms | grep openwrt)" ];then
          echo "$(/bin/date): shutdown openwrt"
          /usr/local/bin/VBoxManage controlvm openwrt poweroff
      fi
      exit 0
  }
  function startvm()
  {
      if [ -z "$(/usr/local/bin/VBoxManage list runningvms | grep openwrt)" ];then
          echo "$(/bin/date): startup openwrt"
          /usr/local/bin/VBoxHeadless -s openwrt &
          wait $!
      fi
  }
  trap stopvm HUP KILL TERM
  startvm;
  ```

- `cat ~/Library/LaunchAgents/com.icymind.openwrt.plist`

  ```
  <?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE plist PUBLIC "-//Apple Computer//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
  <plist version="1.0">
    <dict>
      <key>Label</key>
      <string>com.icymind.openwrt</string>
      <key>ProgramArguments</key>
      <array>
          <string>/Users/simon/Dropbox/Script/com.icymind.vboxopenwrt.sh</string>
      </array>
      <key>KeepAlive</key>
      <true/>
      <key>RunAtLoad</key>
      <true/>
      <key>UserName</key>
      <string>simon</string>
      <key>WorkingDirectory</key>
      <string>/Users/simon/</string>
    </dict>
  </plist>
  ```

- 加载 launchd 任务 : `launchctl bootstrap gui/501 ~/Library/LaunchAgents/com.icymind.openwrt.plist` . 其中 501 是用户的 uid , 可以通过执行 `id -u` 获知 .

### 宿主开机时/网络变化时 , 自动更改网关和 DNS

- `cat ~/Dropbox/Script/com.icymind.network.sh`

  这个脚本会在 vboxnet0 网卡激活后 , 将宿主的默认网关/ DNS 指向虚拟机 . 同时重启 openwrt 的网络 , 让它重新从上游路由器获取 IP 地址.

  ```
  #!/bin/bash
  # make sure your had set nopasswd for route/networksetup command.
  INTERFACE="Wi-Fi"
  GATEWAY="192.168.100.1"
  USER="root"
  # wait for vboxnet0 available
  # vboxnet0 active after virtual machine startup. If change route table before vboxnet0 active, your network will be unreachable
  while true; do
      ifconfig vboxnet0
      if [ $? -eq 0 ]; then
          break
      fi
      sleep 5
  done
  # restart openwrt network to renew ip from upper dhcp
  ssh $USER@$GATEWAY "/etc/init.d/network restart && sleep 4 && /etc/init.d/kcptun restart && /etc/init.d/firewall restart > /dev/null 2>&1"
  # change default route.
  sudo route change default $GATEWAY
  sudo networksetup -setdnsservers $INTERFACE $GATEWAY
  ```

- `cat ~/Library/LaunchAgents/com.icymind.network.plist`

  在 OSX 上 , 每次开机或者网络环境发生变化时:

  - `/etc/resolv.conf`

  - `/Library/Preferences/SystemConfiguration/NetworkInterfaces.plist`

  - `/Library/Preferences/SystemConfiguration/com.apple.airport.preferences.plist`

    这三个文件都会发生变化 , 写个 Agent 监控这几个文件 , 当发生改变时自动执行更改网关的脚本.

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE plist PUBLIC "-//Apple Computer//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
    <plist version="1.0">
      <dict>
        <key>Label</key>
        <string>com.icymind.network</string>

        <key>ProgramArguments</key>
        <array>
            <string>/Users/simon/Dropbox/Script/com.icymind.network.sh</string>
        </array>

        <key>WatchPaths</key>
        <array>
            <string>/etc/resolv.conf</string>
            <string>/Library/Preferences/SystemConfiguration/NetworkInterfaces.plist</string>
            <string>/Library/Preferences/SystemConfiguration/com.apple.airport.preferences.plist</string>
        </array>

        <key>RunAtLoad</key>
        <true/>
      </dict>
    </plist>
    ```

- 同理用 `launchctl bootstrap gui/501 ~/Library/LaunchAgents/com.icymind.network.plist` 加载并执行 .

## log –verbose

- 开始用的是 64 位的 openwrt 镜像 , 装了两遍虚拟路由都不能从上级路由器获取到 IP , 于是改用 32 位的镜像.

- 更改网关和 DNS 需要 `sudo route` 和 `sudo networksetup` , 为了能让脚本顺利执行 , 需要在 /etc/sudoers 中添加:

  ```
  simon   ALL=(ALL) NOPASSWD: /usr/sbin/networksetup, /sbin/route
  ```

  其中 simon 是我的用户名

- 重启 openwrt 的网络需要登录到路由器执行 , 为了让脚本能顺利执行 , 需要开启密钥登录:

  - 如果宿主没有密钥对的话 , 用 `ssh-keygen` 生成 , 公钥在宿主的 ~/.ssh/id_rsa.pub
  - 将宿主公钥的内容复制到 openwrt 的 /etc/dropbear/autorized_keys 文件内即可



# 附录

## 问题1.默认路由是什么？怎么设置？

默认路由与默认网关

由于在路由表中存储针对每个主机或子网的路由项不可行，因此提出了默认路由的概念，默认路由中的网关称为默认网关。默认路由的网络地址为0.0.0.0，网络掩码为0.0.0.0，它匹配任何网络通信，因此当到达特定主机或特定子网的路由并未在路由表中指定时，均可以通过默认路由来进行转发。如果没有设置默认路由，那么无法到达未在路由表中指定路由项的网络目的地址。

设置默认路由后，把数据包的路由责任移交到了路由器，优点是简化了本地计算机上的路由表和配置，缺点则是计算机无法明确目的地址是否可达，从而可能发送针对不可到达地址的流量。虽然位于路由路径上的路由器知道目的地址不可达时会使用ICMP目的地址不可达信息来通知原始发送主机，但是这个过程中，已经占用了额外的网络流量。

在Windows系统中，创建默认路由可以通过以下两种方式实现：

在网络接口的TCP/IP选项中设置默认网关，从而创建默认路由；

使用 route add 命令添加网络地址为0.0.0.0、网络掩码为0.0.0.0的默认路由；

推荐大家总是使用前一种方式。

参考：

1. https://www.ezloo.com/2011/11/windows_route.html
2. http://blog.163.com/ares_cxy/blog/static/84926570201122472237922/
3. http://book.51cto.com/art/201112/310167.htm

## 问题2. Windows 通过SSH 登录 openwrt

putty下载：http://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html

```
Authenticating with public key "imported-openssh-key"
BusyBox v1.23.2 (2016-01-02 14:04:44 CET) built-in shell (ash)

  _______                     ________        __
 |       |.-----.-----.-----.|  |  |  |.----.|  |_
 |   -   ||  _  |  -__|     ||  |  |  ||   _||   _|
 |_______||   __|_____|__|__||________||__|  |____|
          |__| W I R E L E S S   F R E E D O M
 -----------------------------------------------------
 CHAOS CALMER (15.05.1, r48532)
 -----------------------------------------------------
  * 1 1/2 oz Gin            Shake with a glassful
  * 1/4 oz Triple Sec       of broken ice and pour
  * 3/4 oz Lime Juice       unstrained into a goblet.
  * 1 1/2 oz Orange Juice
  * 1 tsp. Grenadine Syrup
 -----------------------------------------------------
root@OpenWrt:~# 
```

