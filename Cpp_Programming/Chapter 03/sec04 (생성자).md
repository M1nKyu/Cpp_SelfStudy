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