# WriterSide 마크업, MD 중심으로

## xml과 md 혼용 가능

## WriterSide의 MD 문법

### 챕터와 헤더

```
    # : h1 - 각 토픽 문서의 제목입니다. 토픽, 문서당 하나만 지정 가능합니다.
    ## : h2 - 각 토핑의 최상위 챕터 입니다.
    ### : h3
    #### : h4
    ##### : h5
    ###### : h6 - WriterSide 에서 지원하는 가장 낮은 챕터 구성입니다.
```

각 챕터는 `{collapsible="true"}`를 우측에 추가해 접을 수 있습니다.
하지만 해당 설정이 적용된 컨텐츠에 대해서 검색되지 않으므로 사용에 주의가 필요합니다.

### 접기(Collapsible elements)

챕터(Chapters), 절차(Procedures), 코드 블록(Code blocks),
정의 목록(Definition lists)은 설정을 추가해 접을 수 있습니다.
이중 MD으로 적용 가능한 요소는 챕터와 코드 블록입니다.

### 링크

```
    [Link text](target.topic)
    [`Link text`](target.topic)
    [**Link text**](target.topic)
    [](target.topic)

    ## Chapter one

    ## Chapter two {id="second"}

    ## Example links

    Here is [a link to the first chapter](#chapter-one).
    
    Here is [a link to the second chapter](#second).
    
    Here is [a link to another topic](another_topic.md).
    
    Here is [a link to an anchor in another topic](another_topic.md#anchor).
    
    Here is [a link to the JetBrains website](https://www.jetbrains.com/).

```

Press `⌘Сmd` `N` to open the Insert menu, and then select Link.

Alternatively, press
`⇧Shift` `⌘Сmd` `U`
. If you previously copied a URL to the clipboard,
Writerside will insert the URL as the target of the link.

### 이미지

![WriterSideThumbnail.png](WriterSideThumbnail.png)

```
    ![Alt Text](image.png){ width="450" }
    ![Alt Text](image.png){ style="inline" }
    ![Alt Text](image.png){ style="block" }
    ![Alt Text](image.png){ thumbnail="true" width="200" }

```

![Alt Text](WriterSideThumbnail.png){style=""}

|  옵션  | border-effect | thumbnail | style  |
|:----:|:-------------:|:---------:|:------:|
| 상세옵션 |    rounded    |   true    | block  |
|      |     line      |   false   | inline |
|      |     none      |           |  auto  |

Press `⌘Сmd` `N` to open the Insert menu, and then select Link.

Alternatively, press
`⌘Сmd` `U`

```
  Click the ![check icon][check]{width="16"} icon to mark an item as done.

[check]: check-icon.png
```

### 비디오

### 리스트

```
1. First item.
    1. First indented item.
    2. Second indented item.

   {type="alpha-lower"}
2. Second item.
3. Third item
4. Fourth item

{start="2"}

- Some list item
- Another list item
- Yet another list item
    - Some indented item
    - Another indented item
- One more item
```

1. First item.
    1. First indented item.
    2. Second indented item.
       {type="alpha-lower"}
2. Second item.
3. Third item
4. Fourth item
   {start="2"}


- Some list item

* Another list item

- Yet another list item
    + Some indented item

    - Another indented item
- One more item

목록에 대한 지침
엄격한 규칙은 아니지만, 목록을 추가할 때 다음 사항을 명심하는 것이 좋습니다.
목록 앞에 문단을 써서 소개하십시오. 소개가 없는 목록은 불분명할 수 있습니다.
목록에 2~8개 항목을 포함합니다. 항목이 너무 많으면 압도적일 수 있으며 아무것도 강조하지 못할 것입니다.
짧은 항목의 긴 목록이 필요한 경우 여러 열을 사용하는 것을 고려하세요.
각 항목의 크기를 최대한 제한하세요. 목록 항목을 가장 기본적인 아이디어 이상으로 확장하지 마세요.
각 항목에 대해 많은 세부 정보를 제공해야 하는 경우 정의 목록을 사용하거나 콘텐츠를 장 으로 나누는 것을 고려하세요.
목록을 과도하게 사용하지 마십시오.
목록은 문단 사이에 구조를 추가하는 좋은 방법이지만 모든 내용을 목록으로 만드는 것은 필요한 맥락을 제공하지 못합니다.
또한 표와 탭과 같은 다른 요소를 고려하십시오.

#### 여러열

```
- this
- is
- a
- long
- list
- rendered
- in
- multiple
- columns

{columns="3"}
```

- this
- is
- a
- long
- list
- rendered
- in
- multiple
- columns
  {columns="3"}

### 정의 목록

```
First Term
: This is the definition of the first term.

Second Term
: This is the definition of the second term.
```

First Term
: This is the definition of the first term.

Second Term
: This is the definition of the second term.

type attribute
: full wide medium narrow compact
If you want to show titles of definition list items in the topic navigation,

[//]: # (add <show-structure for="def"/> to the topic. For more information, see <show-structure>.)

### 테이블 자세한 설정은 xml

header-row
header-column
both
none

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

#### 코드 블럭

If you need to provide a sample of XML or HTML code,
wrap the contents of the code block with a CDATA section.
This will prevent Writerside from processing tags.
You can also use an intention action for this.

```
<code-block lang="xml">
    <![CDATA[
        <some-tag>text in tag</some-tag>
    ]]>
</code-block>
```

Alternatively, you can escape the < and > characters using &lt; and &gt;.

<code-block lang="xml">
    &lt;some-tag&gt;text in tag&lt;/some-tag&gt;
</code-block>

https://www.jetbrains.com/help/writerside/code.html#reference-code-from-file

### 단축키

<shortcut>Ctrl+C</shortcut>

### Admonitions, 콜아웃

>
>
{style="note"}

>
>
{style="tip"}

>
>
{style="warning"}

>
{title="dadasd"}

### TLDR : too long; didn't read

<tldr>
<p></p>
</tldr>

### 요약

### 첨부파일

https://www.jetbrains.com/help/writerside/downloadable-resources.html?keymap=macOS

### mermaid

https://www.jetbrains.com/help/writerside/mermaid-diagrams.html?keymap=macOS#git_example

### PlantUML diagrams

https://www.jetbrains.com/help/writerside/plantuml-diagrams.html?keymap=macOS

### 수식 표현

<primary-label ref="label"/>
<secondary-label ref="wip"/>
<secondary-label ref="beta"/>

https://www.jetbrains.com/help/writerside/math-support.html?keymap=macOS