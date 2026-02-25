---
title: 使用 Hexo 写作
date: 2021-02-21 21:12:56
tags: Hexo
---

# 安装与新建

安装 Hexo。

```bash
npm install -g hexo-cli
```

安装完成后，执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。

```bash
hexo init <folder>
cd <folder>
npm install
```

<!-- more -->

初始化后，项目文件夹将如下所示：

```
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

# 配置

> https://hexo.io/zh-cn/docs/configuration

# 写作

## 创建新页面

执行下列命令来创建一篇新文章或者新的页面。

```bash
hexo new [layout] <title>
```

## Front-matter

Front-matter 是 YAML 格式，它位于文章的开头，用 `---` 包围。

```yaml
---
title: 使用 Hexo 写作
date: 2021-02-21 21:12:56
tags: Hexo
---
```

设置 & 默认值:

| 设置            | 描述                                                                                                      | 默认值                                                        |
| --------------- | --------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| layout          | 布局                                                                                                      | config.default_layout                                         |
| title           | 标题                                                                                                      | 文章的文件名                                                  |
| date            | 建立日期                                                                                                  | 文件建立日期                                                  |
| updated         | 更新日期                                                                                                  | 文件更新日期                                                  |
| comments        | 开启文章的评论功能                                                                                        | TRUE                                                          |
| tags            | 标签（不适用于分页）                                                                                      |                                                               |
| categories      | 分类（不适用于分页）                                                                                      |                                                               |
| permalink       | 覆盖文章的永久链接. 永久链接应该以 `/` 或 `.html` 结尾                                                    | null                                                          |
| excerpt         | 纯文本的页面摘要。 使用 [该插件](https://hexo.io/zh-cn/docs/tag-plugins) 来格式化文本                     |                                                               |
| disableNunjucks | 启用时禁用 Nunjucks 标签` {{ }}`/`{% %}` 和 [标签插件](https://hexo.io/zh-cn/docs/tag-plugins) 的渲染功能 | FALSE                                                         |
| lang            | 设置语言以覆盖[自动检测](https://hexo.io/zh-cn/docs/internationalization)                                 | 继承自 `_config.yml`                                          |
| published       | 文章是否发布                                                                                              | 对于 `_posts` 下的文章为 true，对于 `_draft` 下的文章为 false |

## 标签插件

> https://hexo.io/zh-cn/docs/tag-plugins

### 引用块

在文章中插入引言，可包含作者、来源和标题。

别名： `quote`

```
{% blockquote [author[, source]] [link] [source_link_title] %}
content
{% endblockquote %}
```

例如：

```
{% blockquote @DevDocs https://twitter.com/devdocs/status/356095192085962752 %}
NEW: DevDocs now comes with syntax highlighting. http://devdocs.io
{% endblockquote %}
```

显示效果：

{% blockquote @DevDocs https://twitter.com/devdocs/status/356095192085962752 %}
NEW: DevDocs now comes with syntax highlighting. http://devdocs.io
{% endblockquote %}

### 文章摘要和截断

在文章中使用 &lt;!-- more --&gt;，那么 &lt;!-- more --&gt; 之前的文字将会被视为摘要。首页中将只出现这部分文字，同时这部分文字也会出现在正文之中。

### 代码块

可以将代码片段添加到您的帖子的有用功能。

别名： code

```
{% codeblock [title] [lang:language] [url] [link text] [additional options] %}
code snippet
{% endcodeblock %}
```

以 `option:value` 的格式指定额外选项，例如：`line_number:false first_line:5`。

| 额外选项       | 描述                                                                                                         | 默认值 |
| -------------- | ------------------------------------------------------------------------------------------------------------ | ------ |
| line_number    | 显示行号                                                                                                     | true   |
| line_threshold | 只有代码块的行数超过该阈值，才显示行数                                                                       | 0      |
| highlight      | 启用代码高亮                                                                                                 | true   |
| first_line     | 指定第一个行号                                                                                               | 1      |
| mark           | 突出显示特定的行，每个值用逗号分隔。 使用破折号指定数字范围例如：`mark:1,4-7,10` 将标记第 1、4 至 7 和 10 行 |        |
| wrap           | 用 &lt;table&gt; 包裹代码块                                                                                  | true   |

普通的代码块：

```
{% codeblock %}
alert('Hello World!');
{% endcodeblock %}
```

{% codeblock %}
alert('Hello World!');
{% endcodeblock %}

指定语言：

```
{% codeblock lang:objc %}
[rectangle setX: 10 y: 10 width: 20 height: 20];
{% endcodeblock %}
```

{% codeblock lang:objc %}
[rectangle setX: 10 y: 10 width: 20 height: 20];
{% endcodeblock %}

附加说明和网址：

```
{% codeblock lang:js Array.map https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map Array.prototype.map() - JavaScript | MDN %}
const array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]
{% endcodeblock %}
```

{% codeblock lang:js Array.map https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map Array.prototype.map() - JavaScript | MDN %}
const array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x \* 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]
{% endcodeblock %}

### 反引号代码块

另一种形式的代码块，不同的是它使用三个反引号来包裹。

````
``` [language] [title] [url] [link text] code snippet ```
````

### iframe

在文章中插入 iframe。

```
{% iframe url [width] [height] %}
```

### 链接

在文章中插入链接，并自动给外部链接添加 `target="_blank"` 属性。

```
{% link text url [external] [title] %}
```

### 资源的引用

> 资源（Asset）代表 `source` 文件夹中除了文章以外的所有文件，例如图片、CSS、JS 文件等。比方说，如果你的 Hexo 项目中只有少量图片，那最简单的方法就是将它们放在 `source/images` 文件夹中。然后通过类似于 `![](/images/image.jpg)` 的方法访问它们。

将 `config.yml` 文件中的 `post_asset_folder` 选项设为 `true` 来打开，这样 Hexo 将会在你每一次通过` hexo new [layout] <title>` 命令创建新文章时自动创建一个与文章同名的文件夹，当然也可以手动创建。

{% codeblock _config.yml lang:yml %}
post_asset_folder: true
{% endcodeblock %}

通过常规的 `markdown` 语法和相对路径来引用图片和其它资源可能会导致它们在存档页或者主页上显示不正确。使用以下 `Hexo` 标签来加载资源：

```
{% asset_path slug %}
{% asset_img slug [title] %}
{% asset_link slug [title] %}
```

例如：`{% asset_img Pikachu.jpg Pikachu %}`

{% asset_img Pikachu.jpg Pikachu %}

# 部署

1. 安装 hexo-deployer-git
2. 在 `_config.yml` 中添加以下配置（如果配置已经存在，请将其替换为如下）:
    ```yml
    deploy:
    type: git
    repo: https://github.com/<username>/<project>
    # example, https://github.com/hexojs/hexojs.github.io
    branch: gh-pages
    ```
3. 执行 `hexo clean && hexo deploy`

# 主题

## NexT

> https://theme-next.js.org/docs/getting-started/

### 标签插件

> https://theme-next.js.org/docs/tag-plugins/