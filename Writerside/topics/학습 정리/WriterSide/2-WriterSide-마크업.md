# WriterSide 마크업, MD 중심으로

> 일부 기능은 XML로만 가는한 것들이 있습니다.
> MD 위주로 작성하여 해당 요소는 제외했습니다.
> [공식문서](https://www.jetbrains.com/help/writerside/semantic-markup-reference.html)를 확인해주세요!
> 아참!
> MD 요소에 대해 속성을 정의한 경우는 서식 재정렬 후 들여쓰기 수준을 점검해주세요!!
> 한 칸 더 들어가는 버그가 있어요!

## XML과 MD 혼용 가능

WriterSide에서는 XML과 MD(Markdown)를 함께 사용하여 문서를 작성할 수 있습니다.
기본적으로 문서는 .xml 또는 .md를 골라 생성해야합니다.
하지만 MD 문서에서 XML 문법을 사용할 수 있습니다.
각 형식의 장점을 살려, 보다 유연하게 문서를 구성할 수 있습니다.
XML을 통해 구조적인 데이터 관리를 하고, MD는 간단한 텍스트 작성에 용이합니다.
다만 요소의 정렬이나 배치관련 옵션은 아직 없는 것 같아요.
따라서 저는 좌우 정렬할 요소는 테이블(표)를 이용해 구성했습니다.

## WriterSide의 MD 문법

### 챕터와 헤더

```
    # : h1 - 각 토픽 문서의 제목입니다. 토픽, (중요!)문서당 하나만 지정 가능합니다.
    ## : h2 - 각 토핑의 최상위 챕터 입니다.
    ### : h3
    #### : h4 
    ##### : h5
    ###### : h6 - WriterSide 에서 지원하는 가장 낮은 챕터 구성입니다.
```

각 챕터의 오른쪽에 `{collapsible="true"}`를 우측에 추가해 접을 수 있습니다.
하지만 해당 설정이 적용된 컨텐츠에 대해서 검색되지 않으므로 사용에 주의가 필요합니다.

```markdown
    ### 챕터 이름 {collapsible="true"}
    // 접을 수 있습니다.
```

### 접기(Collapsible elements)

챕터(Chapters), 절차(Procedures), 코드 블록(Code blocks),
정의 목록(Definition lists)은 설정을 추가해 접을 수 있습니다.
이중 MD으로 적용 가능한 요소는 챕터와 코드 블록입니다.

### 링크

링크는 다음과 같이 작성할 수 있습니다.
링크는 문서 내부, 외부 URL 모두에 동일하게 사용가능합니다.
링크 이름에는 아래와 같이 강조를 위한 표현을 사용할 수 있습니다.
이름과 링크가 똑같다면 이름을 비우도록 권장됩니다.
또한 특정 챕터로 이동하도록 작성할 수 있습니다.
토픽으로 등록된 MD 문서를 링크하는 경우 `.md`이 붙습니다.
다만 토픽으로 등록된 것이 확실한 경우`.md`를 붙이지 않고 토픽 자체를 링크할 수 있습니다.

```
    [Link text](target.topic.md)
    [`Link text`](target.topic)
    [**Link text**](target.topic)
    [](target.topic)
    [모듈 내부의 상대 주소도 사용 가능합니다](pkg.target)

    ## 첫 챕터
    ## 챕터 2 {id="second"}
    이것은 [첫 챕터로 이동하는 링크](#첫-챕터)
    이건은 [id로 챕터를 지정한 링크](#second)
    이것은 [다른 토픽으로의 링크](다른-토픽-이름.md)
    이것은 [다른 토픽의 "이런" 챕터로의 링크](다른-토픽-이름.md#이런)
    
    URL [JetBrains website](https://www.jetbrains.com/)

```

링크를 클립보드로 복사한 후 단축키로 쉽게 링크를 삽입할 수 있습니다.
<p> macOS <shortcut>⇧Shift⌘Сmd+U</shortcut>, 삽입 옵션 전체는  <shortcut>⌘Сmd+N</shortcut> </p>
<p> Windows <shortcut>Ctrl+Shift+U</shortcut>, 삽입 옵션 전체는 <shortcut>Alt+Insert</shortcut> </p>

### 이미지

다음과 같은 방식으로 이미지를 삽입하고 효과를 적용할 수 있습니다.
MD 로는 효과가 한정되어있습니다. 파일 지정 방식은 링크 삽입 방식과 동일합니다.

```
    ![Alt Text](image.png){ width="450" }
    ![Alt Text](image.png){ style="inline" }
    ![Alt Text](image.png){ style="block" }
    ![Alt Text](image.png){ thumbnail="true" width="200" }

```

아래의 테이블은 이미지에 적용할 수 있는 효과입니다.

|  옵션  | border-effect | thumbnail | style  |
|:----:|:-------------:|:---------:|:------:|
| 상세옵션 |    rounded    |   true    | block  |
|      |     line      |   false   | inline |
|      |     none      |           |  auto  |

WriterSide 에서는 아직 자체적인 이미지 정렬 기능을 제공하지 않습니다.
대체적으로 테이블 내부에 삽입하는 방법을 사용할 수 있습니다.
이때 이미지 삽입 표현은 XML으로 전환해야합니다.

### 비디오

비디오를 첨부할 수 있습니다.
MD 표현은 지원하지 않지만 MD 문서에서 해당 XML 문법을 사용할 수 있습니다.
로컬 파일은 미리보기 이미지를 별도로 설정해야합니다.

```xml

<video src="sample.mp4" preview-src="preview-image.png"/>
<video src="https://youtu.be/BeJu9bMPLGU"/>
```

### 리스트

리스트 요소는 순서가 있는 리스트와 순서가 없는 리스트가 있습니다.

순서가 있는 리스트의 경우 다음과 같이 속성을 적용할 수 있습니다.

```
1. 처음
    1. 처음의 하나
    2. 처음의 둘
                        // 알파벳 리스트로 바꿉니다.(기본값 1)
   {type="alpha-lower"} // 대상과 같은 수준의 들여쓰기가 필요합니다.
                        // 대상 사이에 빈 줄이 있어야 합니다.
2. Second item.
3. Third item
4. Fourth item
            // 대상 리스트의 시작 번호를 바꿀수 있습니다.(기본값="1")
{start="2"} // 대상과 같은 수준의 들여쓰기가 필요합니다.
            // 대상 사이에 빈 줄이 있어야 합니다.
            // 1 이상만 지정 가능합니다.
```

1. 처음
    1. 처음의 하나
    2. 처음의 둘

   {type="alpha-lower"}
2. Second item.
3. Third item
4. Fourth item

{start="2"}


```markdown
- 리스트는
- 이렇게
    - 작성할 수
    - 있지만
- 2~8개 정도만 포함하라고 추천합니다.
+ -, +, * 3개 입니다.
* 결과는 하나입니다.
```
- 리스트는
- 이렇게
    - 작성할 수
    - 있지만
- 2~8개 정도만 포함하라고 추천합니다.
+ 사용가능한 기호는 -, +, * 3개 입니다.
* -, +, * 3개 입니다.
* 결과는 하나입니다.


### 여러 열의 리스트
만약 리스트가 너무 길다면 열을 분할할 수 있습니다.
```
-- 너무
- 긴
- 리스트는
- 가독성이
- 떨어집니다
- 다중 열 리스트를
- 사용해보세요
- 다른 서비스에도
- 비슷한 것들이 있죠?

{columns="3"}

- 1)순서가 있는 경우는    //1) 뒤에 띄어쓰기 하면 안돼요!!
- 2)이렇게             //순서가 있는 리스트로 인식됩니다.
- 3)해보세요
- 4)몇 개까지
- 5)될까요?
- 5개 부터는 문제가 생기네요
- 4개까지만 지정해보세요

{columns="5"}
```

- 너무
- 긴
- 리스트는
- 가독성이
- 떨어집니다
- 다중 열 리스트를
- 사용해보세요
- 다른 서비스에도
- 비슷한 것들이 있죠?

{columns="3"}

- 1)순서가 있는 경우는
- 2)이렇게
- 3)해보세요
- 4)몇 개까지
- 5)될까요?
- 5개 부터는 문제가 생기네요
- 4개까지만 지정해보세요

