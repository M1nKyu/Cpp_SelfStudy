# string 클래스 개요
- C++에서 문자열을 다루는 방법은 2가지
	- C-스트링
		- 전통적 문자열, '`\0`'으로 끝나는 문자 배열을 문자열로 취급
		- 할당받은 메모리 크기 이상 문자열 저장 불가능
	- string 클래스
		- 표준 라이브러리에서 제공하는 클래스
		- 문자열을 **객체로 다룬다**
		- `#include <string>`필요
		- 문자열 크기에 맞추어 스스로 메모리 크기 조절
			- 저장되는 문자열 크기 염려하지 않아도 된다. 
```cpp
#include <string>
using namespace std;
...

string str = "I love "; // 공백 포함 7개의 문자로 구성
str.append("C++."); // str은 "I love C++."이 된다
```
---
# string 객체 생성 및 출력
## string 객체 생성
- 다양하게 문자열 생성 가능
- **문자열 크기에는 제한 없다**
```cpp
strign str; // 빈 문자열을 가진 스트링 객체
string address("서울시 성북구 삼선동 389"); // 문자열 리터럴로 초기화
string copyAddress(address); // address를 복사한 copyAddress 생성

// C-스트링(char [] 배열)로부터 스트링 객체 생성
char text[] = {'L', 'o', 'v', 'e', ' ', 'C', '+', '+', '\0' }; 
string title(text); // "Love C++"을 가진 string 객체 생성
```

## string 객체가 가진 문자열 출력
- `cout <<` 사용
```cpp
cout << address << endl; // "서울시 성북구 삼선동 389"
cout << title << endl; // "Love C++"
```

## string 객체의 동적 생성
```cpp
string *p = new string("C++"); // 스트링 객체 동적 생성
cout << *p; // "C++"
p->append(" Great!!") // p가 가리키는 스트링이 "C++ Great!!"가 됨
cout << *p; // "C++ Great!!"
delete p; // 스트링 객체 반환
```

## 예제 4-11
```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
	//스트링 생성
	string str; // 빈 문자열 스트링 객체
	string address("서울시 성북구 삼선동 189");
	string copyAddress(address);

	char text[] = { 'L', 'o', 'v', 'e', ' ', 'C', '+', '+', '\0' };
	string title(text);

	cout << str << endl;
	cout << address << endl;
	cout << copyAddress << endl;
	cout << title << endl;
}
[출력]

서울시 성북구 삼선동 189
서울시 성북구 삼선동 189
Love C++
```
---
# string 객체에 문자열 입력
- `cin >>`을 이용하여 string 객체에 문자열 입력 가능
	- 하지만, 공백 문자가 입력되면 그 앞 까지만 문자열로 다룸
```cpp
string name;
cin >> name;
```

- 공백 포함하여 입력받기 위해서 `getline()`사용
```cpp
string name;
getline(cin, name, '\n'); // \n을 만날 때 까지 문자열을 읽어 name에 저장
```
- `cin.getline()`과는 다르다.

## 예제 4-12
- string 클래스 연산자
	- `<, >, ==`는 두 문자열의 사전순서를 비교 또는 동일여부 확인 가능
	- `+`는 두 문자열을 이어주는 역할
```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
	string names[5];

	for (int i = 0; i < 5; i++)
	{
		cout << "이름 >> ";
		getline(cin, names[i], '\n');
	}

	string latter = names[0];
	for (int i = 0; i < 5; i++)
	{
		if (latter < names[i])
			latter = names[i];
	}
	cout << "사전에서 가장 뒤에 나오는 문자열은 " << latter << endl;
}
[출력]
이름 >> 가나다라
이름 >> 마바사
이름 >> 아자차카
이름 >> 타파하
이름 >> 강민규
사전에서 가장 뒤에 나오는 문자열은 타파하
```
