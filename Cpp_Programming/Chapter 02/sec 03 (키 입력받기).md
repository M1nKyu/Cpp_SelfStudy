# 예제
```
#include <iostream>
using namespace std;

int main()
{
	cout << "높이 입력 >>";
	int height;
	cin >> height;

	cout << "너비 입력 >>";
	int width;
	cin >> width;

	cout << "넓이는 " << height * width << '\n';
	return 0;
}
```

# cin 과 >>연산자를 이용한 키 입력
- cin과 << 연산자는 `<iostream>` 헤더 파일에 선언되어 있음
	- `#include <iostream> 필요

- 여러개의 >> 연산자를 이용하여 **여러 값을 입력 받을 수** 있음
	```
	cin >> width >> height;
	cout << width << "\n" << height << "\n";
	```

## cin 객체
- cin은 C++ **표준 입력 스트림 객체** (standard input stream object)
-  키보드로 입력되는 값은 모두 **cin객체의 스트림 버퍼로 들어오며**
	- 응용프로그램은  cin객체로부터 입력된 키 값을 읽는다

## >>연산자
- 스트림 추출 연산자(stream extraction operator)로 불림
- 왼쪽의 피연산자(스트림객체)로 부터 데이터를 읽어 오른쪽 피연산자인 변수에 삽입
- `<iostream>` 헤더파일에 스트림 추출 연산자로 재정의(Overloading)돼있음

# 엔터 키를 칠 때 변수에 키 값 전달
- **엔터 키가 입력되면 비로소 >> 연산자가 cin의 입력 버퍼에서 키 값을 끌어내어 변수에 저장**
	- 만약 나이 19를 입력하기 위해 1을 입력하자마자 변수에 정수 1이 저장된다면 결코 19를 변수에 저장할 수 없을 것이다.

# 실행문 중간에 변수 선언
- C와 마찬가지로 C++도 **프로그램 어디서나 변수 선언 가능**
- 변수 사용은 변수가 선언된 라인 아래부터 적용
```
int width;
cin >> width; 

cout << "높이 입력:";

int height; //실행문 중간에 변수 선언
cin >> height; 

int area = width * height; //실행문 중간에 변수 선언
cout >> area;
```
## 장단점
- 장점
	1. 변수를 사용하는 코드 바로 위에 선언할 수 있음
		- 변수를 선언할 수 있어 코드 읽기 쉬움
		- 변수 이름을 잘못 타이핑하는 실수를 줄일 수 있음
- 단점
	- 흩어져 있으니 한 눈에 보기 힘들다


