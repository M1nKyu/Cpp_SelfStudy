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

