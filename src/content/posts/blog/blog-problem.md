---
title: Fuwari - 블로그를 만들때 발생했던 오류들 정리
published: 2024-11-07
description: 'Fuwari 템플릿으로 깃허브 블로그를 만들 때 겪었던 이슈들과 해결책을 소개'
image: ''
tags: [깃허브, Fuwari, Astro]
category: '블로그'
draft: false 
lang: ''
---

## git remote add origin \<repository-url\> error: remote origin already exists

### 오류의 원인

이미 `origin`이라는 이름의 리모트 저장소가 설정되어 있어, 동일한 이름으로 다시 추가하려고 시도하면 충돌이 발생

### 해결 방법

* 리모트 URL 변경 (기존 리모트 저장소를 새 URL로 변경)

```bash
git remote set-url origin <repository-url>
```

* 만약 리모트를 삭제하고 새로 추가하려면 아래 명령을 사용

```bash
git remote remove origin
git remote add origin <repository-url>
```

## ERR_PNPM_OUTDATED_LOCKFILE

해당 에러는 GitHub 워크플로우가 실패할 때 발생하는 에러로, 그 내용의 일부는 다음과 같음

```bash
ERR_PNPM_OUTDATED_LOCKFILE  Cannot install with "frozen-lockfile" because pnpm-lock.yaml is not up to date with package.json

Note that in CI environments this setting is true by default. If you still need to run install in such cases, use "pnpm install --no-frozen-lockfile"

    Failure reason:
    specifiers in the lockfile ({"@astrojs/check":"^0.9.3", ... 
```

### 오류의 원인

1. `pnpm-lock.yaml` 파일이 `package.json`의 의존성과 일치하지 않음

2. `frozen-lockfile` 설정 때문에 `pnpm-lock.yaml`이 업데이트되지 않고, 설치가 실패함

### 해결 방법

`pnpm-lock.yaml` 파일을 최신 상태로 업데이트

로컬 환경에서 아래 명령어를 실행하여 `pnpm-lock.yaml`을 `package.json`에 맞게 업데이트

```bash
pnpm install
```

그 후 `pnpm-lock.yaml` 파일을 커밋하고 푸시

## Author identity unknown *** Please tell me who you are.

### 발생 원인

오류는 Git이 커밋을 만들 때 작성자의 이름과 이메일 정보를 알 수 없어서 발생

### 해결 방법

* 글로벌 사용자 이름과 이메일 설정 (전역 설정)

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

* 특정 저장소에서만 사용자 이름과 이메일 설정 (로컬 설정)

```bash
git config user.name "Your Name"
git config user.email "you@example.com"
```

설정 후 커밋을 다시 시도하면 오류가 해결됨
