---
title: 只在更新时运行 effect
date: 2021-07-20 11:08:48
tags: React
categories:
---

{% blockquote @Hooks FAQ https://zh-hans.reactjs.org/docs/hooks-faq.html#can-i-run-an-effect-only-on-updates  %}
这是个比较罕见的使用场景。如果你需要的话，你可以 [使用一个可变的 ref](https://zh-hans.reactjs.org/docs/hooks-faq.html#is-there-something-like-instance-variables) 手动存储一个布尔值来表示是首次渲染还是后续渲染，然后在你的 effect 中检查这个标识。（如果你发现自己经常在这么做，你可以为之创建一个自定义 Hook。
{% endblockquote %}

<!--more-->

<br />

💻 编写代码如下：

```js
import { useEffect, useRef, useState } from "react";

/**
 * 仅在更新时执行
 *
 * @param {React.EffectCallback} effect
 * @param {React.DependencyList} deps
 */
function useUpdateEffect(effect, deps) {
  const hasMounted = useRef(true);

  useEffect(() => {
    if (hasMounted.current) {
      return;
    }
    return effect();
  }, deps);

  useEffect(() => {
    hasMounted.current = false;
  }, []);
}
```

❓ 疑问：

这样使用的话 `eslint-plugin-react-hooks` 会产生两个警告：

1. React Hook useEffect was passed a dependency list that is not an array literal. This means we can't statically verify whether you've passed the correct dependencies. [<em>eslintreact-hooks/exhaustive-deps</em>](https://github.com/facebook/react/issues/14920)

2. React Hook useEffect has a missing dependency: 'effect'. Either include it or remove the dependency array. If 'effect' changes too often, find the parent component that defines it and wrap that definition in useCallback. [<em>eslintreact-hooks/exhaustive-deps</em>](https://github.com/facebook/react/issues/14920)

会有什么问题呢 😶 ❔