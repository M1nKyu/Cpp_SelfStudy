```cpp
---------------------------------- 기본타입✔️
int a = 5; // 기본
int b(5);   // c++에서 권장하기도 하지만 선택은 자유


int a; a = 5;
// int b; b(5);   // 괄호는 생성자 느낌이라서 두 줄로 하면 오류이구나 하고 생각하셔도 됩니다.

 

---------------------------------- string도 마찬가지✔️

string s1 = "Hello";
string s2("Hello");

string s1; s1 = "Hello";
//string s2; s2("Hello"); // 두 줄로 하면 오류


---------------------------------- 배열 중괄호 초기화는 선언할 때만 가능

int a[3] = { 10,20,30 };
int b[3]{ 11, 22, 33 };

// int a[3]; a = { 10,20,30 }; // 두 줄로 하면 오류
// int b[3]; b{ 11, 22, 33 }; // 두 줄로 하면 오류

 

class M {
int a[3] = { 10,5,33 }; // 멤버변수인 배열도 마찬가지 (이퀄기호 생략 가능)
};


class M {
int a[3];
M() {
// a = { 10,5,33 }; /* 이미 멤버변수 선언할 때 세미콜론 나왔다면 그 다음엔 중괄호 불가.

                         똑같은 값을 넣느냐 다양한 값을 넣느냐에 따라 다르겠지만, 
                         for문이든, fill함수든, 아니면 각각 인덱스에 하나씩 넣든
                         중괄호 말고 다른 방법으로 상황에 맞게 초기화해주세요!!  */
}
};


------------------------------------- char[]

char w1[20] = { 'H','e','l','l','o','\0' };  // 배열이므로 중괄호 초기화 당연히 가능
char w2[20]{ 'H','e','l','l','o','\0' };

❗char w3[20] = "Hello"; // 문자열이므로 큰따옴표 초기화도 가능. 가장 편리한 초기화 방법

/* char[]도 배열이므로 위 방법 모두 두 줄로 초기화하는 것은 안 됨 */


--------------------------------------- 객체변수 초기화

#include <iostream>
using namespace std;

class Student {
public:
int number; string name; double grade;
};
int main()
{
Student s1{ 1853330, "고흐", 3.7 };
Student s2 = { 100, "Hello", 9.9 };

❗//Student s1; s1{ 1853330, "고흐", 3.7 }; // 두 줄 안 됨
❗ Student s2; s2 = { 100, "Hello", 9.9 }; // 두 줄 가능 (C언어 구조체는 두 줄 불가했습니다.)

//Student s3(5, "bye", 3.14);
/* 객체변수 선언시 괄호는 생성자 호출이므로, 지금같은 경우 매개변수 3개짜리 생성자가
코딩되어 있어야 하는데, 생성자 코딩 없으므로 오류. 물론 생성자 코딩 되어있다 하더라도
Student s3; s3(5, "bye", 3.14); 이런 식의 두 줄은 당연히 안 됨 */


cout << s1.number << s1.name << s1.grade << endl;
cout << s2.number << s2.name << s2.grade << endl;

}

Student s = {1853330, "고흐", 3.7};
❗두줄로 쓸 수 있는가 (X)
❗Student s;
❗s = { ..., ..., ...}; (불가능..)
❗배열, 클래스의 초기화는 오직 변수 선언과 동시에만 가능..
<해결>
Student s;
s.number = ... ;
s.name = ... ;
s.grade = ... ;
```

```cpp
// 객체 배열 선언
Circle circleArray[3]; // 기본생성자 호출됨
❌ Circle circleArray[3](3); // 이렇게 초기화 불가능

Circle *p = circleArray //일때 첫번째 객체 getArea() 함수 호출
p->getArea();
p[0].getArea();
(*p).getArea();

// 1차원 객체 배열 초기화
Circle circleArray[3] = { Circle(10), Circle(20), Circle() };

// 다차원 객체 배열 선언
Circle circles[2][3] = {{ Circle(1), Circle(2), Circle(3) }, {Circle(4), Circle(5), Circle() }};

// new 초기화
int *p = new int(20);
char *p = new char('a');

// 배열 new, delete
int *p = new int[5];
delete [] p;

// 동적할당 배열 초기화
int *p = new int [] {1, 2, 3, 4}; // 1, 2, 3, 4로 초기화된 배열
❌ int *p = new int[10](20); // 이렇게 초기화 불가능
❌ int *p = new int(10)[20]; // 오류

// 객체 new, delete
Circle *p = new Circle;// new Circle(); 과 동일,기본생성자 호출
Circle *p = new Circle(30);
delete p; // new로 할당받아야만 delete 가능

// 객체 배열 new, delete
Circle *p = new Circle[3]; // 3개의 Circle객체로 구성된 배열
Circle *p = new Circle[3] { Circle(1), Circle(2), Circle(3)};
❌ Circle *p = new Circle[3](30); // 오류
delete [] p;



```
![[Pasted image 20230420224322.png]]
![[Pasted image 20230420224336.png]]