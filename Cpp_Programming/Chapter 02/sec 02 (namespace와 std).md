# namespace (이름공간)
## 이름공간이란?
- 예를 들자면, 아파트 단지의 '마이클'이라는 사람이 여러명 있는데 1동의 마이클을 찾기 위해 
	- *1동::마이클* 이라고 찾는다
- 프로그래밍 과정에서 이름이 충돌하는 경우가 있다.
	- 예시
		- 프로젝트를 여러 명이 나누어 개발하는 경우
		- 다른 사람이 작성한 소스코드나 목적파일을 가져와서 사용하는 경우 등

- 서로다른 이름공간안에서 선언된 이름들은 별개의 이름으로 취급
## 생성, 이용 방법
### 생성
namespace 키워드 뒤에 자신만의 공간이름을 짓고 중괄호로 묶음
```
namespace [공간이름] { ... }
```
### 이용
```
이름공간(namespace) :: 이름(identifier)
```
### 예제
```
#include <iostream>

namespace OutterNamespace
{
	void myfunction()
	{
		int a = 3;
		int b = 4;
		std::cout << "Outter : " << a + b;
	}
	namespace InnerNamespace
	{
		void myfunction()
		{
			int a = 5;
			int b = 5;
			std::cout << "Inner : " << a + b;
		}
	}
}
int main()
{
	OutterNamespace::myfunction();
	std::cout << "\n";
	OutterNamespace::InnerNamespace::myfunction();
	return 0;
}

[출력]
Outter : 7
Inner : 10
```

# std:: 
## std::란?
- **표준 이름 공간**이다
- 모든 C++ 표준 라이브러리는 std 이름 공간에 만들어져 있음
	- 때문에 표준 라이브러리에서 선언된 이름은 `std::` 접두어를 붙여야 한다
	- `cout` 과 `endl`은 `std::`와 함께 사용

## std::의 생략
- std 이름공간(표준이름공간)에 선언된 수많은 이름을 사용할 때마다 `std::`를 붙이는 것은 번거로움
- ==using 지시어==를 이용하면 이름공간 접두어를 생략할 수 있다
```
using std::cout; // cout에 대해서만 std:: 셍략
......
cout << "Hello" << std::endl;
```

- 이름공간에 선언된 모든 이름에 대해서 `std::`를 생략하고자 한다면 namespace 키워드와 using지시어를 사용한다
```
using namespace std;
......
cout << "Hello" << endl;
```

