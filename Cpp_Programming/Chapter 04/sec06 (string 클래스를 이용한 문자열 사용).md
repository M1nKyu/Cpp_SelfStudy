# string 클래스 개요
- C++에서 문자열을 다루는 방법은 2가지
	- C-스트링
		- 전통적 문자열, '`\0`'으로 끝나는 문자 배열을 문자열로 취급
		- 할당받은 메모리 크기 이상 문자열 저장 불가능
	- string 클래스
		- *표준 라이브러리*에서 제공하는 클래스
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

// ❗C-스트링(char [] 배열)로부터 스트링 객체 생성❗
char text[] = {'L', 'o', 'v', 'e', ' ', 'C', '+', '+', '\0' }; 
string title(text); // "Love C++"을 가진 string 객체 생성
```

## string 객체가 가진 문자열 출력
- `cout <<` 사용
```cpp
cout << address << endl; // "서울시 성북구 삼선동 389"
cout << title << endl; // "Love C++"
```

## ❗string 객체의 동적 생성
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
		getline(cin, names[i], '\n'); // '\n'은 기본값이라 생략가능
	}

	string latter = names[0];
	for (int i = 1; i < 5; i++)
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
### ❗==중요==❗위 코드를 char 배열로 구현하면❗❗
```cpp
#pragma warning (disable:4996) /* visual studio 경우 */
#include <iostream>
#include <cstring> // 헤더파일은 cstring
using namespace std;
int main() 
{
❗	char names[5][20]; // char 이차원배열. 이름의 최대길이 설정해야
	cout << "이름 5개를 입력하세요.\n";
	for (int i = 0; i < 5; i++) 
	{
		cout << i << "번: ";
		cin.getline(names[i], 20); // cin.getline()함수
	}
❗	char latter[20]; // 배열로 선언해야함
❗	strcpy(latter, names[0]); // char배열 대입
	for (int i = 1; i < 5; i++) 
	{
❗		if ( strcmp(latter, names[i]) < 0 )	// names[i]는 첫번째 문자
❗			strcpy(latter, names[i]); // char배열 대입
	}
	cout << "사전에서 가장 뒤에 나오는 이름은 " << latter << endl;
}
```
## string 클래스의 주요 멤버 함수
- ![[Pasted image 20230414215525.png]]
- ![[Pasted image 20230414215550.png]]
---
# 문자열 다루기
## 문자열 치환
- `=` 연산자 이용
```cpp
string a = "Java", b = "C++";
a = b; // a="C++"이 된다. a는 b를 복사한 문자열을 가짐
```

## 문자열 비교
- `compare()` 함수를 이용
	- 두 문자열이 **같으면 0**, str보다 **사전 순**으로 앞에오면 음수, 뒤에오면 양수 리턴
```cpp
string name = "Kitae";
string alias = "Kito";
int res = name.compare(alias); //name와 alias 비교
if(res == 0) cout << "두 문자열이 같다."; // 같을때
else if(res < 0) cout << name << " < " << alias << endl; 
else cout << alias << " < " << name << endl;
[출력]
Kitae < Kito
```
- **다음과 같이 연산자를 이용하는 것이 더욱 효과적**
```cpp
if(name == alias) cout << "두 문자열이 같다";
if(name < alias) cout << name << "이 " << alias <, "보다 사전에서 먼저 나옴";
```
## 문자열 연결
- `append()` 
```cpp
string a("I");
a.append(" love "); // a = "I love "
```
- 문자열 연결은 `+, -` 연산자를 이용하자
## 문자열 삽입
- `insert()`
```cpp
string a("I love C++");
a.insert(2, "really "); // a = "I really love C++"
```
- ❗`replace()`
```cpp
// a의 인덱스 2부터 11개의 문자("really love")를 study로 대체
a.replace(2, 11, "study"); // a = "I study C++"
```
## 문자열 길이
- 문자열 길이는 문자열에 포함된 문자 개수를 말함
- 문자열의 길이 리턴 :`length()`, `size()`
- string 객체 내부 메모리 용량 리턴 : `capacity()`
```cpp
string a("I study C++");
int length = a.length(); // length = 11
int size = a.size(); // length()와 동일
int capacity = a.capacity(); // 스트링 a의 현재 용량 capacity = 31
```
## 문자열 삭제
- ❗`erase()` : 문자열의 일부분 삭제
- `clear()` : 문자열 완전히 삭제
```cpp
string a("I love C++");
a.erase(0, 7); // a의 처음부터 7개의 문자 삭제, a = "C++"
a.clear(); // a = ""
```
## ❗서브스트링❗
- `substr()` 
	- 문자열에서 일부분을 발췌한 문자열(서브스트링)을 얻을 수 있음
	- 실행후 b의 문자열 변화는 없음..
```cpp
string b = "I love C++";
string c = b.substr(2, 4); // b의 인덱스 2에서 4개의 문자열 리턴, c = "love"
string d = b.substr(2); // b의 인덱스 2부터 끝까지 문자열 리턴, d = "love C++"
```
## ❗문자열 검색❗
- `find()`
	- 문자열 내에 특정 문자열 존재하는지 검색
	- 발견하면 첫번째 인덱스 리턴,
		- **발견 못하면 -1 리턴**
```cpp
string e = "I love love C++";
int index = e.find("love"); // e에서 "love" 검색, 인덱스 2 리턴
index = e.find("love", index + 1); // e의 인덱스 3부터 "love" 검색, 인덱스 7 리턴
index = e.find("C#"); // 발견할 수 없음, -1 리턴
index = e.find('v', 7); // e의 인덱스 7부터 검색, 9 리턴
```
## 문자열의 각 문자 다루기
- `at()` 함수와 `[]`연산자는 둘 다 문자열의 특정 위치에 있는 문자를 리턴
	- `at()` 과 달리 ❗`[]`는 특정 문자를 다른 문자로 수정❗할 수 있다.
```cpp
string f("I love C++");
char ch1 = f.at(7); // C
char ch2 = f[7] // f.at(7)과 동일, C
f[7] = 'D'; // f는 "I love D++"

