## string

c++ 的string 本质是一个类, 内部封装了char *

### 重构运算符

#### +=

```c++
//string 实现了
string str1 = "我";
str1 += "爱玩游戏";
cout << str1 << endl; // 我爱玩游戏
string str2 = ", wow";
str1 += str2; // 2.通过一个string类型的实例进行添加
cout << str1 << endl; //我爱玩游戏, wow

```

#### [ ]

```c++
string str ="hello";
for(int i = 0; i < str.size(); i++){
    cout << str[i] << " ";
    str[i]='o';
}
cout << endl; // h e l l o
cout << str << endl; // ooooo
```

### 方法

#### append

```c++
string str1 = "我";
str1.append("爱玩游戏");
cout << str1 << endl; //我爱玩游戏
```

#### find/rfind

```c++
string str = "hello hello";
str.find("lo"); //3 匹配的字符串的第一个字符的位置
str.rfind("lo"); // 9 从右往左招
str.find("test"); //-1 找不到
```

#### replace

```c++
string str = "hello world";
str.replace(6,5, "c++"); // hello c++
```

#### compare

```c++
string str ="hello";
str.compare("hello"); // 0
```

#### insert

```c++
string str ="hello";
str.insert(1,"111"); // h111ello
str.erase(1,3); //hello
```

#### substr

```c++
string str = "hello";
string sub = str.substr(1,3);
cout << sub << endl; //ell
```



