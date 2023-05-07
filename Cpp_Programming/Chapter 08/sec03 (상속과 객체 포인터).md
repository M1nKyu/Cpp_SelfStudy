- 파생클래스 객체를 파생 클래스의 포인터나 기본 클래스의 포인터로 가리킬 수 있다
# 업캐스팅
- 업캐스팅(up-casting)이란 파생 클래스의 객체를 기본 클래스의 포인터로 가리키는 것
	- 파생클래스의 객체를 기본 클래스의 객체처럼 다룰 수 있게 함
		- 파생클래스가 기본클래스의 멤버를 포함하기 때문에

- Point 클래스의 포인터로 ColorPoint 객체를 가리키는 업캐스팅 사례
```cpp
int main(){
	ColorPoint cp;
	ColorPoint *pDer = &cp;
	Point* pBase = pDer; // 업캐스팅
	 
	pDer->set(3,4);
	pBase->showPoint();
	pDer->setColor("Red");
	pDer->showColorPoint();
	
	pBase->showColorPoint(); // 컴파일 오류
	                         // pBase 포인터로는 ColorPoint 객체 내의 Point 클래
		                     // 스 멤버만 접근할 수 있다.
}
```
- 업캐스팅한 기본클래스의 포인터로는 기본 클래스의 멤버만 접근할 수 있다

- 다음과 같이 명시적 타입 변환이 필요 없다
```cpp
Point* pBase = (Point*)pDer; // (Point*) 생략 가능
```
---
# 다운캐스팅
- 기본 클래스 포인터가 가리키는 객체를 파생 클래스의 포인터로 가리키는 것
- 업캐스팅과 달리 명시적으로 타입변환을 지정해야 한다
```cpp
int main(){
	ColorPoint cp;
	ColorPoint *pDer;
	Point* pBase = &cp; // 업 캐스팅

	pBase->set(3,4);
	pBase->showPoint();

	pDer = (ColorPoint *)pBase; // 다운 캐스팅, 강제 타입 변환 반드시 필요
	pDer0->setColor("Red");
	pDer->showColorPoint();
}
```

- 명시적으로 타입변환을 지정해야 한다
```cpp
pDer = (ColorPoint*)pBase; // 다운 캐스팅, 강제 타입 변환 필요
```
