# 동적 메모리 할당
- 실행중 필요한 만큼 메모리를 할당받고 반환하는 '동적 메모리 할당/반환 메커니즘' 필요
- C언어 : malloc() / free() 함수 사용
- C++ : new / delete 연산자 사용
	- new : 힙(heap) 공간으로부터 메모리 할당받음
	- delete : 할당받은 메모리를 힙으로 반환

# new 와 delete 연산자
```cpp
// 기본 형식
데이터타입 *포인터변수 = new 데이터타입;
delete 포인터변수;
```
- **new 연산자**
	- '데이터타입'의 크기만큼 힙으로부터 메모리를 할당받고 주소를 리턴
	- 그 결과, '포인터변수'는 할당받은 메모리의 주소를 가진다
- **delete 연산자**
	- '포인터변수'가 가리키는 메모리를 힙으로 반환
- 데이터 타입은 int, char, double 등 기본 타입 뿐만 아니라 구조체(struct), 클래스(class)도 포함
```cpp
int *pInt = new int; //int 타입의 정수 공간 할당
char *pChar = new char; // char 타입의 문자 공간 할당
Circle *pCircle = new Circle; // Circle 클래스 타입의 객체 할당

delete pInt; // 할당받은 정수 공간 반환
delete pChar; // 할당받은 문자 공간 반환
delete pCircle; // 할당받은 객체 공간 반환
```

- **힙 메모리가 부족하면 new는 NULL을 리턴**하므로,
	- new의 리턴값이 NULL인지 검사하는 것이 좋다
```cpp
int *p = new int; // 힙으로부터 int 타입의 정수 공간 할당

if(!p){ return; } // if(p == NULL)과 동일, 메모리 할당받기 실패 

*p = 5; // 할당받은 정수 공간에 5 기록
int n = *p; // 할당받은 정수 공간에서 값 읽기, n = 5
delete p; // 할당받은 정수 공간 반환
```

## 동적 할당 메모리 초기화
- new를 이용할때, '초깃값'을 지정하여 초기화할 수 있다.
	- 동적할당을 받으면서 초기화하는 것이다.
	- `데이터타입 *포인터변수 = new 데이터타입(초깃값);`
```cpp
int *pInt = new int(20); // 20으로 초기화된 int 공간 할당
char *pChar = new char('a'); // 'a'로 초기화돤 char 공간 할당
```

## delete 사용 시 주의
- 메모리를 반환할 때, 적절하지 못한 포인터를 사용하면, 실행오류 발생
```cpp
< 실행 오류 >
int n;
int *p = &n;
delete p; // p가 가리키는 메모리는 동적 할당받은 것이 아니므로 실행오류

< 정상 >
int *p = new int;
delete p; // 정상적인 메모리 반환
delete p; // 실행 오류, 이미 반환된 메모리를 중복 반환할 수 없다
```
- 이미 반환된 메모리를 **중복 반환할 수는 없다**

## 예제 4-5
```cpp
#include <iostream>
using namespace std;

int main()
{
	int* p;

	p = new int;
	if (!p)
	{
		cout << "메모리를 할당할 수 없습니다";
		return 0;
	}

	*p = 5;
	int n = *p;
	cout << "*p = " << *p << endl;
	cout << "n = " << n << endl;

	delete p;
}
[출력]
*p = 5
n = 5
```
---
# 배열의 동적 할당 및 반환