# prepare-interview

## 기술면접 준비

제가 이직을 준비하면서 면접 예상 질문들을 정리하였습니다. 질문들은 구글에 "백엔드 기술면접 깃허브" 라고 검색하시면 많은 정보가 나오는데 그 중에 예상 질문들을 가져와서 "저만의 답변"을 만들었습니다.

이미 많은 정보들이 있고 그것을 참고하면 되는데 굳이 정리하는 이유는 이미 정리된 것들을 봐도 되지만 그 정리된 내용들을 보면 이상하게(?) 암기도 잘 안되고, 어떤 것은 이해가 안되는 것도 있었습니다. (기억도 잘 안나고요.) 하지만 제가 이해한데로 정리, 요약하고 다시보면 이해가 잘 되었습니다. 그래서 질문들을 가지고 저만의 방식으로 다시 정리할 필요성을 느꼈고, 이번에 이직 준비를 하면서 계속 참고하려고 만들게 되었습니다.

<details>
<summary>Managed - Unmanaged 언어의 차이는 무엇이고 어떤 장, 단점이 있나요?</summary>
<div markdown="1">

[분류 기준은 메모리 관리 주체]

코드가 하드웨어에서 바로 구동되는 것이 아닌 특정 런타임 환경에 의해 관리되고 의존하는 코드를 의미

즉, 가상머신 위에서 관리되고 작동되는 Java와 같은 언어로 작성된 코드를 Managed Code라고 한다.

Managed 언어의 장점

- 메모리 관리를 가상머신이 대신 해줌
- 메모리 관리를 자동으로 해주기 때문에 메모리 누수의 문제에서 보다 자유로움
- 코드가 런타임 환경에 의존하므로 하드웨어나 OS에 종속되지 않음

Managed 언어의 단점

- 메모리를 구체적으로 관리할 수 없어 프로그래밍의 자유도가 낮고 비정기적인 메모리 정리가 이루어짐

Unmanaged 언어의 장점

- Managed 언어에 비해 속도가 빠르다.
- 메모리를 구체적으로 관리할 수 있기 때문에 프로그래밍의 자유도가 높다.

Unanaged 언어의 장점

- 사용자가 직접 메모리 관리를 해야하기 때문에 번거롭다
- 관리를 안하면 Memory Leack이 발생할 수 있다. 

</div>
</details>

<details>
<summary>Java 접근 제어자에는 무엇이 있는지 설명해주시고 Protected와 Private는 어느 시점에 어떻게 사용될 수 있는지 이야기 해주세요.</summary>
<div markdown="1">

자바의 접근제어자는 private, public, protected, default 가 있으며, private의 경우 싱글톤 패턴에서 생성자 호출을 막기 위해 private을 사용한다. 다만 상속관계에서만 생성자 호출을 열어두고 싶을 경우에는 protected를 사용한다.

</div>
</details>

<details>
<summary>JVM의 메모리 구조에 대해서 설명해 주세요.</summary>
<div markdown="1">

먼저 JVM이란 자바 가상 머신으로 자바와 OS 사이에서 중개자 역할을 수행하며, 따라서 자바는 OS에 독립적이지만 JVM은 OS에 종속적이다.

먼저 소스코드를 작성하여 자바 컴파일러에 의해 자바 소스파일(.java)은 바이트코드(.class)로 변환된다. 변환된 바이트코드를 클래스로더(Class Loader)가 JVM의 런타임 데이터 영역(Runtime Data Area)에 적재하고, 실행 엔진(Execution Engine)에 의해 실행된다.

- 클래스로드 런타임 데이터 영역에 적재할 때에는 컴파일 타임이 아닌 런타임에 클래스를 처음으로 참조할 때 해당 클래스를 로드하고 링크하는 동적로드의 특징이 있다.
- 런타임 데이터 영역에는 메서드 영역, 힙 영역, 스택 영역, PC 레지스터, 네이티브 메서드 스택이 있다.
  - 메서드 영역 - 모든 스레드가 공유하는 영역으로 JVM이 시작될 때 생성되며 클래스, 인터페이스, 메서드, static 변수 등이 저장된다.
  - 힙 영역 - 인스턴스 또는 객체를 저장하는 공간으로 가비지 컬레션의 대상이 된다.
  - 스택 영역 - 각 스레드마다 하나의 스택이 존재하며 스택 프레임이라는 구조체를 저장한다. 지역변수, 매개변수, 리턴 값 등이 저장된다.
  - PC 레지스터 - 스레드마다 현재 실행할 스택 프레임을 가리키는 주소가 생성된다.
  - 네이티브 메서드 스택 - 자바 외의 언어로 작성된 네이티브 코드를 위한 스택이다.
