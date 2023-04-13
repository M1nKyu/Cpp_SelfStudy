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

# 객체 배열의 동적 생성 및 반환
- `new`와 `delete`사용
## 객체 배열의 동적 생성과 생성자
```cpp
// new를 이용하여 객체 배열을 동적으로 생성
클래스이름 *포인터변수 = new 클래스이름 [배열크기];

// 3개의 Circle객체로 구성된 배열을 동적 생성
// 기본 생성자 Circle()이 호출된다
Circle *pArray = new Circle[3];
```

- 생성자 호출
```cpp
Circle *pArray = new Circle [3] (30); // 오류

// 배열을 각 원소 객체로 초기화 할 수 있다
Circle *pArray = new Circle [3] {Circle(1), Circle(2), Circle(3)};
```
---
## 객체 배열의 사용
- 동적으로 생성된 객체 배열은 보통 객체 배열처럼 사용한다
```cpp
Circle *pArray = new Circle[3];
pArray[0].setRadius(10);
pArray[1].setRadius(20);
pArray[2].setRadius(30);
for(int i = 0; i < 3; i++)
	cout << pArray[i].getArea();

// pArray는 포인터이므로 다음과 같이도 작성 가능
pArray->setRadius(10);
(pArray + 1)->setRadius(20);
(pArray + 2)->setRadius(30);
for(int i = 0; i < 3; i++)
	cout << (pArray+i)->getArea();
```
---
## 배열의 반환과 소멸자
```cpp
delete [] 포인터변수; // 포인터 변수가 가리키는 배열을 반환

// 예시
delete [] pArray;
```

- delete는 pArray가 가리키는 **배열을 반환하기 직전, 배열의 각 원소 객체의 소멸자를 실행**
	- 실행순서 : **생성의 반대 순**
		`pArray[2] 객체의 소멸자 -> pArray[1] 객체의 소멸자 -> pArray[0] 객체 소멸자`
---
## 예제 4-9
```cpp
// 클래스 생략 
int main()
{
	Circle* pArray = new Circle[3]; // 각 객체의 기본생성자 Circle() 실행
	pArray[0].setRadius(10);
	pArray[1].setRadius(20);
	pArray[2].setRadius(30);

	for (int i = 0; i < 3; i++)
		cout << pArray[i].getArea() << endl;

	Circle* p = pArray; //포인터 p에 배열의 주소값 설정
	for (int i = 0; i < 3; i++)
	{
		cout << p->getArea() << endl;
		p++;
	}
	delete[] pArray; // 객체 배열 반환
}
[출력]
생성자 실행 radius = 1
생성자 실행 radius = 1
생성자 실행 radius = 1
314
1256
2826
314
1256
2826
소멸자 실행 radius = 30
소멸자 실행 radius = 20
소멸자 실행 radius = 10
```

## 예제 4-10
- 원의 개수를 입력받고 Circle배열을 동적 생성
	- 반지름 값을 입력받아 Circle 배열에 저장하고, 면적이 100에서 200사이인 원의 개수를 출력
```cpp
#include <iostream>
using namespace std;

class Circle
{
	int radius;
public:
	Circle();
	~Circle() {};
	void setRadius(int r) { radius = r; }
	double getArea() {return 3.14 * radius * radius;}
};
Circle::Circle()
{
	radius = 1;
}
int main()
{
	cout << "생성하고자 하는 원의 개수?";
	int n, radius;
	cin >> n; // 원의 개수
	if (n <= 0) return 0;
	Circle* pArray = new Circle[n]; // n개의 Circle 배열 생성
	for (int i = 0; i < n; i++)
	{
		cout << "원" << i + 1 << ": ";
		cin >> radius;
		pArray[i].setRadius(radius);
	}

	int count = 0; // 카운트 변수
	Circle* p = pArray;
	for (int i = 0; i < n; i++)
	{
		cout << p->getArea() << ' '; // 원의 면적 출력
		if (p->getArea() > 100 && p->getArea() <= 200)
			count++;
		p++;
	}
	cout << endl << "면적이 100에서 200 사이인 원의 개수는 " << count << endl;
	delete[] pArray;
}
[출력]
생성하고자 하는 원의 개수?4
원1: 5
원2: 6
원3: 7
원4: 8
78.5 113.04 153.86 200.96
면적이 100에서 200 사이인 원의 개수는 2
```
---
## 참고
### 동적으로 할당받은 메모리는 반드시 반환해야 하는가?
- 한 프로그램에서 많은 메모리를 할당 받는 것이, 다른 프로그램의 힙에 영향 X
- 하지만, 필요없게 된 메모리를 힙에 반환하지 않거나, 코딩잘못으로 누수가 생기면 
	- 힙에 메모리가 부족하여 할당 못받게 됨(메모리 누수)
		- 다행히 프로그램 종료 시 힙 전체가 운영체제에 의해 반환됨