# 동적 클래스 로딩

Java의 동적 클래스 로딩이란, **JVM에서 실행에 필요한 모든 클래스 파일을 메모리에 올려놓지 않고, 필요한 시점에 동적으로 메모리에 올리는 기술을 말한다.**

따라서 가능한 적은 클래스 파일을 메모리에 올려 실행할 수 있으므로 조금 더 효율적이라고 할 수 있다.

# JVM 메모리 구조

![[https://velog.io/@hubcreator/JVM-클래스-동적-로딩](https://velog.io/@hubcreator/JVM-%ED%81%B4%EB%9E%98%EC%8A%A4-%EB%8F%99%EC%A0%81-%EB%A1%9C%EB%94%A9)](attachment:b82159d1-3807-455a-b8a2-8db527e16fdd:image.png)

[https://velog.io/@hubcreator/JVM-클래스-동적-로딩](https://velog.io/@hubcreator/JVM-%ED%81%B4%EB%9E%98%EC%8A%A4-%EB%8F%99%EC%A0%81-%EB%A1%9C%EB%94%A9)

## 인터프리터

컴파일러가 자바 소스코드를 컴파일하면 클래스 파일(바이너리 파일)이 만들어진다.

이 파일은 JVM이 읽을 수 없기 때문에, JVM에서는 이를 읽을 수 있도록 인터프리터를 통해 다시 한 번 JVM이 이해할 수 있는 형태인 기계어로 해석해 실행한다.

인터프리터는 클래스 파일에 있는 바이트 코드를 한 줄 씩 실행한다는 특징이 있다.

Java는 어떤 운영체제든 한 번 컴파일하면 각 OS에 존재하는JVM에서 바로 읽을 수 있다는 특징이 있는데, 그 이유는 **컴파일한 클래스 파일을 OS에 종속적인 JVM이 다시 한 번 실행시에 인터프리터를 통해 자신이 이해할 수 있는 기계어로 번역하기 때문이다.**

## 클래스 로더

클래스 로더란 컴파일된 클래스 파일을 JVM의 메모리 영역 중 Runtime Data Areas에 필요한 파일을 올려주는 역할을 담당한다.

JVM은 모든 클래스 파일을 메모리에 올려놓지 않기 때문에 필요한 클래스 파일을 로드하기 위해서는 클래스 로더를 통해 클래스 파일을 찾아 메서드 영역에 올려야한다.

## 인터프리터와 클래스 로더, 클래스 동적 로딩의 관계

```java
class MyClass {
	// Main 클래스와 다른 파일에 있다고 가정		
}

class Main {
	public static void main(String[] args) { // (1)
		MyClass myclass = null; // (2)
		myclass = new MyClass(); // (3)
	}
}
```

1. 인터프리터가 코드를 한 줄 씩 실행하다, 메모리에 없는 클래스를 읽어야 할 때면 클래스 로더에게 해당 클래스를 메모리에 올려줄 것을 요청한다.
2. 클래스 로더는 자신의 클래스 패스를 찾아 클래스를 메서드 영역에 올린다.

# 참고 자료

- [https://velog.io/@hubcreator/JVM-클래스-동적-로딩](https://velog.io/@hubcreator/JVM-%ED%81%B4%EB%9E%98%EC%8A%A4-%EB%8F%99%EC%A0%81-%EB%A1%9C%EB%94%A9)