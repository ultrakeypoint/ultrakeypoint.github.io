---
layout: post
title: 다국어 처리 개발 빠르게 하기
date: 2024-07-07
image: /assets/images/blog/2024-07-07/1.png
author: ultrakeypoint
tags: [dev, Element UI, el-table, virtual scroll]
---

웹페이지 전체 중 우리나라 한국말로 작성된 페이지의 총수는 1%도 안 된다는 사실 알고 계셨나요? 전 구글의 디렉터이자, 최초의 비영어권 출신인 로이스 김은 성장하기 위한 3가지 요소를 건강, 네트워크, 그리고 `영어`라고 말합니다. 그만큼 많은 사람과 소통하기 위해서는 영어를 해야 하고, 우리나라 사람 입장에서는 다중 언어를 지원하는 것은 기본적인 항목이 되었습니다. 그리고, 인스타그램의 CEO도 애플리케이션으로 성공하기 위한 1가지를, 작은 번역 오류는 서비스를 이용하는 사용자의 실망감과 이탈률을 올린다고 말합니다. 이처럼 서비스의 품질을 올리기 위해 많이 사용하고 있는 I18N 플러그인과 패키지를 잘 활용하여 방법을 정리해 봅니다.

[국제화 (internationalization, I18N)]

다중 언어를 지원하는 구조는 대부분 유사합니다.

```js
// ko.json
{
  "title": "울트라키포인트"
}

// en.json
{
  "title": "ultrakeypoint"
}
```

이런 파일을 매번 정렬하면서 이쁘게 맞추려고 노력하고 계시나요?  
이제는 그렇게 하지 마시고 아래와 같이 VSCode의 Extension을 사용하여 편리하고 빠르게 팀원과 협업하세요.

![helper1]

```html
<h1>{ translate('ultrakeypoint') }</h1>
<h1>{ t('ultrakeypoint') }</h1>
```

시시스템에 따라 다양하게 html에 설정하여 출력합니다.

![helper2]  
각각의 언어 파일로 이동하여 파일을 수정하지 마시고, 정의된 곳에 마우스를 올리면 자동으로 각각의 언어를 작성할 수 있는 화면이 표시됩니다.

![i18n Folder]

언어 파일이 많으면 많을수록 번역하는 것도 일이지만 그 안에 Object를 만드는 것도 많은 시간이 소요되니 Extension을 통해서 시간을 절약해 보세요.

[i18n Ally 바로가기]

[국제화 (internationalization, I18N)]: https://developer.mozilla.org/ko/docs/Glossary/Internationalization
[i18n Ally 바로가기]: https://marketplace.visualstudio.com/items?itemName=Lokalise.i18n-ally
[helper1]: /assets/images/blog/2024-07-07/2.png
[helper2]: /assets/images/blog/2024-07-07/3.png
[i18n Folder]: /assets/images/blog/2024-07-07/4.png
