# 1주차_SD_문자열 덧셈 계산기

[원본](1주차-문자열-덧셈-계산기.md), [LD](), [SN]()

## 학습 목표

* Git, GitHub, IDE 등 실제 개발을 위한 환경에 익숙해진다.
* 교육 분야에 맞는 프로그래밍 언어를 사용하여 간단한 문제를 해결한다.

---

## 프리코스 진행 방식

### 진행 방식

* 미션 구성
  * **과제 진행 요구 사항**
  * **기능 요구 사항**
  * **프로그래밍 요구 사항**
* 위 요구 사항을 모두 만족하기 위해 노력할 것
* 특히 기능 구현 전 기능 목록을 만들고, 기능 단위로 커밋 하여 진행할 것
* **기능 요구 사항에 미개재 사항은 스스로 판단하여 구현**
* 매주 미션은 화요일 오후 3시부터 확인 가능, 차주 월요일까지 구현 완료 및 제출해야함
  * **제출은 일요일 오후 3시부터 가능.**
  * **시간 미준수시 미션 미제출로 간주.**
  * 종료 일시 이후 추가 푸시 미허용

### 미션 제출 방법

* 미션 구현 완료 후 GitHub 통해 제출
    * 제출 방법: [프리코스 과제 제출](https://github.com/woowacourse/woowacourse-docs/tree/master/precourse)
* 최종 제출 : GitHub 미션 제출, [우아한테크코스 지원 플랫폼](https://apply.techcourse.co.kr/)에 PR 링크 포함 제출
    * 자세한 안내는 [제출 가이드](https://github.com/woowacourse/woowacourse-docs/tree/master/precourse#%EC%A0%9C%EC%B6%9C-%EA%B0%80%EC%9D%B4%EB%93%9C)를 참고한다.
    * 과제 수행 중 느낀 점, 배운 점, 많은 시간을 투자한 부분 등 자유롭게 작성

### 과제 제출 전 체크 리스트

* **요구 사항 명시된 `출력 형식` 미준수 시 0점**
  * 기능 구현이 올바르거나 완벽해도
* 기능 구현 완료 후 모든 테스트에 대한 성공 여부 확인
  * **테스트 실패 => 0점**

#### 테스트 실행 가이드

* Java 버전 21 확인(`java -version`)
* 테스트 방법
  * Mac, Linux : `./gradlew clean test`
  * Windows : `gradlew.bat clean test` 또는 `./gradlew.bat clean test` 
* 명령 실행 시 모든 테스트가 아래와 같이 통과하는지 확인
    ```apache
    BUILD SUCCESSFUL in 0s
    ```

---

## 문자열 덧셈 계산기

### 과제 진행 요구 사항

* 미션 시작 : 미션 저장소 포크 및 클론
  * [문자열 덧셈 계산기](https://github.com/woowacourse-precourse/java-calculator-7) 
* 구현 기능 목록 정리
  * 시점 : **기능 구현 전
  * 위치: `README.md`
* Git 커밋 단위: 상기의 기능 목록 단위 추가
    * [AngularJS Git Commit Message Conventions](https://gist.github.com/stephenparish/9941e89d80e2bc58a153)을 참고해 커밋 메시지를 작성한다.
* 자세한 방법은 프리코스 진행 가이드 문서를 참고

### 기능 요구 사항
목표: 입력한 문자열에서 숫자를 추출하여 더하는 계산기를 구현한다.
* "쉼표(,) or 콜론(:)"을 `구분자`로 가지는 `문자열`을 `전달`하는 경우 `구분자를 기준으로 분리한` 각 `숫자의 합`을 `반환`한다.
    * 예: "" => 0, "1,2" => 3, "1,2,3" => 6, "1,2:3" => 6
* `커스텀 구분자` 지정 가능(상기 기본 구분자 외)
  * 문자열 앞 "//" "\\n" 사이에 위치하는 문자
  * 예: "//;\\n1;2;3" => ; , 6 반환
* `사용자 입력 오류`(잘못된 입력)
  * `IllegalArgumentException` 발생, 애플리케이션 종료

#### 입출력 요구 사항

##### 입력
* 구분자와 양수로 구성된 문자열

##### 출력
* 덧셈 결과
    ```ada
    결과 : 6
    ```
##### 실행 결과 예시
```ada
덧셈할 문자열을 입력해 주세요.
1,2:3
결과 : 6
```

### 프로그래밍 요구 사항

* JDK 버전: 21
* 엔트리 포인트: `Application`의 `main()`
* `build.gradle` 변경 금지
  * **제공된 라이브러리 외 외부 라이브러리 사용 금지**
* 프로그램 종료 시 `System.exit()`를 호출 금지
* 파일, 패키지 등의 이름 변경, 이동 금지
  * 프로그래밍 요구 사항에 명시된 사항만 가능
* 자바 코드 컨벤션 준수
    * [Java Style Guide](https://github.com/woowacourse/woowacourse-docs/blob/main/styleguide/java)

### 라이브러리
* `Console` API 사용해 구현
  * `camp.nextstep.edu.missionutils`에서 제공
  * 사용자 입력:  `camp.nextstep.edu.missionutils.Console`의 `readLine()`
