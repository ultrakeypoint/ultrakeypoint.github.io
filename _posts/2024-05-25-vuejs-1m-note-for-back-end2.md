---
layout: post
title: VueJS 1분 노트 for Back-End 2
date: 2024-05-25
image: /assets/images/blog/2024-05-24/1.png
author: ultrakeypoint
tags: [dev, VueJS2, Back-End]
---

클라이언트의 긴급한 요청이나 같이 일하던 동료가 퇴사하여 결원이 발생할 경우, 사업이 확장되어 프로젝트의 개발 범위가 늘어나서, 백앤드를 담당하고 있지만 프론트 개발자를 도와줘야 될 경우 등등 VueJS를 빠르게 신속하게 개발하여 결과물을 만들어야 될 이유가 종종 생긴다. 그러나, 정확하게 이해하지 못한 개녕으로 기존에 개발되어 있는 코드만 Copy/Paste 하는 코드몽키가 되어, 새로운 복작한 로직이 들어가면 본인이 이 코드를 왜 넣어야 되는지도 모르고, 재사용과 확장성을 무시하여 기존에 있던 시스템 마저 엉망이 될 수 있다.

자!, 그럼, VueJS 최소한의 핵심이라도 정확하게 알고, 프로젝트에 참여해보자.

_Front-End 개발에 익숙하지 않는 개발자(Back-End, DBA 등)를 위해 VueJS 쉽고 빠르게 개발할 수 있도록 만든 초경량 가이드입니다. 이미 개발에 대한 사전지식이 있다고 가정합니다._

#### VueJS 핵심 요소 7가지

[`Component`](#component) 화면 또는 기능 구성  
[`Render`](#render) 화면에 보여주는 처리  
[`Style`](#style) 화면에 다양한 스타일 처리  
[`Computed`](#computed) 복잡한 연산 처리  
[`Watcher`](#watcher) 데이터 변화 감지  
[`Event`](#event) 클릭 등 이벤트 처리  
[`Store`](#store) 컴포넌트 간 상태 공유

### `Component`

##### 단일 파일로 구성하고 1개의 화면 또는 1개의 기능으로 분리한다.

<b>template</b> : 화면에 표시되는 영역  
<b>script</b> : 화면을 제어하기 위한 스크립트  
<b>style</b> : 화면의 스타일링

예제 :
{% raw %}

```vue
<template>
  <p>{{ greeting }} World!</p>
</template>

<script>
module.exports = {
  data: function () {
    return {
      greeting: "Hello"
    };
  }
};
</script>

<style scoped>
p {
  font-size: 2em;
  text-align: left;
}
</style>
```

{% endraw %}
결과 :

```text
Hello World!
```

### `Render`

<b>v-show</b> : 화면에 항상 Rendering 되어 표시  
<b>v-if</b> : 화면에 표시될 경우만 Rendering 되어 표시  
<b>v-for</b> : 화면에 반복해서 Rendering 되어 표시

예제 :
{% raw %}

```vue
<template>
  <div>
    <p v-show="always">always render and visible</p>
    <p v-show="!always">always render and no visible</p>
    <p v-if="show">render and visible</p>
    <p v-if="!show">no render and no visible</p>
    <p v-for="ball in balls">No.{{ ball + 1 }} ball</p>
  </div>
</template>

<script>
module.exports = {
  data: function () {
    return {
      always: true,
      show: true,
      greeting: "Hello",
      balls: [0, 1, 2]
    };
  }
};
</script>

<style scoped>
p {
  font-size: 2em;
  text-align: left;
}
</style>
```

{% endraw %}

결과 :

```text
always render and visible

render and visible

No.1 ball

No.2 ball

No.3 ball
```

### `Style`

<b>:class</b> : style을 이용하여 다양하게 스타일링

예제 :
{% raw %}

```vue
<template>
  <div>
    <p>default, No Active</p>
    <p :class="{active}">Active</p>
  </div>
</template>

<script>
module.exports = {
  data: function () {
    return {
      active: true,
      big: true,
      small: false,
      greeting: "Hello"
    };
  }
};
</script>

<style scoped>
.active {
  display: block;
}
p {
  display: none;
}
</style>
```

{% endraw %}

결과 :

```text
Active
```

### `Computed`

##### 복잡하게 연산되는 결과 값을 template에 함축적으로 표시할 때 사용

예제:
{% raw %}

```vue
<template>
  <div>message : {{ reversedMessage }}</div>
</template>

<script>
module.exports = {
  data: function () {
    return {
      message: "Hello"
    };
  },
  computed: {
    reversedMessage: function () {
      return this.message.split("").reverse().join("");
    }
  }
};
</script>
```

{% endraw %}
결과:

```text
message : olleH
```

### `Watcher`

##### 데이터 변화를 확인하고 새로운 로직을 만들 때 사용

예제:
{% raw %}

```vue
<template>
  <div id="watch-example">
    <p>
      Are you zero?
      <input v-model="typing" />
    </p>
    <p v-if="isAnswer">Good</p>
    <p v-if="!isAnswer">Yet</p>
  </div>
</template>

<script>
module.exports = {
  data: function () {
    return {
      typing: "",
      isAnswer: ""
    };
  },
  watch: {
    typing: function (newAnswer, oldAnswer) {
      this.isAnswer = 0 === Number(newAnswer);
    }
  }
};
</script>
```

{% endraw %}

결과:

```text
Are you zero? 0

Good
```

### `Event`

##### template에서 발생하는 이벤트를 처리할 때 사용

예제:
{% raw %}

```vue
<template>
  <div id="example-1">
    <button @click="counter += 1">Add 1</button>
    <p>The button above has been clicked {{ counter }} times.</p>
  </div>
</template>

<script>
module.exports = {
  data: function () {
    return {
      counter: 0
    };
  }
};
</script>
```

{% endraw %}

결과:

```text
[Add]

The button above has been clicked 6 times.
```

### `Store`

##### 데이터의 흐름을 단방향으로 처리하고, 컴포넌트와 컴포넌트의 상태를 공유.

![Store]

예제:
{% raw %}

```vue
<script>
var sourceOfTruth = {};

var vmA = new Vue({
  data: sourceOfTruth
});

var vmB = new Vue({
  data: sourceOfTruth
});
</script>
```

{% endraw %}

{% raw %}

```vue
<script>
var store = {
  debug: true,
  state: {
    message: "Hello!"
  },
  setMessageAction(newValue) {
    if (this.debug) console.log("setMessageAction triggered with", newValue);
    this.state.message = newValue;
  },
  clearMessageAction() {
    if (this.debug) console.log("clearMessageAction triggered");
    this.state.message = "";
  }
};
</script>
```

{% endraw %}

{% raw %}

```vue
<script>
var vmA = new Vue({
  data: {
    privateState: {},
    sharedState: store.state
  }
});

var vmB = new Vue({
  data: {
    privateState: {},
    sharedState: store.state
  }
});
</script>
```

## {% endraw %}

VueJS 7개의 핵심개념을 알아보았습니다.  
프로젝트를 진행하면 이미 개발되어 있는 부분이나 참고할만 자료가 있으면 핵심개념과 조합하여 잘 활용하시길 바랍니다.

`도움이 되셨다면, 댓글 부탁 드립니다.` :+1:

<!-- 이미지 -->

[Store]: /assets/images/blog/2024-05-25/1.png
