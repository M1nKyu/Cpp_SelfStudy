
# 2.
## 1. 만들어진 연대순으로 나열
```
Java, C, C#, C++
```
- 정답:  C > C++ > Java > C++
## 2. C++ 표준이 중요한 이유는?
```
1. 개발속도    2. 호환성   3. 특수성   4. 정확성
```
- 정답 : 2
# 3.
## 1. C언어와 호환성을 유지하기 위해 원칙이 무너지게 된 C++ 언어의 객체 지향 특성은?
```
1. 캡슐화   2. 다형성   3. 상속성   4. 데이터 추상화
```
- 정답 :  1
## 2. C++에서 C언어에 새로 추가한 기능이 아닌 것은?
```
1. 멀티스레딩   2. new연산자   3. 연산자 재정의   4. 참조에 의한 호출
```
- 정답 : 1
# 4.
## 1. 링킹이 필요한 이유가 아닌 것은?
*1.* C++ 코드의 디버깅을 효율적으로 하기 위해서 (X)
2. C++ 프로그램에서 *표준 C++ 라이브러리의 함수를 호출하는 경우, 개발자가 작성한 코드와 표준 라이브러리 코드를 합쳐 실행파일을 만드는 과정*이 필요하기 때문
3. C++ 프로그램을 여러개의 C++ 소스 파일로 나누어 작성할 때, 한 소스파일에서 다른 소스파일의 함수를 호출하면 *두 프로그램을 합치는 과정*이 필요하기 때문
4. C++언어로 작성된 목적파일과 C언어로 작성된 목적 파일을 합쳐 실행 파일을 만드는 과정이 필요하기 때문

## 2. main.cpp, f.cpp. g.cpp로 구성되는 C++ 프로그램 개발 과정에 대해 다음에 답하라
- (1) : main.cpp, f.cpp, g.cpp를 각각 컴파일 하여 생성되는 목적파일은 무엇인가?
	- 답 : main.obj, f.obj, g.obj

- (2) : 목적 파일들을 연결하여 하나의 실행파일을 만드는 과정을 무엇이라고 하는가?
	- 답 : 링킹