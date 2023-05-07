- 상속이 없다면 객체 지향 언어라고 말하지 않는다
# C++ 클래스의  상속
- 두 클래스 사이에 부모-자식 상속 관계를 선언한다
	- **기본 클래스**(base class) : 부모 클래스
	- **파생 클래스**(derived class) : 자식 클래스

- 상속은 코드의 중복작성을 없앤다
- C++ 에서는 **다중 상속(multiplt inheritance)을 허용**

```cpp
class Phone{
	void call();
	void receive();
};

// Phone 클래스 상속
class MobilePhone : public Phone{
	void connectWireless();
	void recharge();
};

// MobilePhone 클래스 상속
// 총 6개의 기능을 가진 클래스가 된다
class MusicPhone : public MobilePhone{
	void downloadMusic();
	void play();
};
```
---
# 상속의 목적과 장점
## 1. 간결한 클래스 작성
- 동일한 코드가 여러 클래스에 중복되면 클래스의 유지보수에 번거로운 일이 발생
	- 상속을 이용하여 해결
## 2. 클래스 간의 계층적 분류 및 관리의 용이함
- 상속은 클래스를 계층 관계로 표현함으로 표현함으로써, 
	- 프로그램에 존재하는 클래스들의 구조적인 관계 파악을 쉽게 해줌
## 3. 클래스 재사용과 확장을 통한 소프트웨어의 생산성 향상
- 가장 큰 장점, 소프트웨어의 생산성을 향상
- 업그레이드 주기가 빨라지고 있는 추세, 새로운 소프트웨어를 밑바닥부터 작성해서는 싲아에서 살아남을 수 없음