# `#`include `<`iostream`>`와 전처리기
- ==헤더 파일의 확장==
	- 전처리기가 `#include`문에 저장된 `<헤더파일>`의 텍스트를 `#include`문이 있던 자리에 삽입하는 것을  '헤더파일의 확장' 이라 한다

- `#include <iostream>`문을 처리하는 과정
	- `<iostream>파일은 <istream>파일을 include 하고 `
		- `<istream>파일은 <ostream>파일을 include 하며,
			- `다시 <ostream>파일은 <ios>파일을 include한다`
				- `<iostrean>, <istream>, <ostream>, <ios> 헤더파이 모두 소스파일 내에 확장되어 들어오게 되는 것이다. `
					- `확장이 끝나면 .cpp 파일이 컴파일된다`

# iostream 헤더파일은 어디에?
- 내 컴퓨터 기준
```
C:\Program Files\Microsoft Visual Studio\2022\Professional\VC\Tools\MSVC\14.35.32215 \include
```
- 위 폴더를 열어보면 `<iostream>`헤더 파일은 확장자가 없다
	- 2003년 C++표준부터 **헤더파일에 확장자를 붙이지 않기 때문이다**

# `<헤더파일>`과 `"헤더파일"`
- `#include <헤더파일>`
	- **컴파일러가 설치된 폴더**에서 헤더파일을 찾으라는 지시
- `#include "헤더파일"`
	- **개발자의 프로젝트 폴더**나 개발자가 컴파일 옵션으로 지정한 include 폴더에서 헤더파일을 찾도록 지시

# 헤더파일에는 무엇이 들어있는가?
- 일반적인 학생들의 답 : 함수의 코드가 들어있다.
	- 전혀 틀린 답이다. 
		- 함수에 대한 코드는 이미 컴파일된 기계어 형태로 C 라이브러리에 들어 있다
			- 실행중에 함수가 호출되면 C라이브러리의 코드를 호출하지 헤더파일의 무언가를 호출하는 것이 아니다
				- **헤더파일에는 함수의 원형만 들어있으며, 컴파일 할때 함수의 호출이 정확한지 판단하는데 사용된다**

# cout과 cin은 어디에 선언되어 있는가?
- cout과 cin은 모두 `<iostream>`헤더파일에 **선언된 객체**들이다
- 직접 `<iostream>`파일을 열어 확인해보면 
	- cin은 istream 타입
	- cout은 ostream 타입의 객체로 선언된 것을 볼 수 있음



