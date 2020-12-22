### 收集网站域名解析记录

利用第三方服务对目标进行被动信息收集

被动信息收集

信息收集-DNS

子域名信息收集

shodan信息收集

google

---

### traceroute

确定网络拓扑, 确认本机与目标是否在统一局域网

### nmap

说明: 扫描局域网内的主机, 确定目标主机是否活跃

语法: `nmap 选项 参数`

* `nmap -sP [IP地址]+` 确认某个/些IP地址是否活跃
* `nmap -sP 网段` 确认某个网段下活跃的IP地址
* `nmap --script broadcast-dhcp-discover` hdcp监听 ???
* `nmap -p [端口范围] IP` 扫描指定IP所开放的接口, 范围用逗号分隔, 不指则随机扫描1000个
* `nmap -O 目标` 目标设备信息, 如操作系统等
* `nmap -sV IP` 目标主机运行的服务

### netdiscover

说明: 支持主动和被动式的ARP侦查工具

语法: `netdiscover 选项 参数`

* `netdiscover -r 范围` 如 `netdiscover -r 192.168.1.0/24`
* `netdiscover` 自动选择范围并进行扫描
* `netdiscover -p` 被动嗅探活动主机

### dmitry

说明: 解析域名,获取与该域名有关的信息, 如注册地址, 电话, 邮箱等

语法: `dmitry 选项 参数`

* `dmitry -w 域名`
* `dmitry -s 域名 -o 输出文件` 查找子域名(主机名)

### ping

说明: 检查网络是否连通, 根据TTL(time to live)获取目标主机的操作系统

| 操作系统              | TTL  |
| --------------------- | ---- |
| Unix及类Unix          | 255  |
| Linux kernel 2.2&2.4  | 64   |
| Window xp/2000/7/8/10 | 128  |
| windows 95/98         | 32   |

### amap/amapcrap

说明: 

* `amapcrap` 可以将随机数据发送到UDP,TCP,SSL端口获取非法响应信息.
* `amap` 可以尝试识别一个运行在非正常端口上的应用

语法: 

* `amapcrap -n 最大连接数 -m 0ab IP port -v`
* `amap -bqv IP port`