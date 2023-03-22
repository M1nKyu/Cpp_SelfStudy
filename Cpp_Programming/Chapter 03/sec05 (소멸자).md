# 소멸자란
- 객체가 소멸되는 시점에서 자동으로 호출되는 클래스의 구성요소
```cpp
class Circle
{
	Circle();
	Circle(int r);
	......
	~Circle(); // 소멸자 함수 선언
};

/* 소멸자 함수 구현 */
Circle::~Circle(){
	......
}
```

## 소멸자의 특징
1. 소멸자의 목적은 객체가 사라질 때 필요한 마무리 작업을 위함
	- 객체가 소멸할 때, 동적으로 할당받은 메모리를 운영체제에게 돌려주거나, 열어 놓은 파일을 저장하고 닫거나, 연결된 네트워크를 해제하는 등 객체가 사라지기 전에 필요한 조치를 하도록 하기 위함
2. 소멸자의 이름은 클래스앞에 `~`를 붙인다
	- `Circle::~Circle(){...}`
3. 리턴타입이 없으며, 어떠한 값도 리턴해선 안된다
	- 생성자와 같은 특징
4. 소멸자는 오직 한개만 존재
	- 생성자와 다른 특징
	- 한 클래스에 한개만 존재하며 매개변수를 가지지 않는다
5. 소멸자가 선언돼있지않으면, 기본 소멸자가 자동으로 생성
	- 기본 소멸자는 아무일도 하지 않고 단순 리턴만 하도록 만들어짐
---
# 소멸자 실행
- Circle 클래스에 소멸자를 추가하고, 소멸자가 실행되면 화면에 메시지를 출력하도록 작성
```cpp
int main(){
	Circle donut;
	Circle pizza(30);
	return 0;
}
```
- main()의 **스택**에 donut, pizza 순서로 객체가 생성되며,
	- `return 0;` 문이 실행되면 생성된 반대순으로 pizza, donut 객체가 소멸된다
		-  pizza객체의 ~Circle() 소멸자와 donut 객체의 ~Circle() 소멸자가 각각 순서대로 실행

```cpp
#include <iostream>
using namespace std;

class Circle
{
public :
	int radius;
	Circle();
	Circle(int r);
	~Circle(); //소멸자 선언
	double getArea();
};

Circle::Circle()
{
	radius = 1;
	cout << "반지름 " << radius << " 원 생성" << endl;
}

Circle::Circle(int r)
{
	radius = r;
	cout << "반지름 " << radius << "원 생성" << endl;
}

Circle:: ~Circle()
{
	cout << "반지름 " << radius << " 원 소멸" << endl;
}

double Circle::getArea()
{
	return 3.14 * radius * radius;
}
int main()
{
	Circle donut;
	Circle pizza(30);
	return 0; // main() 함수가 종료하면 main()함수의 스택에 생성된 pizza, donut 객체 소멸
}

[출력]
반지름 1 원 생성
반지름 30원 생성
반지름 30 원 소멸
반지름 1 원 소멸
```
- 객체 생성과 소멸 순서는 스택을 생각
	- 생성과 반대의 순서

## 생성자/소멸자 실행 순서
- ==지역객체==(local object): 함수 내에 선언된 객체
	- 함수가 실행되면 생성, 종료하면 소멸
- ==전역객체==(global object): 함수 바깥에 선언된 객체
	- 프로그램이 로딩될 때 생성되고, main()이 종료한 뒤 프로그램 메모리가 사라질 때 소멸
- 전역객체나 지역객체나 **모두 생성된 순서의 반대로순으로 소멸된다**
```cpp
class Circle{
	...
};
Circle globalCircle; // 전역객체
void f(){
	Circle localCircle; // 지역객체
}
```

### 예제 3-8
```cpp
#include <iostream>
using namespace std;

class Circle
{
public:
	int radius;
	Circle();
	Circle(int r);
	~Circle();
	double getArea();
};

Circle::Circle()
{
	radius = 1;
	cout << "반지름 " << radius << " 원 생성" << endl;
}

Circle::Circle(int r)
{
	radius = r;
	cout << "반지름 " << radius << " 원 생성" << endl;

}

Circle::~Circle()
{
	cout << "반지름 " << radius << " 원 소멸" << endl;
}

double Circle::getArea()
{
	return 3.14 * radius * radius;
}

//전역변수
Circle globalDonut(1000);
Circle globalPizza(2000);

void f()
{
	//지역변수
	Circle fDonut(100);
	Circle fPizza(200);
}

int main()
{
	//main()함수의 지역변수
	Circle mainDonut;
	Circle mainPizza(30);
	f();
}

[출력]
반지름 1000 원 생성 
반지름 2000 원 생성
반지름 1 원 생성 
반지름 30 원 생성
반지름 100 원 생성
반지름 200 원 생성
반지름 200 원 소멸
반지름 100 원 소멸
반지름 30 원 소멸
반지름 1 원 소멸
반지름 2000 원 소멸
반지름 1000 원 소멸
```