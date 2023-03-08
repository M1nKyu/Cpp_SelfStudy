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
