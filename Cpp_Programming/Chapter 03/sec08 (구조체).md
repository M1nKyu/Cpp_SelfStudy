# 구조체 선언
- C와의 호환성을 위해 구조체(struct) 지원
- C++ 구조체는 표준 C구조체 기능을 확장하여 **클래스와 동일한 구조와 기능을 가짐**
- `struct` 키워드로 선언, 멤버 변수와 멤버 함수를 가지고, 접근지정도 해야 함
```cpp
struct structName{
private:
	//private 속성의 멤버변수나 멤버함수 선언
public:
	//public 속성의 멤버변수나 멤버함수 선언
protected:
	//protected 속성의 멤버변수나 멤버함수 선언
}; // 세미콜론
```
---
# 구조체 객체 생성
- 클래스 객체 선언 방식과 동일
- struct 키워드는 절대 사용하지 않는다
	- `struct structName stjObj`  => 오류
```cpp
structName stObj; 
```
---
# 구조체와 클래스의 차이점
- 기능적으론 동일
- 오직 다른 한가지는 구조체의 디폴트 접근 지정이 public
- 아래 두 코드는 같은 코드
```cpp
(1) 구조체
struct Circle{
	Circle();
	Circle(int r);
	double getArea();
private:
	int radius;
};

(2) 클래스
class Circle{
	int radius;
public:
	Circle();
	Circle(int r);
	double getArea();
};
```
## 예제 3-10
```cpp
#include <iostream>
using namespace std;

struct StructCircle {
private:
	int radius;
public:
	StructCircle(int r) { radius = r; }
	double getArea();
};

double StructCircle::getArea()
{
	return 3.14 * radius * radius;
}

int main()
{
	StructCircle waffle(3);
	cout << "면적은 " << waffle.getArea();
}

[출력]
면적은 28.26
```