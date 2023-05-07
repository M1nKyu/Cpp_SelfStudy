# C++의 문자열
- C++에서 문자열은 기본데이터 타입이 아니며 다음 두 방법으로 표현
	1. C-스트링 : C언어에서 문자열을 표현하는 방법
	2. (권장) **string 클래스 : 문자열을 객체로 다루는 방법**
---
# 첫번째 방법 : C - 스트링
- 널 문자 (`'\0' 또는 0`)으로 끝나는 char 배열
```cpp
/*
name1은 문자열 "Grace"
name2는 문자열이 아니다. ❗단순 문자 배열이다. '\0'이 없기 때문❗
*/
char name1[6] = {'G', 'r', 'a', 'c', 'e', '\0'}; 
❗ char name2[5] = {'G', 'r', 'a', 'c', 'e'};
```
- 문자열 리터럴을 직접 배열에 저장하여 문자열을 만들 수도 있음
	- 배열의 크기는 문자수 보다 **최소한 1은 커야하며 많이커도 상관없음**
```cpp
char name3[6] = "Grace"; 
char name4[] = "Grace"; // 배열의 크기가 6으로 자동 설정
char name5[10] = "Grace"; // 많이커도 상관 없음
```

- `char name5[10] = "Grace"; `의 실행결과
| `[0]` | `[1]` | `[2]` | `[3]` | `[4]` | `[5]`  | `[6]`  | `[7]`  | `[8]`  | `[9]`  | `[10]` |
| ----- | ----- | ----- | ----- | ----- | ------ | ------ | ------ | ------ | ------ | ------ |
| 'G'   | 'r'   | 'a'   | 'c'   | 'e'   | `'\0'` | `'\0'` | `'\0'` | `'\0'` | `'\0'` | `'\0'` | `'\0'`

- C-스트링을 다루기 위해 C 프로그래밍에서의 `strcpy()`, `strcmp()`, `strlen()`등의 함수를 사용 가능
	- **이때 `<cstring>` 헤더 파일을 include해야한다**

### C++에서 한글 비트수
- 영어나 숫자는 한글자 당 *1비트*
- 한글은 한 글자당 *2비트*
- 예시
	- "C++" : 3비트, `최소 array[4]`
	- "씨쁠쁠 " : 6비트, `최소 array[7]`
---
# cin 문자열 입력
- cin과 >>연산자를 이용하여 간단히 문자열을 입력받을 수 있다.
	```cpp
	char name[6]; // 5개의 문자로 구성된 문자열을 저장할 수 있는 char배열
	cin >> name;
	```
- 위의 name[] 배열의 크기가 6이기 때문에 반드시 5개 이하의 문자만 입력할 수 있다
	- *6개이상 입력하면 실행오류 발생*
- ❗**공백없이 입력**하여야 정상적으로 입력된다

## 예제 2-4
```cpp
#include <iostream>
using namespace std;

int main()
{
	cout << "이름을 입력하세요 >> ";

	char name[11];
	cin >> name;

	cout << "이름은 " << name << "입니다\n";
}
```

## 예제 2-5
```cpp
#include <iostream>
#include <cstring>
using namespace std;

int main()
{
	char password[11];
	cout << "프로그램을 종료하려면 암호를 입력하세요. \n";
	while (true)
	{
		cout << "암호>>";
		cin >> password;

		if (strcmp(password, "C++") == 0)
		{
			cout << "프로그램을 정상 종료합니다." << endl;
			break;
		}
		else
		{
			cout << "암호가 틀립니다." << endl;
		}
	}
}
```
### strcmp() [..](https://blockdmask.tistory.com/391)
- 두개의 문자열이 같은지 검사 하는 함수
- ❗헤더파일 : `<cstring>`
- 정의 : `int strcmp(const char* str1, const char* str2)`
- 리턴값
	- 두개의 문자열을 비교해서 **같으면 0**을 리턴
	- str1 > str2 일 경우 양수
	- str1 < str2 일 경우 음수
	- ![[strcmp return.png]]
#### strncmp()
- 두개의 문자열이 원하는 길이만큼 같은지 검사

#### strcmp , strncmp 예제[..](https://coding-factory.tistory.com/594)
```cpp
#include <iostream>
#include <cstring>
using namespace std;

int main()
{
	char s1[10] = "aaa";
	char s2[10] = "aaa";
	char s3[10] = "aab";

	int compare1 = strcmp(s1, s2);
	int compare2 = strcmp(s1, s3);
	int compare3 = strcmp(s3, s1);

	int compare4 = strncmp(s1, s3, 2); //입력된 문자열을 2번째까지 비교한다
	int compare5 = strncmp(s3, s1, 2);

	cout << "결과1 : " << compare1 << endl;
	cout << "결과2 : " << compare2 << endl;
	cout << "결과3 : " << compare3 << endl;

	if (!strcmp(s1, s2)) cout << "s1과 s2는 같다\n";
	if (strcmp(s1, s3)) cout << "s1과 s3은 다르다\n";
	if (strcmp(s1, s3)) cout << "s1과 s3은 다르다\n";

	cout << "결과4 : " << compare4 << endl;
	cout << "결과5 : " << compare5 << endl;

	if (!strncmp(s1, s2, 2)) cout << "s1과 s2는 2째 자리까지 같습니다\n";
	if (!strncmp(s1, s3, 2)) cout << "s1과 s2는 2째 자리까지 같습니다\n";
}
```
#### strcpy(a, b)
- a에 b 복사 
---
# cin과 >> 연산자로 문자열 입력할 때의 허점
- `>>`연산자는 ==공백문자(white space character)==를 만나면 공백 전까지만 문자열로 인식한다
	- `이름을 입력하세요 >> 마 이 클`
		- `이름은 마입니다`
			- 이런식으로 공백문자를 만나 문자열 "마"의 입력이 종료된 것으로 판단

