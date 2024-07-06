---
layout: post
title: Vue Table 10만 데이터 로드하기
date: 2024-07-06
image: /assets/images/blog/2024-07-06/1.png
author: ultrakeypoint
tags: [dev, Element UI, el-table, virtual scroll]
---

서비스 초기에는 데이터가 많지 않아 테이블에 데이터를 로드하는 데 이슈가 많지 않습니다. 하지만, 서비스가 한 달, 두 달, 1년 ~ 5년 되다 보면 데이터의 양도 많고 데이터의 종류도 다양해진다. 이번에는 Vue Element UI를 통해서 10만 개 데이터를 화면에 보여줄 방법을 설명합니다.

핵심 이론은 아래와 같이 데이터를 가공하는 것입니다. 전체 목록의 데이터(`rawList`) 중 가공할 데이터(`viewList`)를 찾는 것이다. 위치는 전체 스크롤에서 해당 스크를의 위치에 보여줘야 할 데이터만 계산하면 됩니다.

```javascript
const rawList = ["ant", "bison", "camel", "duck", "elephant"];
const viewList = rawList.slice(2, 4);
```

하지만, 우리는 시간도 없고, 고객님은 항상 급해서, 빠르게 만들어야 되기 때문에 패키지를 사용합니다.

예제: [virtual scroll 예제]  
소스: [virtual scroll 예제 소스]  
패키지: [el-table], [el-table-virtual-scroll]

##### 핵심 소스

```html
<virtual-scroll
  :data="list"
  :item-size="62"
  key-prop="id"
  @change="(renderData) => (virtualList = renderData)">
  <el-table
    row-key="id"
    height="500px"
    :data="virtualList">
    <el-table-column
      prop="id"
      label="No"
      width="80" />
    <el-table-column
      prop="date"
      label="Date"
      width="100"></el-table-column>
    <el-table-column
      prop="name"
      label="Name"
      width="100"></el-table-column>
    <el-table-column
      prop="address"
      label="Address"></el-table-column>
  </el-table>
</virtual-scroll>
```

[virtual scroll 예제]: https://ultrakeypoint.github.io/el-table-virtual-scroll/
[virtual scroll 예제 소스]: https://github.com/ultrakeypoint/el-table-virtual-scroll
[el-table]: https://element.eleme.io/#/en-US/component/table
[el-table-virtual-scroll]: https://github.com/xiaocheng555/el-table-virtual-scroll