- 실행 엔진에서 바이트 코드를 해석하는 방식이 2가지가 있다.
  - 인터프리터 - 바이트코드 명령어를 하나식 읽어서 해석하고 실행한다. 기본적으로 이 방식을 사용하며 느리다.
  - JIT 컴파일러: 인터프리터의 단점을 보완하기 위해 나온 것으로, 인터프리터 방식으로 실행하다가 적절한 시점(반복적인 코드)에 바이트코드 전체를 컴파일하여 네이티브 코드로 변경하고 이후에는 이 네이티브 코드로 직접 실행하는 것이다. 네이티브 코드는 캐시에 보관하기 때문에 속도가 빠르다.

</div>
</details>

<details>
<summary>Garbage Collector은 무엇이고 장단점과 동작 방식에 대해서도 간략히 설명해주세요.</summary>
<div markdown="1">

자바의 메모리 관리 방법중 하나로 JVM의 힙 영역에 동적으로 할당됐던 메모리 중 필요없게 된 메모리 객체를 모아서 주기적으로 제거하는 프로세스를 말한다.

이 가비지 컬렉터가 대신 메모리 관리를 해주기 때문에 사용자 입장에서는 Memory Leak 문제에 대해 고민하지 않고 오로지 개발에 집중할 수 있다.

하지만 메모리가 언제해제되는지 정확하게 알 수 없어 제어하기 힘들며, 가비지 컬렉션이 동작하는 동안에는 다른 동작을 멈추기 때문에 오버헤드가 발생되는 문제가 있다. 이를 **Stop-The-World** 라 한다.

가비지 컬렉션 과정은 `Mark and Sweep` 이라고 한다. JVM의 가비지 컬렉터가 스택의 모든 변수를 스캔하면서 각각 어떤 오브젝트를 레퍼런스 하고 있는지 찾는 과정이 Mark다. Reachable 오브젝트가 레퍼런스하고 있는 오브젝트 또한 marking한다. 첫 번째 단계인 marking 작업을 위해 모든 스레드는 중단된다. (Stop-The-World) 그리고 나서 mark 되어있지 않은 모든 오브젝트들을 힙에서 제거하는 과정이 Sweep이다.

</div>
</details>

<details>
<summary>Java 8 버전에 추가된 중요 기능들에 대하여서 설명해주세요.</summary>
<div markdown="1">

- 람다표현식 지원
- 스트림은 자바의 배열, 컬렉션을 편리하게 처리하는 방법을 제공하는 API이다.
- Optional은 자바의 null 처리를 도와주는 API이다.
- 새로운 날짜 API인 LocalDateTime, LocalDate, LocalTime 클래스가 있다.

</div>
</details>

<details>
<summary>Java는 Call By Value일까요, Call By Reference 일까요?</summary>
<div markdown="1">

- Call by value : 메서드 호출시 메서드 파라미터를 복사해서 전달하기 때문에 원본의 데이터가 변경될 가능성이 없다. 다만 파라미터 전달할 때마다 복사하기 때문에 메모리 공간을 더 잡아먹는다.
  - 메서드 파라미터가 `primitive type`이면 변수값 자체를 복사한다.
  - 메서드 파라미터가 `reference type`이면 해당 객체의 주소값을 복사하여 가지고 있다. 즉, 원본 객체의 프로퍼티까지는 접근이 가능하나, 원본 객체 자체를 변경할 수는 없다.
- Call by reference : 함수 호출시 참조(주소) 자체를 전달하기 때문에 데이터값을 변경하면 원본 데이터에도 영향이 간다. 따라서 call by reference는 데이터값을 복사하지 않기 때문에 메모리 공간은 어느정도 해결되었지만 원본 데이터가 변경될 수 있다는 위험이 있다.

자바의 경우, 항상 **call by value**로 넘긴다.

</div>
</details>

## References

- https://github.com/Lob-dev/Junior-Back-end-Developer-Concepts# prepare-interview