// f의 마지막 문자 얻기
char ch3 = f.at(f.length() - 1); // ch3 은 '+'
```
---
# 문자열의 숫자 변환, stoi()
- `stoi()`
	- 문자열을 숫자로 변환하는 전역함수
```cpp
string year = "2014";
int n = stoi(year); //n은 정수 2014를 가짐
```
---
# 문자 다루기
- string은 문자열만 다루지 **문자를 다루는 기능은 없음**
- 문자를 다루는 함수는 `<locale>`헤더 파일에 존재
- `<locale>` 헤더 파일에 있는 `toupper()`, `isdigit()`, `isalpha()` 함수 사용 예
```cpp
string a = "hello";
for(int i = 0; i < a.length(); i++) a[i] = toupper(a[i]); // a가 "HELLO"로 변경
cout << a; // HELLO
if(isdigit(a[0])) cout << "숫자";
else if(isalpha(a.at(0))) cout << "문자"; // a[0]은 문자 'H'
[출력]
HELLO문자
```
---
# 예제
## ❗❗예제 4-13❗❗
- 빈칸을 포함하는 문자열 입력받고
	- 한 문자씩 왼쪽으로 회전하도록 문자열을 변경하고 출력
```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
	string s;

	cout << "아래에 문자열을 입력하세요. 빈칸이 있어도 됩니다. (한글X)" << endl;
	getline(cin, s, '\n');
❗	int len = s.length();

❗	for (int i = 0; i < len; i++)
	{
❗		string first = s.substr(0, 1); // 0 부터 1개, 즉 첫번째 문자
❗		string sub = s.substr(1); // 1번 부터 끝까지
❗		s = sub + first; // 회전 효과
❗		cout << s << endl;
	}
}
[출력]
I love sleep
 love sleepI
love sleepI
ove sleepI l
ve sleepI lo
e sleepI lov
 sleepI love
sleepI love
leepI love s
eepI love sl
epI love sle
pI love slee
I love sleep
```
### 한글입력
```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
	string s;

	cout << "아래에 문자열을 입력하세요. 빈칸이 있어도 됩니다. (한글)" << endl;
	getline(cin, s, '\n');
	int len = s.length();

