---
layout: post
title: VueJS 1분 노트 for Back-End 1
date: 2024-05-24
image: /assets/images/blog/2024-05-24/1.png
author: ultrakeypoint
tags: [VueJS2, Back-End]
---

Front-End 개발에 익숙하지 않는 개발자(Back-End, DBA 등)를 위해 VueJS 쉽고 빠르게 개발할 수 있도록 만든 초경량 가이드입니다. 이미 개발에 대한 사전지식이 있다고 가정합니다. VueJS는 웹을 좀 더 쉽게 개발하기 위해 Javascript로 만들어진 Front-End 프래임워크입니다. Back-End에는 Spring Boot, Codeigniter와 같은 역할입니다. VueJS는 이름처럼 Javascript Framework이고, Javascript를 동작시키는 브라우저에서 실행이 됩니다.

VueJS : `Javascript`  
Spring Boot : `JAVA`  
Codeigniter : `PHP`

그럼 이제 Vuejs를 위해 환경을 설정해보겠습니다.

VueJS를 설치하기 위해서 Package Manager인 [NPM]을 사용하여 위해 [NodeJS]가 설치되어 있어야 합니다. 설치는 해당 사이트를 참고하세요.

```bash
// NodeJS 설치 버전 확인

$ node -v
v16.19.0
```

그럼, 이제 VueJS를 설치합니다. 그전에 VueJS를 사용하기위해 수동으로 일일히 추가하지 않고, CLI를 사용하여 VueJS 프로젝트를 한번에 생성할 수 있도록 합니다.

```bash
// -g는 해당 프로젝트(package.json)에 국한된 것이 아닌  컴퓨터 전체(global)에서 사용하기 위해 설치합니다.

$ npm install -g vue-cli
$ vue --version
2.9.6
```

NPM은 Javascript(Node) Package를 관리하기위해 필요하며, Java의 Maven, PHP의 Composer와 같은 역할입니다

VueJS : `NPM` - `package.json`  
Spring Boot : `Maven` - `pom.xml`  
Codeigniter : `Composer` - `composer.json`

람다와 같은 모던 기술이 나오면서, Javascript 또한 발전하였는데, [ECMA-262]의 6번째 버전인 [ECMA-6] 이후 버전에서 안정화되어 지금까지 널리 사용되고 있으며, 대부분의 브라우저가 적용 되어 있습니다. 이후 수많은 Assets(js, css, html 등등)을 관리하기 위해 [Webpack]이나 [Rollup]과 같은 bundler가 프로젝트에 포함되었고, 이것을 포함해서 프로젝트를 생성합니다.

```bash
// vue-cli를 통해 vue-project 라는 VueJS 프로젝트 생성

$ vue init webpack vue-project
```

WebPack 기반 VueJS 프로젝트를 실행합니다.

```bash
// script를 쉽게 실행할 수 있도록 package.json scripts 에 정의합니다.
// package.json의 scripts(스크립트) 중에 dev를 실행한다. (= Webpack VueJS 프로젝트 구동)

$ npm run dev
```

- ![VueJS]

여기까지 기본적인 VueJS 프로젝트 구동을 설명하였고, 다음 글에서는 [VueJS 핵심개념](/2024/05/25/vuejs-1m-note-for-back-end2/)에 대해 설명 드리겠습니다.  

`도움이 되셨다면, 댓글 부탁 드립니다.` :+1:  

<!-- 이미지 -->

[VueJS]: /assets/images/blog/2024-05-24/2.png

<!-- 링크 -->

[NPM]: https://www.npmjs.com/
[NodeJS]: https://nodejs.org/
[ECMA-262]: https://ecma-international.org/publications-and-standards/standards/ecma-262/
[ECMA-6]: https://ecma-international.org/publications-and-standards/standards/ecma-6/
[Webpack]: https://webpack.kr/
[Rollup]: https://rollupjs.org/
