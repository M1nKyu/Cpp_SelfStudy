# 헤더파일과 cpp 파일 분리
- 다음과 같은 원칙으로 분리
	- 클래스마다 선언부는 헤더파일에, 구현부는 cpp파일에 분리
	- main() 등 함수나 전역변수는 한개 이상의 cpp 파일에 나누어 작성한다

## 파일 분리 예시
- Circle.h : Circle클래스 선언부
```cpp
class Circle{
private:
	int radius;
public:
	Circle();
	Circle(int r);
	double getArea();
};
```
- Circle.cpp : Circle클래스 구현부
```cpp
#include <iostream>
using namespace std;

#include "Circle.h" // Circle.h include

Circle::Circle(){
	radius = 1;
	cout << "반지름 " << radius;
	cout << " 원 생성" << endl; 
}
Circle::Circlee(int r){
	radius = r;
	cout << "반지름 " << radius;
	cout << " 원 생성" << endl;
}
double Circle::getArea(){
	return 3.14 * radius * radius;
}
```
- main.cpp : main() 함수 등 나머지 코드
```cpp
#include <iostream>
using namespace std;

#include "Circle.h"

int main(){
	Circle donut;
	double area = donut.getArea();
	cout << "donut 면적은 ";
	cout << area << endl;

	Circle pizza(30);
	area = pizza.getArea();
	cout << "pizza 면적은 ";
	cout << area << endl;
}
```
- C++ 컴파일러는 
	- Circle.cpp 와 main.cpp 를 컴파일하여
		- **Circle.obj 와 main.obj를 각각 생성**하고
			- 이들을 **링크하여 main.exe 실행 파일을 만든다**

# 헤더 파일을 중복 include 할때 문제점 해결
- 선언부를 헤더파일로 작성할 때
	- cpp파일에서 클래스가 선언된 헤더파일을 여러번 include하면, 중복선언으로 컴파일 오류가 발생할 수 있음
	- 예를 들어, a.h 헤더파일에서 b.h헤더파일을 내부적으로 include 했는데, 이것을 모른채 cpp파일에서 a.h와 b.h를 둘다 include 하면 결국 cpp 파일에는 b.h가 두번 include
## 조건 컴파일문
### 예시
- Circle.h
```cpp
// 조건 컴파일 문의 상수(CIRCLE_H)는 다른 조건 컴파일 상수와 충돌을 피하기 위해 클래스 이름으로 하는 것이 좋음
#ifndef CIRCLE_H 
#define CIRCLE_H

class Circle{
private:
	int radius;
public:
	Circle();
	Circle(int r);
	double getArea();
};
//조건 컴파일문
#endif
```
- main.cpp
```cpp
#include <iostream>
using namespace std;

// 컴파일 오류 없어짐
#include "Circle.h"
#include "Circle.h"
#include "Circle.h"

int main(){ ... }
```

- 조건 컴파일문이 어떻게 이 문제를 해결하는가
	1. main() 함수의 첫번째 `#include "Circle.h"`이 처리될 때, 다음 문에의 해 CIRCLE_H 상수 정의
		- `#define CIRCLE_H`
			- 그리고 Circle 선언부가 main.cpp에 확장된다
	2. main()함수의 두번째 `#include "Circle.h"`가 처리될 때, CIRCLE_H 상수가 이미 정의돼 있기 때문에, 다음 조건 컴파일 문의 값이 false가 되어 `#endif` 문 밖으로 빠져나오게 된다. 그러므로 Circle 클래스 선언부는 main.cpp에 확장되지 않는다
		- `#ifndef CIRCLE_H`
	3. main() 함수의 세번째 `#include "Circle.h"` 문은 두번째 include 문과 동일한 방식으로 처리
	- 결국 처음 `#include "Circle.h"`문만 처리되어 Circle클래스 선언부가 한번만 main.cpp에 확장