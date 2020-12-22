```c++
class Person{
    int age;
    int * height;
    public:
    Person(const Person &p){
		age = p.age;
   	 	height = p.height; //这里不是将引用的值给height?
   	 	height = new int(*p.height); // 既然p是引用为什么要加*
	}
    ~Person(){
        if(height != NULL){
            delete height;
            height = NULL;
        }
    }
}
```

这两个有什么区别

```c++
class Animal{
    virtual void shout(){ // 2
        cout << '动物叫' << endl;
    }
}

class Dog: public Animal{
    virtual void shout(){  // 1
        cout << '狗叫' << endl;
    }
    // 这两个有什么区别
    /*
    void shout(){  // 1
        cout << '狗叫' << endl;
    }
    */
}

void animalShout(Animal &animal){ // 3
    animal.shout();
}

int main(){
    Dog d;
    animalShout(d); // 狗叫
}
```

读写二进制

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
    ofs.write((const char *)&p, sizeof(Person)); // 这里为什么要强转换
    ofs.close();
}
```

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
    ifs.read((char *)&p, sizeof(Person)); // 这里为什么要强转换
    cout << p.name << p.age << endl;
    ifs.close();
}
```

buff自动

```c++
#include <iostream>
#include <fstream>
using namespace std;

int main()
{
  char buf[4];
  ifstream ifs("./1-helloworld.cc", ios::in);
  if (!ifs.is_open()) {
    cout << "open faild" << endl;
    return 1;
  }

  int line = 0;
  while( ifs >> buf){ // 如何自动设置buff大小
    cout << line << ':' << buf << endl;
    line++;
  }

  return 0;
}
```