##### 공백문자(white space character)란?
- 줄 사이에 사용자가 읽기쉽도록 삽입하는 문자로서
	- (`' '`), (`'\t'`), (`'\n'`), (`'\r'`), (`'\f'`), (`'\v'`)
		- `\r : 캐리지 리턴`, `\f : 폼피드`, `\v : 수직 탭`
		- 문자가 공백문자인지 확인하는 함수 : `int isspace(char c);`
			- 공백문자이면 true(0이아닌정수) 리턴

---
# cin.getline()으로 공백이 포함된 문자열 입력
- cin 객체의 `getline() 멤버 함수`를 이용하면 공백이 포함된 문자열을 입력받을 수 있음
- 함수의 원형
	- `cin.getline(char buf[], int size, char delimitChar)`
		- buf : 키보드로부터 읽은 문자열을 지정할 배열
		- size : buf[ ] 배열의 크기
		- delimitChar : 문자열 입력 끝을 지정하는 구분 문자
		- ==과정==
			1. size -1 개의 문자를 입력받거나, *delimitChar로 지정된 문자를 만나면 문자열 입력 종료*
			2.입력된 문자열은 buf[] 배열에 저장되며, delimitChar로 지정된 문자는 저장되지 않고 cin 버퍼에서도 사라진다
			3. buf[] 배열에 *널문자 (`\0`)가 덧붙여진다.*

- 엔터키를 구분 문자로 지정하여 문자열 입력받는 예
	```
	char address[100];
	cin.getline(address, 100, '\n'); //엔터키가 입력될때까지 최대 99개의 문자 입력
	```
| 'S' | 'e' | 'o' | 'u' | 'l' | '  ' | 'K' | 'o' | 'r' | 'e' | 'a' | '`\0`' | ... |
| --- | --- | --- | --- | --- | ---- | --- | --- | --- | --- | --- | ------ | --- |
	위 코드에서 사용자가 'Seoul Korea <`Enter`>'를 입력할때의 결과이다.

- `cin.getline()`은 delimitChar를 생략할 수 있다
	- 디폴트 값이 `\n`이다 
		- `cin.getline(address, 100);` 이런식으로 간소화할 수 있다
		- ❗키보드로 만약 배열보다 긴 문장을 넣었다면, 에러가 나지않고 **자동으로 CUT**
## 예제 2-6
```cpp
#include <iostream>
using namespace std;

int main()
{
	cout << "주소 입력:";

	char address[100];
	cin.getline(address, 100, '\n');

	cout << "주소는 " << address << "이다\n";
}

[출력]
주소 입력: 어디어디 어디어디 어디 몇호
주소는 어디어디 어디어디 어디 몇호이다
```
---
# 두번째 방법 : string 클래스 (선호)
- **문자열의 크기에 제약이 없다**
	- string 클래스가 문자열 크기에 맞게 *내부 버퍼 조절*
- **객체지향적이다**
- **C-스트링 방식보다 문자열을 다루기 쉽다**
- 다양한 멤버 함수와 연산자 제공
- ❗`<string>` 헤더파일에 선언
	- `#include <string>` 필요
- **`cin >>`으로도 입력이 가능하다**

## 예제 2-7
- **string은 char 배열과는 달리 이퀄기호를 이용해서 비교 가능**
```cpp
#include <iostream>
#include <string> // string 클래스를 사용하기 위한 헤더파일
using namespace std;

int main()
{
	string song("Falling in love with you"); //문자열 song
	string elvis("Elvis Presley"); //문자열 elvis

	string singer;

	cout << song + "를 부른 가수는??";
	cout << " (힌트 : 첫 글자는 " << elvis[0] << ")\n"; //[]연산자 사용

	getline(cin, singer); // getline() <string>에 정의돼있음, cin.getline()아님.
	if (singer == elvis) cout << "맞았습니다";
	else cout << "틀렸습니다. 정답은 " + elvis + "입니다." << endl;
}

[출력]
Falling in love with you를 부른 가수는?? (힌트 : 첫 글자는 E)
Elon musk
틀렸습니다. 정답은 Elvis Presley입니다.
```
### getline()
- `<string>`에 저장되어 있음
- string형에 문자열 저장시 사용
- string 타입의 문자열을 입력받기 위해 제공되는 ❗**전역함수**❗
```cpp
#include <iostream>
#include <string>

int main()
{
   string str;
    
   getline(cin,str); // 표준입력방식으로 str에 문자열 끝까지 저장
   getline(cin,str,s); // 표준입력방식으로 str에 's'까지 저장
}
```
---
# Check Time (2)
- ' . '이 입력될 때까지 도시의 이름을 문자열로 입력받아 `char city[21]`배열에 저장하는 `cin.getline()` 호출 코드를 작성. 
```cpp
#include <iostream>
#include <cstring>
using namespace std;

int main() 
{
	char city[21];

	cout << "도시의 이름이 무엇인가요? :";
	cin.getline(city, 21, '.');

	cout << "도시의 이름은 " << city << "입니다";
}
[출력]
도시의 이름이 무엇인가요? :Pohang.
도시의 이름은 Pohang입니다
```
