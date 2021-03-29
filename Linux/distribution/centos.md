# centos

## repository

### 备份原配置文件

```bash
sudo mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```

### 下载新配置文件

>  推荐中科大

#### 阿里云

CentOS7

```javascript
sudo wget -O CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
```

CentOS6

```javascript
sudo wget -O CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-6.repo
```

CentOS5

```javascript
sudo wget -O CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-5.repo
```

#### 网易

CentOS7

```javascript
sudo wget -O CentOS-Base.repo http://mirrors.163.com/.help/CentOS7-Base-163.repo
```

CentOS6

```javascript
sudo wget -O CentOS-Base.repo http://mirrors.163.com/.help/CentOS6-Base-163.repo
```

CentOS5

```javascript
sudo wget -O CentOS-Base.repo http://mirrors.163.com/.help/CentOS5-Base-163.repo
```

#### 中科大

CentOS7

```javascript
sudo wget -O CentOS-Base.repo https://lug.ustc.edu.cn/wiki/_export/code/mirrors/help/centos?codeblock=3
```

CentOS6

```javascript
sudo wget -O CentOS-Base.repo https://lug.ustc.edu.cn/wiki/_export/code/mirrors/help/centos?codeblock=2
```

CentOS5

```javascript
sudo wget -O CentOS-Base.repo https://lug.ustc.edu.cn/wiki/_export/code/mirrors/help/centos?codeblock=1
```

### 更新源数据

先清除原来的元数据缓存

```bash
# 清除原来的缓存
sudo yum clean all
# 生成新的缓存
sudo yum makecache
```

### 

