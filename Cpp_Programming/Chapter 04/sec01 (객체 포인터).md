```cpp
Circle donut;
double d = donut.getArea();

Circle = *p; // 객체에 대한 포인터 선언
p = &donut; // 포인터에 객체 주소 저장
d = p->getArea(); // 멤버 함수 호출
```
## 객체에 대한 포인터 변수 선언
```cpp
Circle *p; // 현재 아무 객체도 가리키지 않음 
```

## 포인터 변수에 객체 주소 지정
- 객체의 주소는 객체 이름 앞에 `&`연산자를 사용하여 표현
```cpp
p = &donut; // p에 donut 객체의 주소 저장
```

- 다음과 같이 선언할때, 같이 초기화 하면 된다
```cpp
Circle *p = &donut;
```

## 포인터를 이용한 객체 멤버 접근
- 객체 포인터로 멤버를 접근할 때 `->` 연산자를 사용한다
```cpp
d = p->getArea();
d - (*p).getArea(); // 이와 같이 코딩할 수도 있음
```

- 초기화되지 않은 객체 포인터를 사용하면 오류 발생
```cpp
Circle *p;
p->getArea(); // 'null pointer assignment' 오류 발생
```

## 예제 4-1
```cpp
#include <iostream>
using namespace std;

class Circle
{
	int radius;
public:
	Circle() { radius = 1; }
	Circle(int r) { radius = r; }
	double getArea();
};
double Circle::getArea()
{
	return 3.14 * radius * radius;
}

int main()
{
	Circle donut;
	Circle pizza(30);
	cout << donut.getArea() << endl; // 3.14

	Circle* p;
	p = &donut;
	cout << p->getArea() << endl; // 3.14
 	cout << (*p).getArea() << endl; // 3.14

	p = &pizza;
	cout << p->getArea() << endl; // 2826
	cout << (*p).getArea() << endl; // 2826
}
[출력]
3.14
3.14
3.14
2826
2826
``` 