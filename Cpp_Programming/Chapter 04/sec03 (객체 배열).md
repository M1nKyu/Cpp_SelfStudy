# 객체 배열 선언 및 활용
- 객체 배열은 원소가 객체라는 점을 빼면, int char등의 기본 타입의 배열의 선언과 활용의 방법과 동일함
## 예제 4-2
```cpp
#include <iostream>
using namespace std;

class Circle
{
	int radius;
public:
	Circle() { radius = 1; }
	Circle(int r) { radius = r; }
	void setRadius(int r) { radius = r; }
	double getArea();
};
double Circle::getArea()
{
	return 3.14 * radius * radius;
}
int main()
{
	Circle circleArray[3]; // Circle 객체 배열 생성
	// 배열의 각 원소 객체의 멤버 접근
	circleArray[0].setRadius(10);
	circleArray[1].setRadius(20);
	circleArray[2].setRadius(30);
	
	for (int i = 0; i < 3; i++)
	{
		cout << "Circle " << i << "의 면적은 " << circleArray[i].getArea() << endl;
	}

	Circle* p;
	p = circleArray;
	for (int i = 0; i < 3; i++)
	{
		cout << "Circle " << i << "의 면적은 " << p->getArea() << endl;
		p++; // p는 배열의 다음원소를 가리킴
	}
}
[출력]
Circle 0의 면적은 314
Circle 1의 면적은 1256
Circle 2의 면적은 2826
Circle 0의 면적은 314
Circle 1의 면적은 1256
Circle 2의 면적은 2826
```
---
## 객체 배열 선언
- circleArray는 **3개의 Circle객체를 원소로** 가지는 배열이다
```cpp
Circle circleArray[3];
```
---
## 객체 배열 선언문은 기본 생성자를 호출한다
- `Circle circleArray[3];`이 실행되면
	- `Circle::Circle() { radius = 1; }` 기본 생성자가 호출된다

#### 주의점
- 아무 생성자도 선언되지 않은 경우, 컴파일러가 자동으로 생성하지만, 
	- **매개변수를 가진 생성자만 선언돼있는 경우, 기본생성자는 자동으로 생성되지 않아**오류
```cpp
class Circle{
	int radius;
public:
	Circle(int r) {...} // 매개변수 가진 생성자 선언
	double getArea(){...}
};
int main(){
	Circle circleArray[3]; // 기본생성자 호출, 기본생성자 없으므로 컴파일 오류
}
```

- 다음과 같이 초기화 못한다.
	- `Circle circleArray[3](3);`
---
## 객체 배열 사용
- 배열의 각 원소 객체는 [ ] 연산자로 구분
- 호출시, 원소객체와 멤버 사이에 점(`.`)연산자를 사용
```cpp
circleArray[0].setRadius(10);
circleArray[1].setRadius(20);
circleArray[2].setRadius(30);
```
#### 포인터를 이용한 배열다루기
```cpp
Circle *p;
p = circleArray; // p는 circleArray 객체를 가리킨다
for(int i = 0; i < 3; i++){
	cout << "Circle " << i << "의 면적은 " << p->getArea() << endl;
	p++; // 다음 Circle객체 주소로 증가
}
```
- `p[i]`는 배열의 i번째 Circle 객체이다. 그러므로 첫번째 Circle객체의 getArea()함수는 다음과 같이 호출 가능하다
```cpp
p[0].getArea(); // 배열의 첫번째 Circle객체의 getArea()함수 호출
(*p).getArea(); // 위와 동일한 코드이다
```
- **이를 응용하면 위의 for문을 다음과 같이 작성할 수 있다.**
```cpp
Circle *p = circleArray;
for(int i = 0; i < 3; i++){
	cout << "Circle " << i << "의 면적은 " << p[i].getArea() << endl;
}
```
---
## 배열 소멸과 소멸자
- 함수가 종료하면 함수 내 배열도 자동 소멸
	- 배열이 소멸되면 모든 원소 객체가 소멸되며 
		- 원소객체 마다 소멸자가 호출된다
			- 높은 인덱스부터 소멸
				- `array[2] 소멸자 실행 -> array[1] 소멸자 실행 ...`
