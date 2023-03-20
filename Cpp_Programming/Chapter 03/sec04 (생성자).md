# 생성자란
- 객체를 생성할 때 객체를 초기화해주는 멤버 함수
```cpp
class Circle
{
	......
	/* 두개의 생성자 함수 선언 */
	Circle(); // 클래스 이름과 동일
	Circle(int r); // 리턴 타입을 명기하지 않음
};

/* 생성자 함수 구현 */
//매개변수가 없는 생 성자
Circle::Circle() 
{
	......
}
//매개변수 가진 생성자
Circle::Circle(int r)
{
	......
}
```
- 생성자의 목적
	- 객체가 생성될 때 필요한 초기 작업을 위함

- 생성자 함수는 오직 한번만 실행됨
	- 객체가 생성되는 시점에 오직 한번만 자동으로 실행

- 생성자 함수의 이름은 **클래스 이름과 동일**

- 생성자 함수의 원형에 **리턴타입을 선언하지 않는다**
	- 생성자앞에 `void`, `int` 등 리턴타입을 선언하지 않는다
	- 또, `return;`을 통해 함수 실행을 종료할 수는 있지만, 어떤 값도 리턴하면 안된다.

- 생성자는 중복 가능하다
	- 매개 변수 개수나 타입이 서로 다르게 생성
---
# 객체 생성과 생성자 실행
## 예제 3-3
```cpp
#include <iostream>
using namespace std;

class Circle
{
public:
	int radius;
	Circle(); // 기본 생성자
	Circle(int r); // 매개변수 있는 생성자
	double getArea();
};

Circle::Circle()
{
	readius = 1;
	cout << "반지름 " << radius << " 원 생성" << endl;
}

Circle::Circle(int r)
{
	radius = r;
	cout << "반지름 " << radius << " 원 생성" << endl;
}

double Circle::getArea()
{
	return 3.14 * radius * radius;
}

int main()
{
	Circle donut;
	double area = donut.getArea();
	cout << "donut 면적은 " << area << endl;

	Circle pizza(30);
	area = pizza.getArea();
	cout << "pizza 면적은 " << area << endl;
}
/
[출력]
반지름 1 원 생성
donut 면적은 3.14
반지름 30 원 생성
pizza 면적은 2826
```
- 객체의 생성과정
	- 객체 크기의 공간을 할당한 후, 객체 내의 생성자 함수가 실행됨
---
# 위임 생성자(delegating constructor)
- **생성자가 다른 생성자 호출**
```cpp
Circle::Circle(){
	radius = 1;
	cout << "반지름 " << radius << " 원 생성" << endl;
}
Circle::Circle(int r){
	radius = r;
	cout << "반지름 " << radius << " 원 생성" << endl;
}
```
- 위에서 비슷한 2개의 코드가 중복된다. 이를 아래처럼 간소화 한다
```cpp
Circle::Circle() : Circle(1){} // Circle(int r)의 생성자 호출

Circle::Circle(int r){
	radius = r;
	cout << "반지름 " << radius << " 원 생성" << endl;
}
```
- `Circle()`는 객체의 초기화를 다른 생성자에 위임한다고 해서 ==위임 생성재==
- `Circle(int r)` 는 ==타겟 생성자==라고 부름
---
# 생성자와 멤버 변수 초기화
## 생성자 코드에서 멤버 변수 초기화
```cpp
class Point
{
	int x, y;
public:
	Point();
	Point(int a, int b);
};
Point::Point() { x = 0; y = 0;}
Point::Point(int a, int b) { x = a; y = b;}
```
## 생성자 서두에 초깃값으로 초기화
```cpp
Point::Point() : x(0), y(0){ // 멤버 변수 x, y를 0으로 초기화
}
Point::Point(int a, int b) // 멤버 변수 x=a로, y=b로 초기화
	: x(a), y(b){ // 콜론(:) 이하 부분을 다음 줄에 써도 됨
}
```
또는
```cpp
Point::Point(int a)
	: x(a), y(0) { // 멤버 변수 x=a, y=0으로 초기화
}
Point::Point(int a)
	: x(100+a), y(100) { // 멤버 변수 x=100+a, y=100으로 초기화
}
```
## 클래스 선언부에서 직접 초기화
```cpp
class Point{
	int x = 0, y = 0;
	...
};
```
## 예제 3-5
```cpp
#include <iostream>
using namespace std;

class Point
{
	int x, y;
public :
	Point();
	Point(int a, int b);
	void show() {
		cout << "(" << x << ", " << y << ")" << endl; }
};

Point::Point() : Point(0, 0) {} // 위임 생성자
Point::Point(int a, int b) // 타겟 생성자
{
	x = a;
	y = b;
}
int main()
{
	Point origin;
	Point target(10, 20);
	origin.show();
	target.show();
}
```
---
# 생성자는 꼭 있어야 하는가
- 예 
- 클래스에 여러개의 새성자가 있다 해도, C++ 컴파일러는 생성자 중 반드시 하나를 호출
- 생성자가 없는 클래스는 ==기본 생성자==를 만들어 삽입

# 기본 생성자 (디폴트 생성자)
- 클래스에 선언된 생성자가 없을때 컴파일러가 자동으로 생성하는 생성자
- 매개변수가 없는 생성자이다
```cpp
class Circle{
	Circle(); // 기본생성자
};
```

## 기본 생성자가 자동으로 생성되는 경우
- 클래스에 생성자가 없을때 `Circle donut` 코드를 실행한다면 기본생성자가 자동으로 삽입되어 문제없이 컴파일 된다.
## 기본 생성자가 자동으로 생성되지 않는 경우
- 생성자가 하나라도 선언돼있으면 기본생성자를 삽입하지 않는다
- 만약 `Circle pizza(30);`코드는 `Circle (int r)` 생성자를 호출하는데
	- `Circle donut;` 을 통해 객체를 생성하려는데 더이상 기본생성자가 생성되지 않아 컴파일 오류를 발생시킨다
```cpp
class Circle
{
public:
	int radius;
	double getArea();
	Circle(int r); // 생성자가 선언돼있기 때문에 컴파일러는 기본 생성자를 생성하지 않음
};
Circle::Circle(int r)
{
	radius = r;
}
int main()
{
	Circle pizza(30);
	Circle donut; // 컴파일 오류, 기본 생성자가 없기 때문
}
```
## 예제 3-6
```cpp
#include <iostream>
using namespace std;

class Rectangle
{
public:
	int width;
	int height;
	Rectangle();
	Rectangle(int a);
	Rectangle(int a, int b);
	bool isSquare();
};

Rectangle::Rectangle() : Rectangle(1, 1) {}
Rectangle::Rectangle(int a) : Rectangle(a, a) {}
Rectangle::Rectangle(int a, int b)
{
	width = a;
	height = b;
}

bool Rectangle::isSquare()
{
	return width == height;
}

int main()
{
	Rectangle rect1;
	Rectangle rect2(3, 5);
	Rectangle rect3(3);

	if (rect1.isSquare()) cout << "rect1은 정사각형이다." << endl;
	if (rect2.isSquare()) cout << "rect2은 정사각형이다." << endl;
	if (rect3.isSquare()) cout << "rect3은 정사각형이다." << endl;
}
```