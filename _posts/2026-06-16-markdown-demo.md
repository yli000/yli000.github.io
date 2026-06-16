---
layout: post
title: 排版效果示例
---

这篇文章把常用的 Markdown 排版效果都放在一起，方便对照着写。源文件在
`_posts/2026-06-16-markdown-demo.md`，照着复制就行。

## 文字强调

可以 **加粗**、*斜体*、***又粗又斜***，也可以 ~~删除线~~。

## 引用

> 引用块用来放别人的话或者想强调的段落。
>
> 引用里也能 **加粗**、放 `代码`，甚至嵌套：
>
> > 这是引用里的引用。

## 代码

行内代码写成 `print("hello")` 这样。整段代码用三个反引号包起来，并标上语言就会有高亮：

```python
def fib(n):
    a, b = 0, 1
    for _ in range(n):
        a, b = b, a + b
    return a

print([fib(i) for i in range(10)])
```

```bash
bundle exec jekyll serve --livereload
```

## 列表

无序列表：

- 第一项
- 第二项
  - 嵌套子项
  - 子项也能放 `代码` 或 **加粗**
- 第三项

有序列表：

1. 先做这个
2. 再做那个
3. 最后收尾

任务清单：

- [x] 已完成的事
- [ ] 还没做的事

## 链接与分割线

这是一个[链接](https://daviddarnes.com/garth/)，指向本博客用的 Garth 主题。

下面是一条分割线：

---

## 表格

| 效果 | 写法 | 默认支持 |
| --- | --- | :---: |
| 加粗 | `**text**` | ✅ |
| 引用 | `> text` | ✅ |
| 代码块 | ` ```lang ` | ✅ |
| 折叠 | `<details>` | ✅（HTML） |

## 折叠 / 收起（重点）

Obsidian 那种折叠块用 HTML 的 `<details>` 标签实现，点标题行展开或收起。
关键是要写 `markdown="1"`，否则里面的 Markdown 不会被解析。

<details markdown="1">
<summary>点我展开：里面可以放任意 Markdown</summary>

收起的内容里照样能用各种格式：

- 列表
- **加粗** 和 `行内代码`
- 引用：

> 折叠块里的引用也正常。

```python
print("折叠块里的代码也有高亮")
```

</details>

也可以把折叠块当成「注释 / 补充说明」，默认收起、需要时再看：

<details markdown="1">
<summary>补充说明（默认收起）</summary>

这里放一些不想占正文篇幅、但又舍不得删的细节。

</details>

折叠块还能嵌套：

<details markdown="1">
<summary>外层</summary>

外层内容。

<details markdown="1">
<summary>内层</summary>

内层内容。

</details>

</details>
