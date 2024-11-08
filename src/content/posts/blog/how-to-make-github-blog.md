---
title: Fuwari를 이용해 깃허브 블로그 만들기
published: 2024-11-06
description: 'Fuwari 템플릿을 이용해 깃허브 블로그를 만드는 방법에 대한 소개'
image: ''
tags: [가이드, 깃허브, Fuwari, Astro]
category: '블로그'
draft: false 
---

소개와 용어 설명을 건너뛰고싶다면 [여기](#새-github-저장소-생성)를 클릭

따라 하는 중 오류가 발생했다면, [여기](/posts/blog/blog-problem/)를 클릭해 참고

## 소개 및 용어 설명

### Fuwari란?

Astro로 구축된 정적 블로그 템플릿

::github{repo="saicaca/fuwari"}

데모 사이트: https://fuwari.vercel.app/

#### 특징

- [Astro](https://astro.build) 및 [Tailwind CSS](https://tailwindcss.com)로 구축됨
- 부드러운 애니메이션 및 페이지 전환 + 반응형 디자인
- 사용자 정의 가능한 테마 색상 및 배너
- 라이트 모드 / 다크 모드
- 검색
- 목차

### 깃허브 블로그란?

GitHub Pages를 이용해 무료로 만들 수 있는 블로그

#### GitHub Pages란?

깃허브 저장소의 파일을 웹사이트로 호스팅해주는 기능

주로 정적 웹사이트 생성기인 Jekyll이나 Astro, Hexo 같은 도구를 사용해 사이트를 생성하고, GitHub에 푸시하여 배포

https://docs.github.com/ko/pages

### Astro란?

정적 사이트 생성기이자 웹 프레임워크

빠르고 가볍게 블로그와 같은 콘텐츠 중심 웹사이트를 웹사이트를 구축할 수 있게 해줌

#### Astro 프로젝트 구조

https://docs.astro.build/ko/basics/project-structure/

---

## 새 GitHub 저장소 생성

https://github.com/new

Repository name은 `<username>.github.io` 로 해야함

![새 GitHub 저장소 생성 사진](/assets/how-to-make-github-blog/2024-11-06%20134840.png)

## 레포지토리 복제

복제할 디렉토리로 이동한 후 git clone 명령어 사용 후 복제한 fuwari 폴더로 이동

```bash
git clone https://github.com/saicaca/fuwari.git
cd fuwari
```

## 종속성 설치

:::important
아직 [pnpm](https://pnpm.io)을 설치하지 않았다면 `npm install -g pnpm`을 실행하여 [pnpm](https://pnpm.io)을 설치
:::

```bash
pnpm install && pnpm add sharp
```

## 블로그 구성 파일 편집

`src/config.ts` 열어서 블로그를 커스터마이징

더 자세한 내용은 [여기](/posts/blog/blog-config/)를 클릭

## (옵션) 새 게시물 생성

`pnpm new-post <filename>`을 실행하여 새 게시물을 만들고 `src/content/posts/`에서 편집

## Github Pages용 Astro 구성

GitHub 페이지에 배포하기 위해서는 배포하기 전에 `astro.config.mjs`에서 사이트 구성을 편집해야 함

### github.io URL에 배포

`astro.config.mjs`에서 아래와 같이 site 및 base 옵션을 설정

```yml
export default defineConfig({
  site: 'https://<username>.github.io',
  base: '/',
```

### GitHub Action 구성

프로젝트에서 `.github/workflows/deploy.yml` 파일을 만들고 아래 YAML 내용을 붙여넣기

```yml
name: Deploy to GitHub Pages

on:
  # 'main' 브랜치로 푸시할 때마다 워크플로를 트리거합니다.
  # 다른 브랜치 이름을 사용하시나요? `main`을 브랜치 이름으로 바꾸세요.
  push:
    branches: [ main ]
  # GitHub의 Actions 탭에서 이 워크플로를 수동으로 실행할 수 있습니다.
  workflow_dispatch:

# Allow this job to clone the repo and create a page deployment
permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout your repository using git
        uses: actions/checkout@v4
      - name: Install, build, and upload your site
        uses: withastro/action@v3
        # with:
          # path: . # 저장소 내 Astro 프로젝트의 루트 위치입니다. (선택 사항)
          # node-version: 20 # 사이트를 빌드하는 데 사용해야 하는 특정 버전의 Node입니다. 기본값은 20입니다. (선택 사항)
          # package-manager: pnpm@latest # 종속성을 설치하고 사이트를 빌드하는 데 사용해야 하는 노드 패키지 관리자입니다. lockfile을 기반으로 자동으로 감지됩니다. (선택 사항)

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### GitHub Actions을(를) 사용하여 게시하도록 사이트를 구성

GitHub에서 저장소의 Settings 탭으로 이동하여 설정의 Pages 섹션을 찾은다음

사이트의 Source로 GitHub Actions를 선택

![GitHub Actions 설정 사진](/assets/how-to-make-github-blog/2024-11-06%20134008.png)

## (옵션) 로컬 블로그 테스트

`pnpm dev` 명령어를 실행하여 `localhost:4321`에서 로컬 개발 서버를 시작해 테스트

## 새 저장소에 로컬 파일 푸시

아래의 명령어들을 실행

```bash
# 터미널(또는 명령 프롬프트)을 열고, 아래 명령어로 로컬 저장소를 초기화
git init

# 기존 파일을 모두 추가
git add .

# 추가한 파일들을 커밋
git commit -m "Initial commit"

# GitHub 저장소에 로컬 저장소를 연결
git remote set-url origin <repository-url>

# (옵션, 윈도우 기준) Git Credential Manager 사용 설정
git config --global credential.helper manager

# 사용자 이메일과 이름을 설정 (이전에 전역 설정을 했다면 생략 가능)
git config user.email "you@example.com"
git config user.name "Your Name"

# 로컬 커밋을 GitHub 저장소에 푸시
# (기본 브랜치 이름이 main이 아닌 master일 수도 있음. 
# 현재 브랜치 이름을 확인하려면 git branch 명령어를 사용)
git push -u origin main
```

## 빌드 확인

GitHub에서 저장소의 Actions 탭으로 이동해 워크플로 수행여부 확인

## 배포된 깃허브 블로그 접속

워크플로가 성공했으면 `https://<username>.github.io`로 접속해 정상적으로 사이트에 접근 가능
