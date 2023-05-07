# 상속 선언
```cpp
// Student(파생클래스명), public(상속접근지정), Person(기본클래스명)
class Student : public Person {
	......
};

class StudentWorker : public Student {
	......
};
```
- 상속은 class 선언 뒤에, 콜론(:)과 기본 클래스 이름을 선언하면 된다
	- 기본 클래스 이름 앞에 반드시 상속접근을 지정해야 한다
---
# 파생 클래스 객체와 멤버 호출
## 예제 8-2
```cpp
#include <iostream>
#include <string>
using namespace std;

class Point{ // 2차원 폄면에서 한 점을 표현하는 Point 클래스 선언
	int x, y; // 한점에서의 좌표값
public:
	void set(int x, int y) { this->x = x; this->y = y;}
	void showPoint(){
		cout << "(" << x << "," << y << ")" << endl;
	}
};

class ColorPoint : public Point { // Point를 상속받음
	string color;
public:
	void setColor(string color) { this->color = color; }
	void showColorPoint();
};
void ColorPoint::showColorPoint(){
	cout << color << ":";
	showPoint(); // Point의 showPoint() 호출
}

int main(){
	Point p; // 기본 클래스의 객체 생성
	ColorPoint cp; // 파생 클래스의 객체 생성
	cp.set(3,4); // 기본 클래스의 멤버 호출
	cp.setColor("Red"); // 파생 클래스의 멤버 호출
	cp.showColorPoint(); // 파생 클래스의 멤버 호출
}

[출력]
Red: (3,4)
```
## 상속 선언
```cpp
class ColorPoint : public Point{
	...
};
```
## 파생 클래스 객체 생성
```cpp
Point p; // 기본 클래스 객체 생성
ColorPoint cp; // 파생 클래스 객체 생성
```
- 파생 클래스 객체는 기본 클래스 멤버와 파생 클래스의 멤버를 모두 가짐
## 파생 클래스에서 기본 클래스 멤버 접근
- 파생 클래스는 상속을 통해 기본 클래스의 멤버를 자신의 멤버로 확장
	- 파생클래스의 멤버들은 기본클래스의 private 멤버 이외에 모든 멤버를 접근할 수 있음
## 기본 클래스의 private 멤버의 상속과 접근
- 기본클래스에 선언된 private 멤버는 파생 클래스에 상속되고, 
	- 파생 클래스의 객체에도 포함되지만,
		- 파생 클래스의 어떤 함수에서도 직접 접근할 수 없다.
---
