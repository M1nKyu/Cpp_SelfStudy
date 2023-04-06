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