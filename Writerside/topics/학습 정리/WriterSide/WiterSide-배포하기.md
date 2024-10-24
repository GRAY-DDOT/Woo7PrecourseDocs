# WiterSide 배포하기

> 다음 문서는 WriterSide 의 공식 문서를 요약한 것입니다.
> 원본은 아래 링크를 참고해주세요!
> [로컬 빌드](https://www.jetbrains.com/help/writerside/local-build.html#0)
> [GitHub로 배포](https://www.jetbrains.com/help/writerside/deploy-docs-to-github-pages.html#0)

## 로컬 빌드
로컬 빌드는 InteliJ의 실행 버튼을 누르면 이루어집니다.
Edit Configuration 을 선택하고 빌드할 인스턴스를 선택하고 실행하면면 끝입니다!



## GitHub 로 배포

GitHub Actions를 사용하여 WriterSide 문서화 웹사이트를 빌드하고, 이를 GitHub Pages에 배포할 수 있습니다.

### GitHub Actions 워크플로우 설정하기

WriterSide 프로젝트를 GitHub 로 배포한다면, GitHub Actions 으로 자동화된 빌드 및 배포 과정을 설정할 수 있습니다.
먼저 프로젝트 루트에 `.github/workflows/` 디렉터리를 생성하여 워크플로우 파일을 저장할 준비를 합니다.

이후, `.github/workflows/` 디렉터리에 `build-docs.yml`이라는 YAML 파일을 생성합니다.
이 파일에서 문서를 빌드, 테스트, 배포하는 작업들을 정의하게 됩니다.

### 문서화 웹사이트 빌드하기

다음은 `build-docs.yml`에서 메인 브랜치로의 모든 푸시가 발생할 때마다 트리거되는 기본적인 워크플로우 예시입니다.
아래 워크플로우는 WriterSide 프로젝트를 빌드합니다.
모듈 이름이 `Writerside`이고 기본 인스턴스 ID가 `ddotdocs`인 프로젝트를 빌드합니다.

```yaml
# build-docs.yml 예시
name: Build documentation

on:
  push:
    branches: ["main"]
  workflow_dispatch:

permissions:
  id-token: write
  pages: write

env:
  INSTANCE: 'Writerside/ddotdocs'
  ARTIFACT: 'webHelpDDOTDOCS2-all.zip'
  DOCKER_VERSION: '242.21870'

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Build docs using Writerside Docker builder
        uses: JetBrains/writerside-github-action@v4
        with:
          instance: ${{ env.INSTANCE }}
          artifact: ${{ env.ARTIFACT }}
          docker-version: ${{ env.DOCKER_VERSION }}

      - name: Save artifact with build results
        uses: actions/upload-artifact@v4
        with:
          name: docs
          path: |
            artifacts/${{ env.ARTIFACT }}
            artifacts/report.json
          retention-days: 7

  test:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - name: Download artifacts
        uses: actions/download-artifact@v4
        with:
          name: docs
          path: artifacts

      - name: Test documentation
        uses: JetBrains/writerside-checker-action@v1
        with:
          instance: ${{ env.INSTANCE }}

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    needs: [build, test]
    runs-on: ubuntu-latest
    steps:
      - name: Download artifacts
        uses: actions/download-artifact@v4
        with:
          name: docs

      - name: Unzip artifact
        run: unzip -O UTF-8 -qq '${{ env.ARTIFACT }}' -d dir

      - name: Setup Pages
        uses: actions/configure-pages@v4

      - name: Package and upload Pages artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: dir

      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```
{collapsible="true" default-state="collapsed" }

- **INSTANCE**: 모듈 이름과 인스턴스 ID를 슬래시로 구분하여 설정합니다.
- **ARTIFACT**: Writerside 빌더가 생성한 아카이브의 이름입니다.
- **DOCKER_VERSION**: Writerside Docker 빌더의 버전을 지정합니다.

위 파일을 커밋하고 푸시하면 GitHub 프로젝트 저장소의 **Actions** 탭에서 빌드 작업을 확인할 수 있습니다.

#### 생성된 아티팩트 테스트하기

Writerside 빌더는 빌드 중 발생한 문제를 담은 보고서를 생성합니다.
이 보고서를 수동으로 확인하거나, 별도의 작업을 추가하여 오류가 있을 경우 워크플로우를 실패하도록 설정할 수 있습니다.

이전 예시의 워크플로우 파일을 수정하여 빌드 작업이 생성한 `report.json` 파일을 아티팩트에 포함시키고, 테스트 작업을 추가할 수 있습니다.

```yaml
  test:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - name: Download artifacts
        uses: actions/download-artifact@v4
        with:
          name: docs
          path: artifacts

      - name: Test documentation
        uses: JetBrains/writerside-checker-action@v1
        with:
          instance: ${{ env.INSTANCE }}
```
{collapsible="true" default-state="collapsed" }

테스트 작업은 빌드가 성공적으로 끝났을 때만 실행되고, 빌드 보고서에 오류가 있을 경우 작업이 실패하도록 설정합니다.

### GitHub Pages에 빌드/테스트/배포하기 {id="all-in-one"}

빌드한 아티팩트를 수동으로 또는 별도의 워크플로우에서 배포할 수 있습니다.
하지만 이를 자동화하여 성공적으로 빌드되고 테스트된 아티팩트를 GitHub Pages에 배포하는 작업을 하나의 워크플로우에 설정할 수 있습니다.

#### GitHub Pages 배포 활성화하기 {id="set-GitHub-Pages"}

GitHub 저장소 설정에서 **Settings** > **Pages**로 이동한 후, **Source**에서 **GitHub Actions**를 선택합니다.
이와 같이 워크플로우를 통해 GitHub Pages에 배포할 수 있습니다.

#### 워크플로우 수정 및 배포 작업 추가하기

아래는 제가 이 프로젝트를 배포하기위해 수정한 `build-docs.yml` 입니다.

```yaml
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    needs: [build, test]
    runs-on: ubuntu-latest
    steps:
      - name: Download artifacts
        uses: actions/download-artifact@v4
        with:
          name: docs

      - name: Unzip artifact
        run: unzip -O UTF-8 -qq '${{ env.ARTIFACT }}' -d dir

      - name: Setup Pages
        uses: actions/configure-pages@v4

      - name: Package and upload Pages artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: dir

      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```
{collapsible="true" default-state="collapsed" }

위 파일을 커밋하고 푸시하면, 배포 작업은 빌드와 테스트가 모두 성공했을 때만 실행됩니다.
성공적으로 배포되면, 배포된 문서의 URL이 출력됩니다.

## 배포를 마무리하며

여러분들이 보시는 이 사이트는 위와 같은 과정을 통해 작성되고 배포되었습니다.
종료되지 않은 미션에 대해서는 gitignore 을 적용했으니 안심하셔도 됩니다.
우테코 프리코스인데 너무 많은 시간을 WriterSide를 가지고 노는 것에 사용한 것 같네요.

그래도 흥미롭고 재미있었습니다.
FE와 호스팅, 데이터베이스 걱정 없이 이런 문서 사이트 정도는 쉽게 배포할 수 있어서 좋은 것 같습니다.
무엇보다 **GitHub Action** 을 경험해 볼 수 있다는 점이 가장 큰 장점인 것 같아요.

## 그외의 것들은 공식 문서에서!

공식 문서가 정말 친절하고 자세하게 작성되어 있습니다.
배포에 있어서도 검색 인덱싱 관련 내용도 포함되어 있습니다.
관심이 있으시면 공식 문서를 참고해주세요!