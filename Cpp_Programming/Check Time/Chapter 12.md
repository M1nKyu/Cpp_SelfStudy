# 03.
## 키보드로 전화번호와 이름을 입력받아 tel.txt 파일에 저장하는 프로그램, 빈칸 채우기
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main()
{
	// 1.(fout을 생성한다)
	if(!fout) return 0;
	char tel[100], name[100];
	cin >> tel >> name;
	// 2.(파일에 전화번호와 이름 저장)
	// 3.(스트림을 닫는다)
}
```
---
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main()
{
	ofstream fout("c:\temp\tel.txt"); //1
	if(!fout) return 0;
	char tel[100], name[100];
	cin >> tel >> name;
	fout << tel << name; //2
	fout.close(); //3
	
}
```
