# 함수 호출에 따른 시간 오버헤드
- 오버헤드란 
	- 어떤 처리를 하기위해 들어가는 간접적인 처리 시간, 메모리 등을 말한다
![[함수호출 오버헤드.png]]

- 아래 코드는 함소 호출에 따른 시간오버헤드의 심각성을 보여준다
```cpp
#include <iostream>
using namespace std;

int main(){
	int sum = 0;

	//1에서 10000까지의 홀수의 합 계산
	for(int i = 1; i <= 10000; i++){
		if(odd(i))
			sum += i;	
	}
	cout << sum;
}

[출력]
25000000
```
- 이 코드는 odd() 함수의 코드 x%2를 계산하는 시간보다, 
	- odd() 함수의 호출과 리턴에 따른 오버헤드 시간이 더 크다
		- 그것도 10000번이나 호출하기 때문에 함수 호출 오버헤드는 더욱 가중된다
- 이처럼 **짧은 코드**를 함수로 만들면, **함수 호출의 오버헤드가 상대적으로 커서** 프로그램 실행시간이 길어지는 원인이 된다
---
# 인라인 함수 (inline function)
- 인라인 함수란 짧은 코드로 구성된 함수에 대해서,
	- 함수 호출 오버헤드로 인한 프로그램 *실행속도 저하를 막기 위해* 도입 
		- `inline` 키워드로 선언
```cpp
inline int odd(int x){ 
	return (x%2);
}
```

- 컴파일러는 인라인 함수를 호출하는 곳에 인라인 함수의 코드를 그대로 삽입하여 함수 호출이 일어나지 않게 한다
	- 함수 호출 오버헤드가 없어지기 때문에 실행속도가 빨라진다

```cpp
#include <iostream>
using namespace std;

inline int odd(int x){
	return (x%2);
}
int main(){
	int sum = 0;
	for(int i = 1; i<=10000; i++){
		if(odd(i))
			sum += i;
	}
	cout << sum;
}
```
⬇️컴파일에 의해 inline 함수의 코드 확장 삽입
```cpp
#include <iostream>
using namespace std;

int main(){
	int sum = 0;
	for(int i = 1; i <= 10000; i++){
		if((i%2)) // 확장 삽입
			sum += i;
	}
	cout << sum;
}
```
- **컴파일이 되고 나면 인라인 함수 odd()는 사라지고 odd()를 호출한 곳에 x%2만 존재한다**
	- odd() 함수 호출에 대한 오버헤드가 사라졌다
	- 매크로와 유사

## 인라인 함수의 장단점
- 작은 함수를 인라인으로 선언하면 **C++프로그램의 ❗실행속도❗를 향상**시킬 수 있다.
- 그러나 인라인 함수를 호출하는 곳에 인라인 함수의 코드를 단순 삽입하므로, 
	- **호출하는 곳이 여러군대** 있으면 그 만큼 **전체 크기가 늘어난다**
- 가능한 작은 함수를 인라인으로 선언하는 것이 현명

## 인라인 함수의 제약사항
- 컴파일러는 함수의 크기나 효율을 따져 불필요한 경우, inline 함수를 무시할 수도 있다.
- 컴파일러에 따라 *재귀함수(recursion), static 변수, 반복문, switch문, goto문* 등을 가진 함수는 인라인 함수로 허용하지 않는다
---
# 멤버 함수의 인라인 선언과 자동 인라인
- 생성자를 포함하여 클래스의 ❗**모든 멤버함수가 인라인으로 선언 가능**❗
- 멤버 함수의 크기가 작은 경우, 클래스의 선언부에 직접 구현하여도 무방
- **컴파일러**는 클래스 **선언부에 구현된 멤버함수**에 대해 inline **선언이 없어도** 인라인 함수로 자동 처리한다
	- 아래의 (a)코드와 (b)코드는 사실상 같다
(a)
```cpp
class Circle{
private:
	int radius;
public:
	Circle();
	Circle(int r);
	double getArea();
};
inline Circle::Circle(){
	radius = 1;
}
Circle::Circle(int r){
	radius = r;
}
inline double Circle::getArea(){
	return 3.14 * radius * radius;
}
```
(b)
```cpp
class Circle{
private:
	int radius;
public:
	Circle(){ //자동 인라인 함수
		radius = 1;
	}
	Circle(int r);
	double getArea(){ //자동 인라인 함수
		return 3.14 * radius * radius ;
	}
};
Circle::Circle(int r){
	radius = r;
}
```