# WriterSide 구성

## 1. 구성 소개

WriterSide의 **가장 큰 구성은 프로젝트**입니다.
그리고 내부의 컨탠츠를 바라보는 두 가지 관점이 있습니다.
바로 **모듈**(Module)과 **인스턴스**(Instance)이죠.
모듈은 프로젝트 패키지 관점으로 구분되며 인스턴스는 배포 단위로 구분될 수 있어요.
모듈은 논리적 구조로 프로젝트를 편의에 따라 여러 패키지로 구성 가능하게 하는 목적이 강한 반면,
인스턴스는 배포의 관점에서 별도로 배포할 컨텐츠를 관리할 수 있어요.

### 1.1 모듈 : 논리적 단위

모듈은 프로젝트 내에서 논리적으로 구분되는 단위로, 각 모듈은 고유한 `.cfg` 파일을 가지고 있어 별도 모듈로 생성할 수 있습니다.
이러한 모듈 구성은 독립적인 프로젝트에 대한 작업 등 별도의 패키지로 프로젝트를 나누고 관리하는데 사용됩니다.

<table>
<tr>
<td><img src="WriterSideModule.png" alt="WriterSideModule.png" style="block" border-effect="rounded" width="500" /></td>
<td><img src="WriterSideModuleCfg.png" alt="WriterSideModuleCfg.png" style="block" border-effect="rounded" width="350" /></td>
</tr>
<tr>
<td>선택된 영역이 모듈입니다. 패키지 아이콘 모양이 다릅니다.</td>
<td>모듈은 내부에 동일한 이름의 `.cfg`를 필요로 합니다.</td>
</tr>
</table>

### 1.2 인스턴스 : 배포 단위

인스턴스의 모습


인스턴스는 프로젝트 내부에서 트리(tree) 구조의 토픽(문서) 집합입니다.
실제 파일 시스템 상으로 해당 인스턴스의 .tree 파일이 해당 인스턴스를 구현한다 보시면 됩니다.
인스턴스는 그 이름와 id 속성을 갖는데 {인스턴스 id}.tree 파일이 해당 인스턴스를 관리하는 파일 입니다.
실제 파일의 구조는 다음과 같습니다.
```html
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE instance-profile
        SYSTEM "https://resources.jetbrains.com/writerside/1.0/product-profile.dtd">

<instance-profile id="ddotdocs"
                  name="DDOTWoowaPreDocs"
                  start-page="또찌의-프리코스-도서관.md">

    <toc-element topic="또찌의-프리코스-도서관.md">
        <toc-element topic="문서-관리-규칙.md"/>
    </toc-element>
    <toc-element topic="1주차-문자열-덧셈-계산기.md">
        <toc-element topic="1주차-미션-요약.md"/>
        <toc-element topic="1주차-요구사항-분석.md"/>
        <toc-element topic="1주차-주간-학습-정리.md"/>
    </toc-element>
    <toc-element topic="학습-노트-보관소.md">
        <toc-element topic="Java.md">
            <toc-element topic="JDK21-업데이트.md"/>
            <toc-element topic="Java-예외-처리.md"/>
            <toc-element topic="Java-String-클래스와-메서드.md"/>
        </toc-element>
        <toc-element topic="Git-VCS-Github.md"/>
        <toc-element topic="TDD와-테스트.md">
            <toc-element topic="TDD와-객체-지향-설계.md"/>
            <toc-element topic="Junit5와-Assertions.md"/>
        </toc-element>
        <toc-element topic="WriterSide로-개발-문서-배포하기.md">
            <toc-element topic="1-WriterSide-구성.md"/>
            <toc-element topic="2-WriterSide-마크업.md"/>
            <toc-element topic="WiterSide-배포하기.md"/>
        </toc-element>
    </toc-element>
</instance-profile>
```
{collapsible="true" default-state="collapsed" }

인스턴스를 대상으로 빌드 시 HTML로 변환된 웹 호스팅을 위한 zip파일, PDF, Docker 이미지 등으로 빌드 가능
결과적으로 인스턴스는 하나의 배포단위로 묶는 것이라 할 수 있습니다.

