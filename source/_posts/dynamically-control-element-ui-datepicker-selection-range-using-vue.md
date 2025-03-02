---
title: 使用 Vue 动态控制 Element-UI 的 DatePicker 选择范围
date: 2021-06-05 22:20:39
tags:
  - Vue
  - Element UI
categories:
---

绝大多数情况下我们需要对可选择的日期时间加以范围的控制，而 [`Element-UI`](https://element.eleme.cn/#/zh-CN) 也提供了 `Picker Options` 属性来进行配置。

<!--more-->

# 简述

Picker Options

| 参数| 说明 |类型 |可选值| 默认值 | 
| ---- | ---- | ---- | ---- | ---- |
| disabledDate | 设置禁用状态，参数为当前日期，要求返回 Boolean | Function | — | — |

# 初探 `disabledDate`

首先，先构造两个普通的 `DatePicker` ：

<div style="width:70%;">
{% asset_img code-1.png 构造两个普通DatePicker的代码 %}
</div>

属性 `picker-options` 是一个对象，而 `disabledDate` 又是 `picker-options` 的一个属性，其值是一个 `Function`，接收一个参数 —— 当前选择的日期。

```html
<el-date-picker
  v-model="date1"
  type="date"
  :picker-options="pickerOptions1"
  placeholder="选择日期 - 1"
>
</el-date-picker>
```

```js
export default {
  data() {
    pickerOptions1: {
      disabledDate: function (now) {
        return now > new Date();
      }
    }
  }
};
```

如上面的代码，参数 `now` 代表要选择的日期，`return now > new Date();` 就表示不能选择大于今天的日期，因为选择大于今天就返回 `true`，而`true` 就表示被禁用。

# 动态配置可选范围

使用 [**计算属性**](https://v3.cn.vuejs.org/guide/computed.html)

```html
<el-date-picker
  v-model="date2"
  type="date"
  :picker-options="pickerOptions2"
  placeholder="选择日期 - 2"
>
</el-date-picker>
```

```js
export default {
  computed: {
    pickerOptions2: function () {
      return {
        // 使用箭头函数是因为其不绑定 this ，否则使用 date1 那 this 就在当前 Function 的作用域
        disabledDate: (now) => {
          return now > this.date1;
        },
      };
    },
  },
};
```

