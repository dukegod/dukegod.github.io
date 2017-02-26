---
title: 异步回调callback与立即执行 
date: 2017-02-18
tags: [JavaScript]
---

js天生具有的特性。回调用来解决数据请求，肯定是异步调用了。  
具体点，有的时候我们需要把从服务器中得到的数据，进行拼装，这个时候肯定就需要异步调用了。

<!--more-->

```
function reqDate(e, k, callback) {
    if (flag) {
      return
    }
    var body = {
      'pId': e.poolId,
      'cityId': 0
    }
    req({
      url: '/one.msGoodsPool',
      data: {
        body: JSON.stringify(body)
      },
      type: 'get',
      jsonCallback: 'callback',
      success: function (data) {
        // console.log(data)
        if (data && data.data) {
          flag = true;
          callback(data.data.goods);
        }
        flag = true;
        // return listArray;
      },
      error: function () {
        alert('error');
      }
    })
  }

  // 获取数据
  function goodDate(data, callback) {
    for (var k = 0; k < data.tabList.length; k++) {
      (function (i){
        if (data.tabList[i] && data.tabList[i].poolId) {
          var num = i;
          var goodArray = {
            template: data.template,
            bgColor: data.bgColor,
            state: data.state,
            isShowTab: data.isShowTab,
            tabList: {
              tabName: data.tabList[i],
              goodsList: []
            }
          }
          reqDate(data.tabList[i], data, function (goods) {
            console.log(goods);
            goodArray.tabList.goodsList.push(goods);
            callback(goodArray, num)
          });
        }
      })(k)
    }
  }
  
  // 调用
  
    good.goodDate(v, function (list, key) {
      console.log(key);
      console.log(list);
    })
```

异步调用把整个函数当做参数传入（callback），把请求的返回值放在另一个函数中进行处理。

```
reqDate(data.tabList[i], data, function (goods) {
    console.log(goods);
    goodArray.tabList.goodsList.push(goods);
});

// 处理另一个callback
good.goodDate(v, function (list, key) {
  console.log(key);
  console.log(list);
})
```

for循环不能立即处理i的问题，使用立即执行函数。

```
for (var k = 0; k < data.tabList.length; k++) {
  (function (i){
    if (data.tabList[i] && data.tabList[i].poolId) {
      var num = i;
      var goodArray = {
        template: data.template,
        bgColor: data.bgColor,
        state: data.state,
        isShowTab: data.isShowTab,
        tabList: {
          tabName: data.tabList[i],
          goodsList: []
        }
      }
      reqDate(data.tabList[i], data, function (goods) {
        console.log(goods);
        goodArray.tabList.goodsList.push(goods);
        callback(goodArray, num)
      });
    }
  })(k)
}
```

弊端就是所谓的回调地狱，可以通过其他的一些库进行解决