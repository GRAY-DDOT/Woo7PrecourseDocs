# JDK 21 업데이트
JDK 21은 자바의 최신 LTS로 성능 최적화, 동시성 간소화, 패턴 매칭의 확장, 문자열 처리 향상 등의 변화가 있습니다.
주요 업데이트 내용은 다음과 같습니다.

## 1. 가비지 컬렉션(Garbage Collection) 개선

ZGC의 성능이 향상되었습니다.
ZGC는 대규모 애플리케이션에서 효율적으로 동작하도록 설계된 가비지 컬렉터이며 일시 중지 시간이 매우 적습니다.

## 2. Virtual Thread 도입

Java 플랫폼에 새로운 유형의 스레드인 **가상 스레드(Virtual Threads)**가 도입되었습니다.
기존의 플랫폼 스레드와 다르게 수십만 개 이상의 스레드를 가볍게 생성할 수 있습니다.
대규모 동시성을 처리하는 애플리케이션에 유리합니다.

## 3. Switch를 위한 Pattern Matching 추가

switch 표현식에서 아래 예시와 같이 패턴 매칭을 사용할 수 있는 기능이 도입되었습니다.
다양한 패턴을 매칭하고 분기 처리를 더욱 간결하게 할 수 있습니다.
   ```Java
   static void testPatternSwitch(Object obj) {
       switch (obj) {
           case Integer i -> System.out.println("Integer: " + i);
           case String s -> System.out.println("String: " + s);
           default -> System.out.println("Unknown type");
       }
   }
   
   ```

## 4. Record Pattern

레코드 객체를 패턴 매칭할 수 있는 기능이 도입되었습니다.
이를 통해 레코드의 필드를 쉽게 추출하고 분기 처리를 할 수 있습니다.
레코드 패턴은 instanceof 검사와 값을 추출하는 과정을 한 번에 처리할 수 있습니다.
레코드 객체는 Java 16에서 정식으로 추가된 불변 데이터 객체로 데이터를 간결하고 명확하게 표현하기 위한 용도로 사용합니다.

레코드는 데이터를 저장하기 위한 클래스에서 요구되는 생성자, 접근자(getter), equals(), hashCode(), toString() 등의 메서드를
자동으로 생성해 줍니다.

```Java
record Point(int x, int y) {}

static void printPoint(Object obj) {
   if (obj instanceof Point(int x, int y)) {
   System.out.println("Point at (" + x + ", " + y + ")");
   }
}
```
## 5. 문자열 템플릿(Preview)

문자열 템플릿 기능이 프리뷰로 추가되었습니다.
문자열 내에서 변수를 쉽게 삽입할 수 있으며, 기존의 문자열 연결보다 더 안전하고 효율적인 방식으로 문자열을 처리할 수 있습니다.
문자열 템플릿은 f 접두어로 템플릿 리터럴을 만들며, ${} 구문을 통해 변수를 삽입할 수 있습니다.
조건에 따라 문자열을 더 쉽게 조작할 수 있겠네요.
```Java
String name = "DDOTZY";
String message = STR."Hello, ${name}!";

```

## 6. Sequenced Collections

컬렉션 내 요소의 삽입 순서를 보장하고, 양방향 순회가 가능해졌습니다.
List, Set, Map 인터페이스에 새로운 메서드가 추가되어 요소를 처음 또는 마지막에 추가하거나 제거할 수 있습니다.
```Java
SequencedCollection<String> sequencedList = new LinkedList<>();
sequencedList.addFirst("first");
sequencedList.addLast("last");

```

## 7. 외부 함수 및 메모리 API

외부 함수 및 메모리 API는 자바 프로그램에서 안전하게 외부(네이티브) 메모리를 다루고,
네이티브 코드를 호출할 수 있는 기능을 제공합니다.
C 언어 등의 네이티브 라이브러리와 상호작용 시 유용하게 사용할 수 있습니다..
이전 버전에서 미리보기로 제공되었고 JDK 21부터는 표준 기능으로 제공됩니다.

이밖에 더 많은 업데이트들이 있지만 우선 여기까지 정리하도록 하겠습니다.