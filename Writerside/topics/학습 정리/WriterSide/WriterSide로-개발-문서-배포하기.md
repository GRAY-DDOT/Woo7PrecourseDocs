# WriterSide로 개발 문서 배포하기

## 0. 들어가기

### 프리코스 직전 문서 관리 도구를 변경했다!

본디 옵시디언을 3년 간 사용했습니다.
옵시디언은 가볍고 커스터마이징 요소가 많았죠.
Git을 이용한 버전 컨트롤도 가능했으며 Templator와 Dataview가 매우 편리했습니다.
하지만 너무 많은 커스터 마이징 누적으로 피곤함을 느껴 최근 노션도 다시 사용하기 시작했습다.
노션은 공유를 위한 게시도 편했고 무엇보다 데이터베이스 기능이 매우 편리했죠.
그런데 왜 갑자기 또찌는 무슨 생각으로 갑자기 WriterSide를 사용하기 시작했을까요?

**작업 환경**
: 매번 사용하는 InteliJ와 동일한 디자인과 구성의 에디터를 사용한다.
Writerside는 IntelliJ 플랫폼을 기반으로 하는 JetBrains IDE 입니다.
단축키, 도구 위치, 에러 메시지, 터미널, Git, 프로젝트 파일 구성 등이 같거나 매우 흡사합니다.

**플러그 인**
: JetBrains IDE의 플러그인을 사용할 수 있어요. 즉, InteliJ와 동일한 다양한 플러그인을 사용할 수 있다는 말이죠.
ex)

**MarkDown 지원**
: 마크다운 만으로 웹페이지를 작성할 수 있다.
WriterSide는 기본적으로 기술 문서 작성과 배포를 위해 제작되었습니다.
MD와 XML 두가지 방법으로 전부 작성할 수 있다. 몇몇 소수의 기능과 효과의 경우 XML 작성이 필요합니다.
하지만 대부분의 경우는 마크다운 만으로 작성 가능합니다.
마치 Velog나 Tistroy 같달까요?

**디자인**
: 디자인, 즉 프론트에 대해 고민할 필요가 없다.
컨텐츠만 작성하고 배포하면 됩니다.
그럼 자동으로 **젯브레인 공식 문서**들과 같은 디자인을 적용할 수 있죠.
![writerSideFEpreview.png](writerSideFEpreview.png)

**배포**
: 배포를 시도하는 것 만으로 GitHub Action을 통한 배포과정에 대해 경험할 수 있다.
공식 문서에 관련 설정과 방법 또한 상세하게 설명되어 있습니다.
저도 어렵지 않게 성공했으니 여러분도 쉽게 가능하실 겁니다.
초기에 인스턴스, 트리, 토픽, id 등의 요소들에 문제가 있어 며칠 걸렸습니다.

**Git을 이용한 VSC**
: Git을 지원하는 다양한 에디터들도 많다.
VSC, Obisdian(커뮤니티 플러그인) 등에서는 Git을 지원하며 Notion은 자체적으로 버전 컨트롤을 지원합니다.
WriterSide에서는 InteliJ IDE 작업 환경에 익숙한 사용자가 같은 조건에서 Git으로 문서까지 관리할 수 있어요.

**무료**
: 현재 WriterSide는 EAP, 얼리 액세스이다.
하지만 정식 출시 후에도 마찬가지로 무료로 이용가능합니다.
아래의 이미지는 공식 사이트 FQA에서 관련 사항을 캡쳐한 부분입니다.
![공식 페이지 캡쳐](WriterSide FQA cost.png "공식 페이지 캡쳐")

## 자세한 소개

자세한 소개는 글의 목적과 멀어 공식 페이지 링크를 첨부할게요!
아직 IDE 자체적에는 한글 번역이 적용되지 않았어요...

> [WriterSide 공식 페이지](https://www.jetbrains.com/ko-kr/writerside/)
>
> [API 문서 작성 소개](https://lp.jetbrains.com/api-docs/?_gl=1*drpky8*_ga*MTUwMjk0NjAxMS4xNzE0OTIxMDQy*_ga_9J976DJZ68*MTcyOTE0NDk4NS4yNi4xLjE3MjkxNDgwODcuMC4wLjA.)
>
> [WriterSide 공식 문서](https://www.jetbrains.com/help/writerside/discover-writerside.html)
