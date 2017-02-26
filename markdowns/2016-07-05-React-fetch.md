---
title: fetch 获取数据
date: 2016-07-05
tags: [JavaScript,React]
---

```

loadFetch(){
  return fetch(this.props.source)
    .then((response) => response.json())
    .then((responseJson) => {
      console.log(responseJson);
      return responseJson;
    })
    .catch((error) => {
      console.error(error);
    });
}

```
