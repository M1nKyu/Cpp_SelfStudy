# main() 함수
## 표준 형식
- C++에서 main() 함수의 **리턴 타입은 int**
```cpp
int main()
{
	............
	return 0; //생략가능
}
```
- void는 표준이 아니며  **int main()으로 하는 것이 좋다**
- int main() 함수에서 **return 문은 생략이 가능**하다
	- 편의를 위해 return문이 생략되면 자동으로 `return 0;` 이 실행된다.
---
# [전처리기 (preprocessor)](https://boycoding.tistory.com/145)
- 전처리기란 프로그램을 컴파일할 때 **컴파일 직전에 실행**되는 별도의 프로그램
- 전처리기가 실행되면 각 코드파일에서 ==지시자(directives)==를 찾는다
	- 지시자 : `#`으로 시작해서 줄바꿈으로 끝나는 코드
- `include <iostream>` 은 전처리기(C++ Preprocessor)에 대한 지시문

- `#include`를 하면 전처리기는 포함(include)된 파일의 내용을 지시자의 위치에 *복사*
## 헤더파일 (Header file)
- .cpp 확장자를 가진 코드파일은 C++ 프로그램의 유일한 파일이 아니다. 다른 유형의 파일을 헤더파일(header file)이라고 한다
- 보통 `.h`확장자를 가지며, 다른파일에 대한 선언을 가지고 있음

- `#include <filename>`
	- `<>`는 헤더파일을 include할 때 사용한다. 
	- *컴파일러가 설치된 폴더*에서 찾으라는 지시

- `#include "filename"`
	- `""`는 소스파일이 있는 디렉터리에서 헤더파일을 include하도록 전처리기에 지시
	- 이와 같은 방법으로 **자신이 작성한 헤더파일을 include함**

- ==표준 라이브러리 헤더 파일==
	```cpp
	#include <iostream>
	int main()
	{
		std::cout << "Hello, World!" << std::endl;
		return 0;
	}
	```
	- 위 프로그램은 cout를 정의하지 않았지만 iostream 헤더파일에 선언돼있어 오류가 발생하지 않는 것
	- `#include <iostream>`을 사용하면 iostream이라는 헤더파일의 모든 내용을 복사해오도록 요청
---
# 화면 출력
- `cout` 과 `<<` 연산자를 이용하여 화면출력
```cpp
std::cout << "Helloe\n";
```

## cout 객체
- 스크린 장치와 연결된 C++ **표준 출력 스트림 객체(Standard Output Stream Object)**
- `std::` 접두어는 `cout`의 [이름공간(namespace)](obsidian://open?vault=Obsidian%20Vault&file=Cpp_Programming%2FChapter%2002%2Fsec%2002%20(namespace%EC%99%80%20std))이 std임을 표시

## << 연산자
- ==스트림 삽입 연산자(Stream Insertion operator)==로 불림
- 오른쪽 피연산자를 **왼쪽 스트림 객체**에 삽입
- **원래는 비트 shift 연산자**
	- 스트림 삽입 연산자로 재정의 된 것(다형성)

- 여러개의 `<<`연산자를 사용하여 여러개의 데이터를 출력할 수 있다
```cpp
std::cout << "Hello\n" << "안녕하세요.";
```

- 다음 줄로 넘어가기
```cpp
1.\n 문자 이용
std::cout << "Hello" << \'n';

2. endl 조작자 사용
std::cout << "Hello" << std::endl; (소문자L)
```

- `endl` 은 C++에서 도입한 *조작자*(manipulator)라고 불리는 함수다

## 예제 2-2
- **true는 1로 출력**
```cpp
# include <iostream>

//함수 원형 선언
double area(int r);  

//함수 구현 
double area(int r)
{
	return 3.14 * r * r;
}

int main()
{
	int n = 3;
	char c = '#';
	
	std::cout << c << 5.5 << '-' << n << "hello" << true << std::endl; //endl을 통해 한칸 띄움
	std::cout << "n + 5 = " << n + 5 << '\n';
	std::cout << "면적은 " << area(n);
}
/*
[출력]
#5.5-3hello1
n + 5 = 8
면적은 28.26
*/
```