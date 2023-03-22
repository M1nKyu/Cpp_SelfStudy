## 예제 3-1
```cpp
#include <iostream>
using namespace std;

/* Circle 선언부 */
class Circle
{
public:
	int radius;
	double getArea();
};

/* Circle 구현부 */
double Circle::getArea()
{
	return 3.14 * radius * radius;
}

/* main 함수 */
int main()
{
	Circle donut;
	donut.radius = 1;
	cout << "donut의 면적은 " << donut.getArea() << endl;

	Circle pizza;
	pizza.radius = 30;
	cout << "pizza의 면적은 " << pizza.getArea() << endl;
}
```
---
# 객체 생성과 객체 이름
- 객체가 생성되면 클래스 크기의 메모리가 할당
```cpp
Circle donut; // Circle 클래스의 객체 donut 생성
Circle pizza; // Circle 클래스의 객체 pizza 생성
```
---
# 객체의 멤버 접근
- 멤버에 접근하기 위해서는 **객체이름 뒤에 (`.`)점을 찍고 그 뒤에 멤버**를 쓴다
	- `객체이름.멤버`
	- C언어의 구조체의 필드를 활용하는 방법과 동일
```cpp
donut.radius = 1;
double area = donut.getArea();
// donut객체는 main()에 의해 생성되었으므로 area변수와 함께 main()의 스택에 존재
```

## 예제 3-2
```cpp
#include <iostream>
using namespace std;

class Rectangle
{
public:
	int width;
	int height;
	int getArea();
};

int Rectangle::getArea()
{
	return width * height;
}

int main()
{
	Rectangle rect;
	rect.width = 3;
	rect.height = 5;
	cout << "사각형의 면적은 " << rect.getArea() << endl;
}
```
---
