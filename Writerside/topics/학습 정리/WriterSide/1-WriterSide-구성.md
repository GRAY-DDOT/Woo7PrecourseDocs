# WriterSide 구성

## 1. 구성 소개

WriterSide의 **가장 큰 구성은 프로젝트**입니다.
그리고 내부의 컨탠츠를 바라보는 두 가지 관점이 있습니다.
바로 **모듈**(Module)과 **인스턴스**(Instance)이죠.
모듈은 프로젝트 패키지 관점으로 구분되며 인스턴스는 배포 단위로 구분될 수 있어요.
모듈은 프로젝트를 편의에 따라 여러 패키지로 구성 가능하게 하는 목적이 강한 반면,
인스턴스는 배포의 관점에서 별도로 배포할 컨텐츠를 관리할 수 있어요.

### 1.1 모듈 : 논리적 단위

모듈은 무엇

![WriterSideModule.png](WriterSideModule.png){: width="300"}

모듈은 그 이름과 같은 .cfg 파일을 갖음. 별도 모듈로 생성 가능

![WriterSideModuleCfg.png](WriterSideModuleCfg.png){: width="300"}

### 1.2 인스턴스 : 배포 단위

인스턴스의 모습
![WriterSideInstance.png](WriterSideInstance.png){: width="300"}

![WriterSIde-Instance-more.png](WriterSIde-Instance-more.png){: width="300"}

![WriterSide-Render.png](WriterSide-Render.png){: width="300"}

![WriterSide-add-instance.png](WriterSide-add-instance.png){: width="300"}

### 1.3 토픽
