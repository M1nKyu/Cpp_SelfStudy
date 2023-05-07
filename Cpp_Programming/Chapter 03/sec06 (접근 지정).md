# 접근지정자
- 3가지의 멤버 접근 지정자(acess specifer)가 있다
	1. private(비공개)
	2. public(공개)
	3. protected(보호)

- 멤버에 대한 접근지정은 클래스 선언부에서 접근지정자 다음에 콜론(`:`)을 찍고 멤버들을 선언
```cpp
class Sample{
private :
	//private 멤버 선언
public :
	//public 멤버 선언
protected :
	//protected 멤버 선언
};
```

## private 멤버
- 클래스내의 멤버 함수들에게만 접근 허용

## public 멤버
- 클래스 내외를 막론하고 프로그램의 모든 함수들에게 접근 허용

## protected 멤버
- 클래스내의 멤버함수와 이 클래스를 **상속**받은 파생 클래스의 멤버 함수에게만 접근이 허용
---
# 디폴트 접근 지정은 private
- 접근 지정을 하지 않은 경우 디폴트 접근 지정은 private로 처리된다
	- ❗**캡슐화의 목적**❗이다.
		- **캡슐화의 기본 원칙**이 비공개이기 때문
```cpp
class Circle{
	int radius; //디폴트 접근지정은 private
public:
	Circle()
	Circle(int r)
	double getArea();
};
```
---
# 멤버 보호와 생성자
## 멤버 변수는 private로 지정하는 것이 바람직함
- 클래스 멤버들은 클래스 외부에서 마음대로 접근할 수 없도록 하는것이 기본이다
### (a) 멤버 변수를 public으로 선언한 나쁜 사례
```cpp
class Circle{
public:
	int radius; //멤버 변수 보호받지 못함
	Circle();
	Circle(int r);
	double getArea();
};
Circle::Circle(){
	radius = 1;
}
Circle::Circle(int r){
	radius = r;
}
```

```cpp
int main(){
	Circle waffle;
	waffle.radius = 5; //노출된 멤버는 마음대로 접근, 나쁜사례
}
```
### (b)멤버 변수를 private로 선언한 바람직한 사례
```cpp
class Circle{
private:
	int radius;
public:
	Circle();
	Circle(int r);
	double getArea();
}
Circle::Circle(){
	radius = 1;
}
Circle::Circle(int r){
	radius = r;
}
```

```cpp
int main()
{
	Circle waffle(5);
	waffle.radius = 5; // private 멤버라서 접근 불가능하다
}
```
- `Circle waffle(5);`처럼 생성자를 통해 radius 값을 전달하도록 해야한다

## ❗생성자는 public 으로
- 클래스 **외부에서 객체를 생성**하기 위해서는 생성자를 public으로 선언해야 한다

- 의도적으로 외부에서 객체를 생성할 수 없도록 private로 선언하기도 하고, 
	- 자식클래스에서만 생성자를 호출할 수 있도록 protected로 선언하기도 한다

## ❗예제 3-9❗
- 컴파일 오류가 발생하는 곳은?
```cpp
#include <iostream>
using namespace std;

class PrivateAccessError
{
private:
	int a;
	void f();
	PrivateAccessError();
public:
	int b;
	PrivateAccessError(int x);
	void g();
};

PrivateAccessError::PrivateAccessError()
{
	a = 1; //(1)
	b = 1; //(2)
}
PrivateAccessError::PrivateAccessError(int x)
{
	a = x; //(3)
	b = x; //(4)
}
void PrivateAccessError::f()
{
	a = 5; //(5)
	b = 5; //(6)
}
void PrivateAccessError::g()
{
	a = 6; //(7)
	b = 6; //(8)
}

int main()
{
	PrivateAccessError objA; //(9) 
	PrivateAccessError objB(100); //(10)
	objB.a = 10; //(11)
	objB.b = 20; //(12)
	objB.f(); //(13) 
	objB.g(); //(14)
}
```
- (9) 생성자 PrivateAccessError()는 private 이므로 main()에서 호출할 수 없다
- (11) a는 PrivateAccessError 클래스의 private 멤버이므로 main()에서 접근할 수 없다
- (13) f()는 PrivateAccessError 클래스의 private 멤버이므로 main()에서 호출할  수 없다
- ![[Pasted image 20230415190653.png]]
- 생성자도 private으로 선언은 가능하지만, 한 클래스에서 오직 하나의 객체만 생성할 수 있도록 위한 것이다 (singleton)