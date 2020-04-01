## Gnome menu 

### category

Need to write an XML `.menu` file to be installed in `/etc/xdg/menus/applications-merged/`

Example `/etc/xdg/menus/applications-merged/wps.menu`

```xml
<!DOCTYPE Menu PUBLIC "-//freedesktop//DTD Menu 1.0//EN"
"http://www.freedesktop.org/standards/menu-spec/menu-1.0.dtd">
<Menu>
        <Name>Applications</Name>
        <Menu>
                <Name>金山办公</Name>
                <Directory>wps-office.directory</Directory>
                        <Include>
                                <Filename>wps-office-wps.desktop</Filename>
                                <Filename>wps-office-et.desktop</Filename>
                                <Filename>wps-office-wpp.desktop</Filename>
                                <Filename>wps-office-pdf.desktop</Filename>
                                <Filename>wps-office-misc.desktop</Filename>
                                <Filename>wps-office-uninstall.desktop</Filename>
                                <Filename>wps-office-prometheus.desktop</Filename>      
                </Include>
        </Menu>
</Menu>
```

## wayland

### configure fcitx in wayland

```sh
sudo vi /etc/environment
# add this content
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
```

## QT5

### 解决缩放

方法1: 修改`.desktop`文件, 或者直接执行

```sh
env QT_AUTO_SCREEN_SCALE_FACTOR=0 QT_SCALE_FACTOR=1 命令
```

> 通过env命令来让某个命令按照环境执行

方法2: 修改`~/.profile`文件

```sh
export QT_AUTO_SCREEN_SCALE_FACTOR=0
export QT_SCALE_FACTOR=1
```

