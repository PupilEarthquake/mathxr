---
title: TEST ARTICLE
---

## 1. Introduction

This article is to test the mathematical article's compilation, and other functions. Now, allow me to quote:

> The world is material; matter is in motion; motion follows laws; and these laws can be understood.

## 2. Math

__Prop__ Given a functor {{< katex >}}\alpha: I \to Set{{< /katex >}}, let {{< katex >}} X = \bigsqcup_i \alpha(i) {{< /katex >}}, define:

{{< katex display=true >}}
a \to b \Leftrightarrow (a, b) \in R \Leftrightarrow b = \alpha(\sigma)(a)
{{< /katex >}}

_Proof_

The following diagram says it all:

![fig1](fig1.png)

### 2.1. What about a title containing {{< katex >}}\pi{{< /katex >}}

{{< katex >}} \alpha {{< /katex >}} is an ordinal if it is a transitive set and is well-ordered with respect to {{< katex >}}\in{{< /katex >}}.

## 3. Functions

### 3.1. Download link

[article](article1.pdf)

### 3.2. Columns

```html
{{%/* columns ratio="1:2" */%}} <!-- begin columns block -->

## x1 Column
Lorem markdownum insigne...

<---> <!-- magic separator, between columns -->

## x2 Column
Lorem markdownum insigne...

{{%/* /columns */%}}
```

{{% columns ratio="1:2" %}}
### x1 Column
Lorem markdownum insigne. Olympo signis Delphis! Retexi Nereius nova develat
stringit, frustra Saturnius uteroque inter! Oculis non ritibus Telethusa
protulit, sed sed aere valvis inhaesuro Pallas animam: qui _quid_, ignes.
Miseratus fonte Ditis conubia.

<--->

### x2 Column
Lorem markdownum insigne. Olympo signis Delphis! Retexi Nereius nova develat
stringit, frustra Saturnius uteroque inter!

Lorem markdownum insigne. Olympo signis Delphis! Retexi Nereius nova develat
stringit, frustra Saturnius uteroque inter! Oculis non ritibus Telethusa
protulit, sed sed aere valvis inhaesuro Pallas animam: qui _quid_, ignes.
Miseratus fonte Ditis conubia.

{{% /columns %}}

## 3.3. Fold

```tpl
{{%/* details "Title" [open] */%}}
## Markdown content
Lorem markdownum insigne...
{{%/* /details */%}}
```
{{% details "Title" open %}}
### Markdown content
Lorem markdownum insigne...
{{% /details %}}

## 3.4. Hints

```tpl
{{%/* hint [info|warning|danger] */%}}
**Markdown content**  
Lorem markdownum insigne. Olympo signis Delphis! Retexi Nereius nova develat
stringit, frustra Saturnius uteroque inter! Oculis non ritibus Telethusa
{{%/* /hint */%}}
```

{{% hint info %}}
**Markdown content** 
Lorem markdownum insigne. Olympo signis Delphis! Retexi Nereius nova develat
stringit, frustra Saturnius uteroque inter! Oculis non ritibus Telethusa
{{% /hint %}}
