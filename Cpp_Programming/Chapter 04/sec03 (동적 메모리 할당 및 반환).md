- 동적 vs 정적
	- 정적
		- 코딩 단계에서 메모리 사이즈 결정, 실행 도중 변경 불가
		- 처음에 결정된 크기보다 더 큰 입력 -> **처리하지 못함**
		- 반대로 더 작은 입력 -> **남은 메모리 공간 낭비**
	- 동적
		- 프로그램 실행 이후 동적으로 메모리를 할당 받을 수 있음
		- 필요한 만큼만 할당
			- 메모리 부족 걱정없고, 낭비 없음
			- 할당 -> 사용 -> 반납
---
# 동적 메모리 할당
- 실행중 필요한 만큼 메모리를 할당받고 반환하는 '동적 메모리 할당/반환 메커니즘' 필요
- C언어 : malloc() / free() 함수 사용
- C++ : new / delete 연산자 사용
	- new : **힙(heap) 공간**으로부터 메모리 할당받음
	- delete : 할당받은 메모리를 **힙으로 반환**
---
# new 와 delete 연산자
```cpp
// 기본 형식
데이터타입 *포인터변수 = new 데이터타입;
delete 포인터변수; //❗delete *변수 (X) 
```
- **new 연산자**
	- '데이터타입'의 크기만큼 힙으로부터 메모리를 할당받고 주소를 리턴
	- 그 결과, '포인터변수'는 할당받은 메모리의 주소를 가진다
- **delete 연산자**
	- '포인터변수'가 가리키는 메모리를 힙으로 반환
- ❗❗데이터 타입은 int, char, double 등 **기본 타입** 뿐만 아니라 **구조체(struct), 클래스(class)** 도 포함
```cpp
int *pInt = new int; //int 타입의 정수 공간 할당
char *pChar = new char; // char 타입의 문자 공간 할당
Circle *pCircle = new Circle; // Circle 클래스 타입의 객체 할당

delete pInt; // 할당받은 정수 공간 반환
delete pChar; // 할당받은 문자 공간 반환
delete pCircle; // 할당받은 객체 공간 반환
```

- **힙 메모리가 부족하면 new는 ❗NULL을 리턴**❗하므로,
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
	- ❗`데이터타입 *포인터변수 = new 데이터타입(초깃값);`❗
```cpp
int *pInt = new int(20); // 20으로 초기화된 int 공간 할당
char *pChar = new char('a'); // 'a'로 초기화돤 char 공간 할당
```

## ❗delete 사용 시 주의❗
- 메모리를 반환할 때, 적절하지 못한 포인터를 사용하면, 실행오류 발생
```cpp
< 실행 오류 >
int n;
int *p = &n;
delete p; // p가 가리키는 메모리는 동적 할당받은 것이 아니므로 실행오류

< 정상 >
int *p = new int;
delete p; // 정상적인 메모리 반환
```
- 이미 반환된 메모리를 **중복 반환할 수는 없다**
```cpp
int *p = new int;
delete p; // 정상적인 메모리 반환
delete p; // 실행 오류, 이미 반환된 메모리를 중복 반환할 수 없다
```

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

	*p = 5; // 할당받은 정수 공간에 5 삽입
	int n = *p;
	cout << "*p = " << *p << endl;
	cout << "n = " << n << endl;

	delete p; 
} // }와 함께 스택의 모든 데이터 없어짐.

[출력]
*p = 5
n = 5
```
---
# 배열의 동적 할당 및 반환
- new, delete 연산자로 배열을 할당받고 반환할 수 있음
## 배열의 동적 할당/변환의 기본 형식
```cpp
데이터타입 *포인터변수 = new 데이터타입 [배열의크기]; // 배열의 동적 할당
delete [] 포인터변수; // 배열 메모리 반환
```

- int 배열을 할당받고 0, 1, 2, 3, 4를 배열에 기록하는 예제
```cpp
int *p = new int [5];
if(!p) // 메모리할당 실패시
	return;
	
for(int i = 0; i < 5; i++)
	p[i] = i; // 배열에 순서대로 기록
	
delete [] p; // 배열 메모리 반환
```
- **p가 배열에 대한 포인터이므로, 다음과 같이 쓸 수 있음.**
	- ❗` *(p+i) = i; `

## 예제 4-6
```cpp
#include <iostream>
using namespace std;

int main()
{
	cout << "입력할 정수의 개수는?";
	int n;
	cin >> n;

	if (n <= 0) return 0;
	int* p = new int[n]; //n개의 정수 배열 동적 할당, 대괄호 사이 공백없어도 되는듯
	if (!p)
	{
		cout << "메모리 할당 불가";
		return 0;
	}
	for (int i = 0; i < n; i++)
	{
		cout << i + 1 << "번째 정수: "; 
		cin >> p[i]; // 정수 입력
	}
	int sum = 0;
	for (int i = 0; i < n; i++)
		sum += p[i];
	cout << "평균 = " << sum / n << endl;
	
	delete[] p; //배열 메모리 반환
}


[출력]
입력할 정수의 개수는?4
1번째 정수: 4
2번째 정수: 20
3번째 정수: -5
4번째 정수: 9
평균 = 7
```
## ❗배열을 초기화할 때 주의사항❗
- 배열은 다음과 같이 **동적 할당 시 초기화 불가능하다**
```cpp
int *pArray = new int [10](20); // 구문오류, 초기화 불가
int *pArray = new int(10)[20]; // 구문오류
```

- ❗다음과 같이 지정 가능❗
```cpp
int *pArray = new int [] {1, 2, 3, 4}; // 1, 2, 3, 4로 초기화된 정수배열 생성
```

- ❗기본 타입인 경우 동적 할당시 초기화 가능하다❗
```cpp
int *pInt = new int(30);
int *pChar = new char('a');
```
---
## ❗배열을 delete할때 주의사항
```cpp
int *p = new int [10];
delete p; // 비정상 반환, delete [] p; 로 해야함

int *q = new int;
delete [] q; // 비정상 반환, delete q;로 해야함
```
