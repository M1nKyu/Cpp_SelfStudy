- `<<, >>` 연사자를 이용하여 간단히 텍스트 파일을 읽고 쓸 수 있음

# 파일 쓰기를 위한 스트림 객체 생성
- 텍스트 정보를 파일로 작성하기 위해서는
	- 우선 다음과 같이 ofstream 클래스를 이용하여 파일 출력 스트림 객체를 생성
		- `ofstream fout; // 파일 출력 스트림 객체 fout 생성`
---
# 파일 열기
- 텍스트 데이터를 **파일에 쓰기 전**에, 파일명을 매개변수로 하고 fout 객체의 
	- `open()` 멤버 함수를 호출하여 **파일을 열어 스트림에 연결**해야 한다
		- `fout.open("song.txt"); // song.txt 파일 열기`
			- 파일이 존재하지 않는다면, 빈 파일을 새로 만듬
				- 파일이 존재한다면 기존 song.txt 파일의 내용을 모두 지우고 파일의 맨 앞에서부터 쓸 준비를 한다
- 파일 열기는 **출력 스트림에 파일을 연결하는 과정**
	- 이 과정에서 song.txt가 읽기 전용 파일로 이미 존재하거나,
		- 디스크 용량이 모자라는 등 파일 만들기가 불가능한 경우
			- 파일열기가 실패한다
- `open()` 함수를 사용하지 않고 다음과 같이 가능
	- `ofstream fout("song.txt"); // 파일 출력 스트림 생성과 동시에 파일 열기` 
---
# 파일 열기 성공 검사
- 파일 열기가 실패하면 파일 쓰기를 더이상 진행할 수 없음
	- 다음과 같이 파일 열기 성공 여부를 확인
```cpp
if(!fout){ // fout 스트림의 파일 열기가 실패한 경우
	... // 파일 열기 실패를 처리하는 코드
}
```

- `!fout`은 fout 스트림의 `operator!()`연산자 함수를 실행
	- `operator!()` 함수는 파일 열기가 실패한 경우 true, 성공한 경우 false 리턴

- `is_open()`함수로도 파일 열기를 검사할 수 있음
	- 성공한 경우 true, 실패한 경우 false 리턴
```cpp
if(!fout.is_open()){ // fout 스트림의 파일 열기가 실패한 경우
	... 
}
```
---
# <<연산자를 이용한 파일 쓰기
```cpp
int age = 21;
char singer[] = "Kim";
char song[] = "Yesterday";

ofstream fout("song.txt");
if(!fout) return;
fout << age << '\n'; // 파일에 21과 "Kim"을 기록한다
fout << singer << endl; // 파일에 "Kim"과 '\n'을 덧붙여 기록한다
fout << song << endl; // 파일에 "Yesterday"와 '\n'을 덧붙여 기록한다 
```
---
# 파일 닫기
- 파일 쓰기를 마치면 다음과 같이 `close()`함수를 호출하여 파일을 닫는다.
	- `close()`이후에 fout을 이용하여 파일 쓰기를 할 수 없다
		- 다시 파일을 열어야 쓸 수 있음
```cpp
fout.close()
```
---
## 예제 12-1
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main()
{
	char name[10], dept[20];
	int sid;
	cout << "이름>>";
	cin >> name;
	cout << "학번(숫자로)>>";
	cin >> sid;
	cout << "학과>>";
	cin >> dept;
	ofstream fout("student.txt");
	if (!fout)
	{
		cout << "student.txt 파일을 열 수 없다";
		return 0;
	}
	fout << name << endl;
	fout << sid << endl;
	fout << dept << endl;

	fout.close();
}
```
---
# >>연산자를 이용한 텍스트 파일읽기
- 우선 ifstream 클래스를 이용하여 파일입력 스트림 객체를 생성
```cpp
ifstream fin;
```
- 그리고 `open()` 함수를 이용하여 파일을 열고, 열기의 성공 여부를 검사
```cpp
fin.open("c:\\temp\\student.txt");
if(!fin){
	cout << "파일을 열 수 없습니다";
	return 0;
}
```
- 파일열기를 성공했으면 >> 연산자를 이용하여 텍스트 데이터를 읽는다
```cpp
char name[10], dept[20];
int sid;
fin >> name; 
fin >> sid;
fin >> dept;
```
- 파일 읽기를 마치면 파일을 닫는다
```cpp
fin.close();
```
## 예제 12-2
- student.txt 파일을 읽고 화면에 출력하는 프로그램
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main()
{
	ifstream fin;
	fin.open("student.txt");
	if(!fin){
		cout << "파일을 열 수 없습니다";
		return 0;
	}
	char name[10], dept[20];
	int sid;

	fin >> name;
	fin >> sid;
	fin >> dept;
	
	cout << name << endl;
	cout << sid << endl
	cout << dept << endl;

	fin.close();
}
```