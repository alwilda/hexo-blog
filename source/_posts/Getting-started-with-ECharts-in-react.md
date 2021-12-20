---
title: 在 React 中初始化 ECharts
date: 2021-08-31 10:50:02
tags:
  - React
  - ECharts
categories:
---

习惯了传统的 DOM 操作，在页面上使用 [ECharts](https://echarts.apache.org/zh/index.html) 似乎感觉更方便，好比：

```js
var myChart = echarts.init(document.getElementById('main'));
```

但是在使用了 React 这种 **声明式**/**组件化** 的 JavaScript 库之后，对于 DOM 的操作大大减少了，那么在 React 中该如何初始化一个 ECharts 对象呢？

<!--more-->

```tsx
import { useEffect, useRef } from "react";
import * as echarts from "echarts";

let option = {
    ...
};

function Chart(props: any) {
  let myChart = useRef<echarts.EChartsType | null>(null);

  const renderChart = () => {
    if (myChart.current === null) {
      return;
    }
    myChart.current.setOption(option);
  };

  useEffect(() => {
    renderChart();
  }, []);

  return (
    <div
      ref={(e) => {
        if (e !== null) {
          myChart.current = echarts.init(e);
        }
      }}
      className={props.className}
    ></div>
  );
}
```

😶 上面是更好的方式吗 ❓