인스턴스의 생성은 다음과 같은 과정으로 이루어 집니다
<table>
<tr>
<td><img alt="WriterSide-add-instance.png" src="WriterSide-add-instance.png" border-effect="rounded" width="550"/></td>
<td><img alt="WriterSide-Render.png" src="WriterSide-Render.png" border-effect="rounded" width="350" /></td>
</tr>
</table>

### 1.3 토픽

WriterSide의 **토픽**은 인스턴스에서 하나의 문서(md, xml) 파일을 나타냅니다.
각각의 토픽은 트리 구조를 통해 부모와 자식 관계를 형성할 수 있습니다.
새로 생성한 모든 토픽은 해당 인스턴스가 정의된 모듈에 생성됩니다.
필요에 따라 패키지를 만들어 리팩토링할 수 있습니다.
이를 통해 문서 간의 계층 구조를 명확히 하고, 관련된 문서를 함께 관리할 수 있습니다.
토픽당 문서 하나 씩, 부모 토픽 자식 토픽 전부 문서 파일 하나에 해당합니다.


#### 1.3.1 TOC(Table of Contents)

![WriterSideTopic.png](WriterSideTopic.png){style="block" border-effect="rounded"}
TOC는 **Table of Contents**를 의미하지만,
WriterSide에서는 토픽의 배치 구조를 나타낸다고 생각하면 쉽습니다.
TOC는 전체 문서의 흐름과 구조를 이해하는 데 도움을 줍니다.
이를 통해 사용자는 문서 간의 관계를 쉽게 파악할 수 있습니다.

해당 TOC는 배포된 사이트에서도 좌측에 표시됩니다.
![WritersideTopicWhenDeploied.png](WritersideTopicWhenDeploied.png){style="block" border-effect="rounded"}

TOC 는 또한 인스턴스 내부의 .tree 파일과 연관이 있습니다.
인스턴스의 직관적인 구조는 TOC 를 통해 확인할 수 있습니다.
해당 구조가 실제 작성되고 관리되는 위치는 각 인스턴스의 .tree 파일 입니다.
TOC에서 문서의 구조를 변경하거나 추가 및 삭제를 하면 IDE가 자동으로 리팩토링을 지원합니다.

일반적인 사이트의 사이트 맵이라고 생각하면 편합니다.
다양한 공식문서에도 비슷한 구조가 있죠?

#### 1.3.2 Structure
![WriterSide-Structure.png](WriterSide-Structure.png){style="block" border-effect="rounded"}
TOC가 토픽 간 구성을 나타낸다면 Structure 는 토픽 내부인 md 파일 자체의 구조를 나타냅니다.
즉, 각 문서 내의 섹션과 하위 섹션의 구성을 정의하는 역할을 합니다.
각 페이지의 차례라고 생각 할 수 있습니다.
차례를 작성할 필요가 없습니다.
배포시에는 Structure 를 통해 해당 챕터로 이동할 수 있습니다.

제가 배포 중인 이 저장소는 설정 오류가 있는지 이동하는 기능은 작동하지 않네요..
아마 각 챕터별 id가 명확하게 지정되지 않아서 그런 것 같습니다.

### 1.4 문서 파일, 토픽, 인스턴스의 관계

문서는 xml과 md 두가지 형태로 작성 가능 합니다.
해당 문서는 실제로는 기본 모둘인 ~/Writerside/ 패키지에 저장됩니다.

그렇다면 문서-토픽-인스턴스는 어떤 관계로 이루어 질까요?
각 문서는 특정 토픽과 연결되고, 이러한 토픽들이 모여 하나의 인스턴스를 구성합니다.
이때 문서는 .tree 를 통해 인스턴스를 정의합니다.
토픽의 이름은 각 문서에 단 하나 뿐인 `#(h1)` 태그로 지정됩니다.
h1 태그가 둘 이상이면 빌드 시 오류가 발생합니다.

![WriterSide-h1-only-one.png](WriterSide-h1-only-one.png){style="block" border-effect="rounded"}