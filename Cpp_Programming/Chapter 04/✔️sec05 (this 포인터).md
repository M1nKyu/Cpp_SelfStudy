# this의 기본 개념
- 객체 자신에 대한 포인터
- 클래스의 멤버 함수 내에서만 사용
	- **일반함수에 붙이면 안된다**.
- *전역변수도, 지역변수도 아니다*
	- 컴파일러가 선언한 변수
		- 멤버 함수에 컴파일러에 의해 묵시적으로 삽입되는 매개변수
- **`this.`으로 햇갈려하지 않도록**
	- ❗`this->`로 써야함❗
```cpp
class Circle{
	int radius;
public:
	Circle() { this->radius = 1; }
	Circle(int radius){ this->radius = radius; }
	void setRadius(int radius){ this->radius = radius; }
	...
};
```
---
# this와 객체
- 각 객체 속의 this는 다른 객체 속의 this와 서로 다른 포인터임
---
# this가 필요한 경우
## 1. 멤버변수의 이름과 동일한 이름의 매개변수 이름
```cpp
// 이 경우, this-> 를 생략해도 된다
Circle(){
	this->radius = 1; 
}

// 이 경우, this-> 가 필요하다
Circle(int radius){
	this->radius = radius;
}
```
## ❗2. 객체 자신의 주소를 리턴할 때❗
- 객체의 멤버 함수에서 객체 자신의 주소를 리턴할 때가 있다.
	- 이때 `this`가 반드시 필요
```cpp
class Sample{
public:
	Sample* p(){
		...
		return this; // 현재 객체의 주소 리턴
	}
}
```
## 3. 연산자 중복을 구현할 때..(7장에서)
---
# this의 제약 조건
- this는 클래스의 **멤버함수**에서만 사용할 수 있음
	- this는 객체를 가리킨다. 멤버함수가 아니라는 것은 어떤 객체에도 속하지 않는 것
- 멤버함수라도 **정적 멤버 함수**(**static** member function)는 this를 사용할 수 없다
	- 정적 멤버는 객체가 생성되기 전에 호출될 수 있음
---