{columns="5"}



### 정의 목록
정의 목록은 특별한 형태의 리스트입니다. 용어의 정의를 표현할 수 있어요.
아래와 같이 다양한 스타일을 적용할 수 있습니다.
자세한 속성은 공식 문서를 참고해주세요!
[공식 문서](https://www.jetbrains.com/help/writerside/lists.html#definition_lists)

```markdown
정의 목록
: 정의 목록은 용어의 정의를 표현할 수 있는 목록이에요
```

정의 목록
: 정의 목록은 용어의 정의를 표현할 수 있는 목록이에요


### 테이블, 그런데 속성을 곁드린..
```markdown

|   |   |   |
|---|---|---|
|   |   |   |
|   |   |   |
{style="header-row"}    // 기본 설정이에요

|   |   |   |   |
|---|---|---|---|
|   |   |   |   |

{style="header-column"}


|   |   |   |
|---|---|---|
|   |   |   |
|   |   |   |

{style="both"}


|   |   |   |
|---|---|---|
|   |   |   |
|   |   |   |

{style="none"}

```

|   |   |   |
|---|---|---|
|   |   |   |
|   |   |   |
{style="header-row"}

|   |   |   |   |
|---|---|---|---|
|   |   |   |   |

{style="header-column"}


|   |   |   |
|---|---|---|
|   |   |   |
|   |   |   |

{style="both"}


|   |   |   |
|---|---|---|
|   |   |   |
|   |   |   |

{style="none"}

XML 로는 더 많은 조작을 할 수 있습니다.
링크를 확인해주세요!
[공식 문서](https://www.jetbrains.com/help/writerside/tables.html)
 

### 탭

    ---
    switcher-label: Language
    ---
    
    #### Topic title
    
    ...
    
    ##### Section One {switcher-key="Java"}
    
    Some Java examples.
    
    ##### Section Two {switcher-key="Kotlin"}
    
    Some Kotlin examples.
    ...
    
    <tabs>
    <tab title="First tab">
    First tab content
    </tab>
    <tab title="Second tab">
    Second tab content
    </tab>
    </tabs>
    
    If you want to show tab titles in the topic navigation,
    add <show-structure for="tab"/> to the topic.
    For more information, see <show-structure>.

### 코드

#### 인라인 코드
```text
인라인 코드는 `이렇게` 문장 안에 코드를 넣은 거에요!
`java.lang.String`은 문자열 클래스입니다.
```
인라인 코드는 `이렇게` 문장 안에 코드를 넣은 거에요!
`java.lang.String`은 문자열 클래스입니다.

#### 코드 블럭
코드 블럭은 백틱 (`) 3개로 묶어요
```text
    ```여기에 사용하는 언어를 적으면 아래 코드에 효과가 적용됩니다!
    여기가 본문이에요
    ```
    
    ```Java
    public class ThisIsExampm {
        thisIsExampleMethod();
        int thisis;
    }
```
```

```여기에 사용하는 언어를 적으면 아래 코드에 효과가 적용됩니다!
    여기가 본문이에요
```

```Java
    public class ThisIsExampm {
        thisIsExampleMethod();
        int thisis;
    }
```

> 코드블럭도 접어둘 수 있어요!
> `{collapsible="true" default-state="collapsed"}`
> 위 속성을 한줄 띄고 적용해보세요!

아직도 코드 블럭에 관련된 설정이 많아요..
나머지는 [공식 문서](https://www.jetbrains.com/help/writerside/code.html)를 참고하세요!

### 콜아웃? 강조? 인용? Admonitions

제품마다 부르는 말이 많은데요 WriterSide 에서는 Admonitions 이라 해요.
```markdown

> 이건 팁입니다
{style="tip"} // 기본 설정이에요!


> 이건 노트에요
{style="note"}

> 이건 경고에요!
{style="warning"}
```

> 이건 팁 입니다
{style="tip"}

> 이건 노트에요
{style="note"}

> 이건 경고에요!
{style="warning"}



### 그 밖의 많은 것들은...

너무 많은 내용을 정리하고 있다는 생각이 들었습니다.
그 밖에 것들은 간단히 이름과 링크만 남겨 둘게요!!

- [Tabs](https://www.jetbrains.com/help/writerside/tabs.html)
- [TLDR](https://www.jetbrains.com/help/writerside/tl-dr-blocks.html) : too long; didn't read
- [요약](https://www.jetbrains.com/help/writerside/summary-elements.html)
- [첨부파일](https://www.jetbrains.com/help/writerside/downloadable-resources.html)
- [mermaid](https://www.jetbrains.com/help/writerside/mermaid-diagrams.html)
- [수식 표현](https://www.jetbrains.com/help/writerside/math-support.html)