---
##  Tip. 객체 포인터를 사용한 객체 배열 다루는 다른 방법들
### (1) 포인터 p를 이용하여 객체처럼 접근
```cpp
Circle *p = circleArray;
for(int i = 0; i < 3; i++)
	cout << (*p++).getArea() << endl;
```

### (2) 배열의 이름 circleArray를 포인터로 사용
```cpp
for(int i = 0; i < 3; i++)
	cout << (circleArray + i)->getArea() << endl;
```

### (3) 포인터 p의 정수 연산 이용
```cpp
Circle *p = circleArray;
for(int i = 0; i < 3; i++)
	cout << (p + i)->getArea();
```
---
# 객체 배열 초기화
- 객체 베열을 생성할 때, **생성자를 사용하여 원소 객체를 초기화**할 수 있다
	- `Circle circleArray[3] = { Circle(10), Circle(20), Circle() };`
		- Circle(10)은 Circle(int r)생성자 호출
		- Circle()는 기본 생성자의 호출 

## 예제 4-3
```cpp
#include <iostream>
using namespace std;

class Circle{
public:
	Circle() { radius = 1; }
	Circle(int r) { radius = r; }
	void setRadius(int r) { radius = r; }
	double getArea();
};

double Circle::getArea(){
	return 3.14 * radius * radius;
}

int main(){
	Circle circleArray[3] = { Circle(10), Circle(20), Circle() };
	for(int i = 0; i < 3; i++)
		cout << "Circle " << i << "의 면적은 " << circleArray[i].getArea() << endl;
}

[출력]
Circle 0의 면적은 314
Circle 1의 면적은 1256
Circle 2의 면적은 3.14
```
---
# 다차원 객체 배열
- C++ 은 2, 3차원 등 다차원 객체 배열을 만들 수 있다
	- `Circle circles[2][3];`

- 일차원 배열과 동일하게, 각 원소의 객체가 생성될 때 기본 생성자를 호출
- 다음과 같이 객체의 변수 값을 초기화할 수 있다.
```cpp
circles[0][0] = setRadius(1);
circles[0][1] = setRadius(2);
circles[0][2] = setRadius(3);
circles[0][0] = setRadius(4);
circles[1][1] = setRadius(5);
circles[1][2] = setRadius(6);
```

- { }안에 생성자를 지정하여 배열을 초기화할 수 있다
```cpp
Circle circles[2][3] = {{ Circle(1), Circle(2), Circle(3) }, {Circle(4), Circle(5), Circle() }};
```

## 예제 4-4
```cpp
#include <iostream>
using namespace std;

class Circle
{
	int radius;
public:
	Circle() { radius = 1; }
	Circle(int r) { radius = r; }
	void setRadius(int r) { radius = r; }
	double getArea();
};
double Circle::getArea()
{
	return 3.14 * radius * radius;
}
int main()
{
	Circle circles[2][3];
	circles[0][0].setRadius(1);
	circles[0][1].setRadius(2);
	circles[0][2].setRadius(3);
	circles[1][0].setRadius(4);
	circles[1][1].setRadius(5);
	circles[1][2].setRadius(6);

	for (int i = 0; i < 2; i++)
	{
		for (int j = 0; j < 3; j++)
		{
			cout << "Circle [" << i << "," << j << "]의 면적은 ";
			cout << circles[i][j].getArea() << endl;
		}
	}
}
[출략]
Circle [0,0]의 면적은 3.14
Circle [0,1]의 면적은 12.56
Circle [0,2]의 면적은 28.26
Circle [1,0]의 면적은 50.24
Circle [1,1]의 면적은 78.5
Circle [1,2]의 면적은 113.04
```