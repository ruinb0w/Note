# library

## 文件操作

引入 `#include <fstram>`

### 示例

| 打开方式    | 说明                 |
| ----------- | -------------------- |
| ios::in     | 读文件               |
| ios::out    | 写文件               |
| ios::ate    | 初始位置: 文件尾     |
| ios::app    | 追加写               |
| ios::trunk  | 如果文件存在就先删除 |
| ios::binary | 二进制方式           |

> 通过|来组合使用

#### 写文件

```c++
#include <fstram>
ofstram ofs;
ofs.open("文件路径", 打开方式);
ofs << "写入的数据";
ofs.close();
```

#### 读文件

```c++
#include <fstram>
ifstram ofs;
ifs.open("文件路径", 打开方式);
// 检查文件打开成功
if(!ifs.is_open()){
    cout << "open faild" << endl;
    return;
}
if(!ifs.is_open()){
    cout << "open faild" << endl;
    return;
}
// 方式一
char buf[1024] = {0};
while(ifs >> buf){
    cout << buf << endl;
}
// 方式二
char buf[1024] = {0};
while(ifs.getline(buf, sizeof(buf))){
    cout << buf << endl;
}
// 方式三
string buf;
while(getline(ifs, buf)){
    cout << buf << endl;
}
// 方式四(不推荐)
char c;
while((c=ifs.get()) != EOF){
    cout<< c;
}
ifs.close();
```

#### 写二进制

```c++
#include <fstram>
class Person{
    char name[1024];
    int age;
}

int main(){
    // 可以省略open
	ifstram ofs("路径", ios::out | ios::binary);
    Person p;
    p.name = "小白";
    p.age = 18;
    ofs.write((const char *)&p, sizeof(Person));
    ofs.close();
}
```

#### 读二进制

```c++
#include <fstram>
class Person{
    char name[1024];
    int age;
}

int main(){
    // 可以省略open
	ifstram ofs("路径", ios::in | ios::binary);
    if(!ifs.is_open()){
    	cout << "open faild" << endl;
    	return;
	}
    Person p;
    ifs.read((char *)&p, sizeof(Person));
    cout << p.name << p.age << endl;
    ifs.close();
}
```

#### 读写