❗	for (int i = 0; i < len; i+=2)
	{
❗		string first = s.substr(0, 2); // 0번부터 2칸
❗		string sub = s.substr(2, len-2); // 2번부터 len-2안써도됨
❗		s = sub + first; 
		cout << s << endl;
	}
}
```

### 한글 + 영어 
```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
	string s;

	cout << "아래에 문자열을 입력하세요. 빈칸이 있어도 됩니다. (한글)" << endl;
	getline(cin, s, '\n');
	int len = s.length();

	for (int i = 0; i < len; i++)
	{

		string first, sub;
		if (s[0] < 0) // 한글일때
		{
			first = s.substr(0, 2);
			sub = s.substr(2, len - 2);
			i++; // 한글이 2칸을 차지하니깐, i도 한칸 건너 뛰어야한다
		}
		else // 영어일때
		{
			first = s.substr(0, 1);
			sub = s.substr(1, len - 1);
		}
		s = sub + first;
		cout << s << endl;
	}
}
```
## 예제 4-14
```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
	string s;
	cout << "덧셈 문자열을 입력하세요";
	getline(cin, s, '\n');
	int sum = 0; // 계산한 값
	int start = 0; // 시작점, +를 만날때마다 시작점을 바꿀것이다.
	while (true)
	{
		int index = s.find('+', start); // 시작점부터 +의 인덱스를 찾음
		if (index == -1)
		{
			string part = s.substr(start); //마지막 수 저장
			if (part == "") break; // + 다음에 암것도 없다면 그냥 break
			sum += stoi(part); // ❗마지막 수도 정수로 바꿔서 sum에 더함
			break; //종료
		}
		// + 가 있을때
		int count = index - start; // 서브스트링으로 자를 문자 개수
		string part = s.substr(start, count); // 시작점과 + 사이의 숫자부분을 잘라서 저장, 
		cout << part << endl;
		sum += stoi(part);
		start = index + 1; //시작점을 + 뒤로 지정
	}
	cout << "숫자들의 합은 " << sum;
}
```
## ❗예제 4-15❗
- & 키가 입력될 때까지 여러줄의 영문 문자열을 입력받고
	- 찾는 문자열과 대치할 문자열을 각각 입력받아 문자열 변경
- `cin.ignore()` 
	- 입력버퍼에 하나 없애줌, 주로 엔터 처리
```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
	string s;
	cout << "여러 줄의 문자열을 입력하세요. 입력의 끝은 &문자." << endl;
	getline(cin, s, '&'); // & 나올때까지 입력
	cin.ignore(); // & 뒤에 따라오는 엔터키를 제거하기 위한 코드

	string f, r; // f : 찾을문자열, r : 대치할 문자열
	cout << endl << "find: ";
	getline(cin, f, '\n');
	cout << "replace: ";
	getline(cin, r, '\n');

	int startIndex = 0; // 시작점
	while (true)
	{
		int findex = s.find(f, startIndex); //findex는 검색한 단어의 인덱스
		if (findex == -1) break; // 없으면 종료
		s.replace(findex, f.length(), r); // findex 부터 문자열 f의 길이만큼 r로 변경
		startIndex = findex + r.length(); //다음 부분의 검색문자열을 찾기위해 시작점을 변경
	}
	cout << s << endl;
}
[출력]
i am your father. my father is strog
mmfathermm abcdefather&

find: father
replace: mother
i am your mother. my mother is strog
mmmothermm abcdemother
```

- 몇번 바뀐지 출력하는 코드 넣기
```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
	string s;
	cout << "여러 줄의 문자열을 입력하세요. 입력의 끝은 &문자." << endl;
	getline(cin, s, '&'); 
	cin.ignore(); 

	string f, r; 
	cout << endl << "find: ";
	getline(cin, f, '\n');
	cout << "replace: ";
	getline(cin, r, '\n');

	int startIndex = 0, count = 0; // count
	while (true)
	{
		int findex = s.find(f, startIndex); 
		if (findex == -1) break;
		s.replace(findex, f.length(), r); 
		count ++; // count ++
		startIndex = findex + r.length(); 
	}
	cout << s << endl;
	cout << count << "번 바뀜"; // count 출력
}