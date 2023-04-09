# 1.
## 1. public 멤버함수 draw()를 가진 Polygon 클래스가 있을때, 다음 두 선언문에 대해서 물음에 답하여라
```cpp
Polygon poly;
Polygon *p;
```
### (1) 
- 포인터 p를 활용하여 poly객체의 draw() 함수를 호출하는 코드를 두줄로 작성
```cpp
p = &poly;
p->draw();
```
### (2) 
- 다른 하나는 ?
```cpp
(1)poly.draw();
(2)p = &poly; p->draw();
(3)p = &poly; (*p).draw();
(4)poly->draw();
```
- 답 : 4, poly는 포인터가 아니기때문에, `->`연산자를 사용할 수 없다
---
# 2.
## 1. 다음 클래스에 대해 물음에 답하라
```cpp
class Sample{
	int a;
public:
	Sample() { a = 100; cout << a << ' ' ; }
	Sample(int x) { a = x; cout << a << ' '; }
	Sample(int x, int y) { a = x*y; cout << a << ' ';}
	int get() { return a;}
};
```
### (1) 
- `Sample arr[3];` 이 실행될 때 출력 결과는?
	- 100 100 100
### (2) 
- `Sample arr2D[2][2] = { {Sample(2,3), Sample(2,4)}, {Sample(5),Sample()} };`이 실행될 때 출력되는 결과는?
  - 6 8 5 100 
### (3)
- 객체 포인터를 이용하여 (1)에서 선언된 arr의 모든 원소(a)의 합을 출력하는 for문을 작성해라
```cpp
Circle *p = &arr;
int sum = 0;
for(int i = 0; i < 3; i++){
	sum += p->get();
	p++;
}
cout << sum;
```
### (4)
- (2)에서 선언된 arr2D배열 이름을 이용하여 모든 원소 (a)의 합을 출력하는 for문을 작성해라
```cpp
int sum = 0;
for(int i = 0; i < 2; i++)
	for(int j = 0; j < 2; j++){
		sum += arr2D[i][j].get();
	}
cout << sum;
```
---
# 3.
## 1. 다음 물음에 대한 간단한 코드 보여라
### (1) 1개의 double 공간을 동적 할당받고 3.14를 기록
```cpp
// 1.
double *p = new double;
*p = 3.14;

// 2.
double *p = new double(3.14);
```
### (2) 배열을 동적 할당받아 5개의 정수를 입력받고, 제일 큰 수를 출력하고 배열 반환
```cpp
#include <iostream>
using namespace std;

int main()
{
	int* p = new int[5];

	for (int i = 0; i < 5; i++)
		cin >> p[i];

	int max = p[0];

	for (int i = 1; i < 5; i++)
	{
		if (p[i] > max)
			max = p[i];
	}
	cout << max;
	delete [] p;
}
```

## 2. 틀린 라인을 골라 수정
### (1)
```cpp
int *p = new int(3);
int n = *p;
delete [] p; // delete p; 로 수정
```
### 👍(2) 
```cpp
char *p = new char [10];
char *q = p; 
q[0] = 'a';
delete [] q;
delete [] p; // 이 줄 삭제, 이미 q 포인터를 통해 메모리르 반환함
```