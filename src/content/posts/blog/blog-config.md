---
title: Fuwari - src/config.ts 파일 설명
published: 2024-11-07
description: 'Fuwari 블로그를 커스터마이징하기 위한 config.ts 설정법'
image: ''
tags: [깃허브, Fuwari, Astro]
category: '블로그'
draft: false 
---

## siteConfig

`siteConfig`: 웹사이트 설정을 위한 구성 파일

```ts
export const siteConfig: SiteConfig = {
  title: 'EunsangJo',           // 사이트 제목
  subtitle: 'Dev blog',          // 사이트 부제목
  lang: 'ko',                    // 기본 언어 ('en', 'zh_CN', 'zh_TW', 'ja', 'ko' 중 선택 가능)
  themeColor: {
    hue: 160,                    // 테마 색상의 기본 색조 (0에서 360 사이의 값. 예: 빨강: 0, 청록: 200, 청록색: 250, 핑크: 345)
    fixed: false,                // 방문자에게 테마 색상 선택기 숨기기 여부
  },
  banner: {
    enable: false,               // 배너 사용 여부
    src: 'assets/images/demo-banner.png',   // 배너 이미지 경로 (/src 디렉터리를 기준으로 한 상대 경로, '/'로 시작하면 /public을 기준으로 함)
    position: 'center',          // 배너 이미지 위치 ('top', 'center', 'bottom' 중 선택 가능, 기본값은 'center')
    credit: {
      enable: false,             // 배너 이미지의 출처 텍스트 표시 여부
      text: '',                  // 표시할 출처 텍스트
      url: ''                    // (선택 사항) 원본 작품이나 작가 페이지의 URL 링크
    }
  },
  toc: {
    enable: true,                // 게시물 오른쪽에 목차 표시 여부
    depth: 2                     // 목차에 표시할 최대 제목 깊이 (1에서 3 사이의 값)
  },
  favicon: [                     // 이 배열을 비워 두면 기본 파비콘을 사용
    // {
    //   src: '/favicon/icon.png',    // 파비콘 경로 (/public 디렉터리를 기준으로 함)
    //   theme: 'light',              // (선택 사항) 'light' 또는 'dark', 라이트 모드와 다크 모드에서 다른 파비콘이 있을 때 설정
    //   sizes: '32x32',              // (선택 사항) 파비콘의 크기. 다른 크기의 파비콘이 있을 때 설정
    // }
  ]
}
```

## navBarConfig

`navBarConfig`: 네비게이션 바 구성을 위한 설정 파일

```ts
export const navBarConfig: NavBarConfig = {
  links: [
    LinkPreset.Home,               // 홈 페이지 링크
    LinkPreset.Archive,            // 아카이브 페이지 링크
    LinkPreset.About,              // 소개 페이지 링크
    {
      name: 'GitHub',              // 링크 이름 ('GitHub')
      url: 'https://github.com/EunsangJo/EunsangJo.github.io', // 외부 사이트 링크 URL (내부 링크의 경우 기본 경로는 자동으로 추가되므로 포함하지 않음)
      external: true,              // 외부 링크 여부. true일 경우 외부 링크 아이콘이 표시되며 새 탭에서 열림
    },
  ],
}
```

## profileConfig

`profileConfig`: 프로필 구성을 위한 설정 파일

```ts
export const profileConfig: ProfileConfig = {
  avatar: 'assets/images/avatar.png',  // 프로필 아바타 이미지 경로 (/src 디렉터리를 기준으로 한 상대 경로, '/'로 시작하면 /public을 기준으로 함)
  name: 'EunsangJo',                   // 프로필에 표시할 이름
  bio: 'Contact: jeuuniv@gmail.com',   // 프로필 소개 또는 연락 정보
  
  links: [
    {
      name: 'Baekjoon',                // 링크 이름 ('Baekjoon')
      icon: 'fa6-solid:code',          // 아이콘 코드 (아이콘 코드는 https://icones.js.org/에서 확인 가능)
                                       // 필요한 아이콘 세트가 포함되어 있지 않다면, `pnpm add @iconify-json/<icon-set-name>`로 설치 필요
      url: 'https://www.acmicpc.net/user/jeu003', // 백준 사용자 페이지 링크
    },
    {
      name: 'GitHub',                  // 링크 이름 ('GitHub')
      icon: 'fa6-brands:github',       // 아이콘 코드 (GitHub 아이콘)
      url: 'https://github.com/EunsangJo', // GitHub 프로필 링크
    },
  ],
}
```

## licenseConfig

`licenseConfig`: 사이트의 라이선스 설정을 위한 구성 파일

```ts
export const licenseConfig: LicenseConfig = {
  enable: true,                         // 라이선스 표시 여부 (true일 경우 라이선스가 표시됨)
  name: 'CC BY-NC-SA 4.0',              // 적용할 라이선스 이름 (CC BY-NC-SA 4.0, 저작자 표시-비영리-동일조건 변경 허락)
  url: 'https://creativecommons.org/licenses/by-nc-sa/4.0/', // 라이선스에 대한 상세 정보를 제공하는 URL
}
```
