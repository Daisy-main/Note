# :material-language-cpp:{.lg} 
 
## I/O输入输出
当使用`cin`输入时，例如：
`std::cin >> int hour >> int min;`

输入缓冲区会残留一个回车字符，无法实现`cin.get();`暂停窗口的效果

解决方法：
+ 使用`cin.ignore();`

`cin`会根据变量类型决定如何读取输入值，就像：

`char hours; cin >> hours;`, 输入被`cin`视作字符只读取第一个字符

空格、制表符`Tab`、换行符在会`cin`输入时会被视为字符串的结束标志

### 进制

Cpp支持10进制、8进制和16进制表达整数`86`、`016`、`0x56`

+ Win系统使用系统暂停`system("pause");`

## 类

## 枚举

## 虚函数

虚函数，在基类中声明一个函数为虚函数，使用关键字`virtual`，派生类可以覆写（`override`）这个函数，当基类指针指向派生类对象时，调用派生类方法，如不使用`virtual`调用的会是基类方法

基类虚函数方法: `virtual std::string GetName() { return "Entity"; }`

派生类重写方法: `std::string GetName() override { return "orange"; } `

```C++ title="C++"
#include <iostream>
#include <string>

class Entity
{
public:
	std::string GetName() { return "Entity"; }
    //virtual std::string GetName() { return "Entity"; }
};

class Player : public Entity
{

public:
	std::string GetName() override { return "orange"; } 
    //std::string GetName() override { return "orange"; } 
};

int main()
{
    
	Entity* e = new Entity();
	std::cout << (*e).GetName() << std::endl;

	Player* p = new Player();
	std::cout << p->GetName() << std::endl;

	Entity* entity = p; //子类对象赋值给父类指针
	std::cout << entity->GetName() << std::endl; 

	std::cin.get();

}
```

上述程序中输出结果如下：

=== "不使用虚函数"

    ```bash
    Entity
    orange
    Entity
    ```

=== "使用虚函数"

    ```bash
    Entity
    orange
    orange
    ```

## 纯虚函数/接口

在某些情况下，为基类中定义的虚函数，提供默认实现是没有意义的

纯虚函数允许在基类中定义一个没有函数体的函数（未实现的方法），并强制子类实现该函数，包含纯虚函数的类无法直接实例化

只包含纯虚函数的类，称为接口类，接口类没有成员变量

纯虚函数没有函数体，声明时使用：`virtual std::string GetClassName() = 0;`

```C++ title="C++"
class print
{
public:
	virtual std::string GetClassName() = 0;//纯虚函数
};

class Entity : public print
{
public:
	std::string GetClassName() override { return "Entity"; }
};

class Player : public Entity
{
public:
	std::string GetClassName() override { return "Player"; }
};

int main()
{
	print* a = new Player(); 
	print* b = new Entity();
	std::cout << a->GetClassName() << std::endl; 
	std::cout << b->GetClassName() << std::endl; 

	std::cin.get();
}
```

输出结果为:

```bash
Player
Entity
```

`print* a = new Player();`，如果`Player`中没有实现`virtual std::string GetClassName() = 0;`方法，`Player`是无法被创建的的

## 可见性？

`public`和`private`可见性是为了更好的维护更新代码，明确可见性来保证正确的调用函数，也许在自己忘记代码是怎么写的时候可见性可以派上用场

=== "class"

	```C++

	class Entity // 默认是private
	{
		int x,y;
		void Function();
	};
	// 私有变量和函数仅有Entity内部可见，Entity类的实例也不可见，通过friend友元也可访问
	```
=== "strcut"

	```C++
	struct Entity //默认是public
	{
		int x,y;
		void Function();
	};
	```
## 数组

一些相同类型的数的集合

### 数组遍历

### 1-100 猜数

```C++
int main()
{
    int low = 1;
    int high = 100;
    int guess;
    int count = 0;
    char feedback;

	std::cout << "Think of a number between " << low << " and " << high << ". I will try to guess it!" << std::endl;

	while (true) {
		guess = low + (high - low) / 2;
		count++;
		std::cout << "Is your number " << guess << "? (h/l/c): ";
		std::cin >> feedback;

		if (feedback == 'c') {
			std::cout << "Yay! I guessed your number " << guess << " in " << count << " tries!" << std::endl;
			break;
		} else if (feedback == 'h') {
			high = guess - 1;
		} else if (feedback == 'l') {
			low = guess + 1;
		} else {
			std::cout << "Invalid input. Please enter 'h' for higher, 'l' for lower, or 'c' for correct." << std::endl;
		}
	}
	

	std::cin.get();
}
```

## Static 静态成员

静态成员变量不随对象的销毁而释放内存

## 随机数

随机数的配置，通常需要三个核心组件：种子源、引擎和分布器。现代C++常用`<random>`库生成随机数

随机数标准配置模板

```C++ title="C++"
#include <iostream>
#include <random> // 必须包含此头文件

int main() {
    // 1. 初始化种子源（利用硬件熵池）
    std::random_device rd;

    // 2. 选择随机数引擎（32位梅森旋转算法，性能与质量的平衡点）
    std::mt19937 gen(rd());

    // 3. 定义分布范围，正数分布[min, max]（包含两端）
    std::uniform_int_distribution<> dis(1, 100);

    // 4. 生成并输出
    for (int i = 0; i < 5; ++i) {
        std::cout << dis(gen) << " ";
    }

    return 0;
}
```

## 字符串