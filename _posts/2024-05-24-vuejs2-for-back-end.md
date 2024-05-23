---
layout: post
title: VueJS 5분 가이드 for Back-end
date: 2024-05-23
image: /assets/images/blog/2024-05-24/1.png
author: ultrakeypoint
tags: VueJS, VueJS 2
---

Front-End 개발에 익숙하지 않는 개발자(Back-End, DBA 등)분들을 위해 VueJS 쉽고 빠르게 개발할 수 있도록 초경량 가이드를 만들고자 합니다. 이미 개발에 대한 사전지식이 있다고 가정하고 설명 드리겠습니다. VueJS는 웹을 좀 더 쉽게 개발하기 위해 자바스크립트로 만들어진 Front-End 프래임워크입니다. Back-End에는 Spring Boot, Codeigniter와 같은 역할입니다. VueJS는 이름에 있는 것 처럼 Javascript Framework이고, Javascript에서 동작하는 브라우저에서 실행이 됩니다.

VueJS : `Javascript`  
Spring Boot : `JAVA`  
Codeigniter : `PHP`  

그럼 이제 Vuejs를 위해 환경을 설정해보겠습니다.

VueJS를 설치하기 위해서 Package Manager인 [NPM](https://www.npmjs.com/)을 사용하여 위해 [NodeJS](https://nodejs.org/)가 설치되어 있어야 합니다. 설치는 해당 사이트를 참고하세요.

```bash
// NodeJS 설치 버전 확인  
$ node -v  
v16.19.0
```

NPM은 Java의 Maven이나 PHP의 Composer의 역할입니다.

VueJS : `NPM`  
Spring Boot : `Maven`  
Codeigniter : `Composer`  

Javascript는 모듈링을 하기 위해선 다양한 방식으로 개선되었는데, 현재는 [Webpack](https://webpack.kr/)이나 [Rollup](https://rollupjs.org/)과 같은 Bundler를 통해 실행할 수 있도록 빌드를 진행하는데, NPM을 통해 실행하는 파일인 package.json 파일을 생성합니다.


```cpp
//  some code here
asdfsdf
```

```bash
// Package 관리 파일 생성(package.json)
$ npm init
{
  "name": "vuejs",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```


이제 이 파일에서 프로젝트에서 사용하는 패키지를 관리하게 됩니다.

- VueJS : package.json
- Spring Boot : pom.xml
- Codeigniter : composer.json

그림 이제 VueJS를 설치해보겠습니다.

```
// vue 설치
$ npm install vue@^2 --save
```

Global Standard로써, 람다와 같은 모던 기술이 나오면서 Javascript 또한 발전하였는데, [ECMA-262](https://ecma-international.org/publications-and-standards/standards/ecma-262/)의 6번째 버전인 [ECMA-6](https://ecma-international.org/publications-and-standards/standards/ecma-6/) 이후 버전에 개선되었으며, 대부분의 브라우저가 적용되었다고 생각하시면 됩니다.