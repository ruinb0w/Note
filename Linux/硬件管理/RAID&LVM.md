## RAID

Redundant Array of Inexpensive Disks(廉价磁盘的冗余阵列)

### mdadm

说明: Linux Software RAID

选项:

* `-C` 创建一个新的阵列
* `-v` 显示详细的信息
* `-l` 指定RAID类型
* `-n` 指定磁盘数量
* `-x` 指定备份盘数量

示例:

```sh
# 将4个盘组成RAID10
mdadm -Cv /dev/md0 -n 4 -l 10 /dev/sdb /dev/sdc /dev/sdd /dev/sde
```

## VLM

Logical Volume Manager

常用LVM命令

| 功能 | 物理卷    | 卷组      | 逻辑卷    |
| ---- | --------- | --------- | --------- |
| 扫描 | pvscan    | vgscan    | lvscan    |
| 建立 | pvcreate  | vgcreate  | lvcreate  |
| 显示 | pvdisplay | vgdisplay | lvdisplay |
| 删除 | pvremove  | vgremove  | lvremove  |
| 扩展 |           | vgextend  | lvextend  |
| 缩小 |           | vgreduce  | lvreduce  |

