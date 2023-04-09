# 객체의 동적 생성 및 반환
## new를 이용한 객체의 동적 생성과 생성자
```cpp
클래스이름 *포인터변수 = new 클래스이름; //기본생성자 호출
클래스이름 *포인터변수 = new 클래스이름(생성자매개변수리스트); // 매개변수있는 생성자 호출
```

- 클래스 크기의 메모리를 할당받아 객체 생성
	- 이때 생성자 호출
---
## delete를 이용한 객체 반환과 소멸자
```cpp
delete 포인터변수; // 객체 반환
```

- 예시
```cpp
Circle *p = new Circle; //생성자 Circle()과 동일, p = new Circle();와 동일
Circle *q = new Circle(30); // 생성자 Circle(30) 호출

delete p; // Circle 객체 반환
delete q; // Circle 객체 반환
```

- 반드시 new를 이용하여 동적할당받은 메모리의 주소이어야 delete 사용 가능
```cpp
Circle donut;
Circle *p = &donut;
delete p; // 실행오류, p가 가리키는 객체는 동적할당 받은 것 아님.
```

### (참고)Circle waffle 과 Circle waffle()의 차이
- 어느것이 매개변수 없는 생성자를 호출하는 것?
```cpp
Circle waffle; // (o)
Circle waffle(); // (x), 오류를 발생시키진 않음
```

- `Circle waffle()`을 Circle 객체를 리턴하는 함수 waffle()의 선언으로 인지
	- 그러므로 `waffle.getArea();` 이 코드는 오류가 발생

- **그러나 다음 두 코드는 문제 없음**
```cpp
Circle *p = new Circle; // (o)
Circle *p = new Circle(); // (o)
```

## 예제 4-7
```cpp
#include <iostream>
using namespace std;

class Circle
{
	int radius;
public:
	Circle();
	Circle(int r);
	~Circle();
	void setRadius(int r) { radius = r; }
	double getArea() { return 3.14 * radius * radius; }
};
Circle::Circle()
{
	radius = 1;
	cout << "생성자 실행 radius = " << radius << endl;
}
Circle::Circle(int r)
{
	radius = r;
	cout << "생성자 실행 radius = " << radius << endl;
}
Circle::~Circle()
{
	cout << "소멸자 실행 radius = " << radius << endl;
}
int main()
{
	Circle* p, * q;
	p = new Circle;
	q = new Circle(30);
	cout << p->getArea() << endl << q->getArea() << endl;
	delete p;
	delete q; // delete 순서는 생성순서와 상관X
}
[출력]
생성자 실행 radius = 1
생성자 실행 radius = 30
3.14
2826
소멸자 실행 radius = 1
소멸자 실행 radius = 30
```
## 예제 4-8
- 위 예제에서 정수값으로 반지름을 입력받고, Circle 객체를 동적으로 생성하여 면적출력
- 음수 입력시 종료
```cpp
...
int main()
{
	int radius;
	while (true)
	{
		cout << "정수 반지름 입력(음수이면 종료) >> ";
		cin >> radius;
		if (radius < 0) break;
		Circle* p = new Circle(radius);
		cout << "원의 면적은 " << p->getArea() << endl;
		delete p;
	}
}
[출력]
정수 반지름 입력(음수이면 종료) >> 5
생성자 실행 radius = 5
원의 면적은 78.5
소멸자 실행 radius = 5
정수 반지름 입력(음수이면 종료) >> 9
생성자 실행 radius = 9
원의 면적은 254.34
소멸자 실행 radius = 9
정수 반지름 입력(음수이면 종료) >> -1 // 음수입력시 종료
```

