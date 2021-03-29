### sudo

说明: 可以根据root指定的规则来决定用户执行命令的权限

语法: `sudo command`

* `-l` 查看可以执行的super user操作
* `-u` 指定某个用户身份去执行特定的命令操作

配置文件: `/etc/sudoers`

审计文件: `/var/log/sudo.log`

配置文件语法:

```
root	     ALL        =     (ALL)		       ALL
用户名    允许登录的主机       以谁的身份执行    执行指令的规则

1.用户名可用 %goupName 来表示用户组
2.身份ALL代表root
3.多个命令可以使用逗号分隔
4.不输入密码执行,在命令前加上NOPASSWD, 例如: NOPASSWD:/usr/bin/su
5.阻止执行特定命令 !command, 例如: !/usr/sbin/reboot
6.执行指令的规则是有序的(从前到后)
```

设置别名

1. 主机别名（Host Aliases）

   一般不改，只用ALL。

   `# Host_Alias  FILESERVERS = fs1, fs2`   

   > 注意有空格

   `# Host_Alias  MAILSERVERS = smtp,smtp2`

2. 用户别名包含了**用户**和**用户组**。

   `# User_Alias ADMINS = jsmith, mikem, %groupname` 

   > 用户组前面加百分号

3. 身份别名（Runas_Alias）

   即sudo允许切换到的用户身份，一般不改

   `# Runas_Alias  OP = root`

4. 命令别名（Command Aliases）

   `# Cmnd_Alias SERVICES = /sbin/service, /sbin/chkconfig`

### visudo

说明: 配置`/etc/sudoers`

* `-c` 检查语法

