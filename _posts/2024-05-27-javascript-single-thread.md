---
layout: post
title: Javascript Single Thread
date: 2024-05-27
image: /assets/images/blog/2024-05-27/1.png
author: ultrakeypoint
tags: [dev, javascript, thread]
---

Javascript는 개발하다보면 데이터를 불러오고, 저장하고, 반복적으로 호출하는 등 다양한 요청을 어떻게 처리할지 고민하게 된다. XMLHttpRequest, Ajax, Axio, Promise, await, async 등등 동시성 기능을 개선하기위해 오래전부터 발전해왔다.

몇십년이 지난 지금은 Package나 Libraray를 통해 쉽고 편리하게 사용하고 있다. 그런데, 우리는 한번쯤 `Javascript는 Single Thread`라는 얘기를 들어본적이 있을 것이다. Thread가 1개라는 것은 1개의 로직만 실행할 수 있다는 것인데, 어떻게 여러 개의 로직을 비동기적으로 처리할 수 있을까?

브라우저가 런타임 때 동작할 코드를 Call Stack에 등록하고, Web API를 통해 실행하고 이후에 처리될 내용을 Task Queue 등록한 후 Call Stack이 비워질 때 까지 대기 후 처리한다. 이 동작은 브라우저에서 처리하기 때문에 자세하게 알면 좋겠지만 생략하고, <u>이 동작은 정확한 시간에 처리가 안될 수도 있다는 것이 중요한 포인트다.</u>

```javascript
setTimeout(() => console.log("Hello World"), 3000);
```

위 코드는 3초 후에 Hello World를 로그를 찍는 단순한 코드이다. 여기서 정확하게 알아야 될 부분은 3초 후에 실행한다가 아닌 `최소 3초를 기다려야 하는 시간`이라는 것이다. Javascript는 Single Thread이면서, 메세지큐를 처리하는 이벤트 루프의 논블로킹 처리 특징 때문에 정확한 시간에 처리될 수도 있고, 처리하지 못할 수도 있다. 하지만 이런 특징 덕분에 이벤트를 처리하면서 계속적으로 사용자의 입력을 처리할 수 있는 것이 매력적이다.

![EventLoopVisual]  
(출처: [EventLoop])

`도움이 되셨다면, 댓글 부탁 드립니다.` :+1:

<!-- 이미지 -->

[EventLoopVisual]: /assets/images/blog/2024-05-27/2.png

<!-- 링크 -->

[EventLoop]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Event_loop
