---
title: first post
date: 2023-09-07 23:31
categories: [test]
tags: [test]
author: hachian
math: true
---

この投稿では、マークダウンがどのようにレンダリングされるのかをテストします。通常のマークダウン記法に加え、JekyllテーマのChirpy固有の記法も含みます。

# h1h1h1

Lorem ipsum dolor sit, amet consectetur adipisicing elit.

## h2h2h2

### h3h3h3

#### h4h4h4h4

## インライン記法

- **strong**、**ボールド**
- *em*、*イタリック*
- ~~strike~~、~~打消し線~~
- ^^highlight^^、^^ハイライト^^ (ハイライトはできない)
- $$E = mc^2$$
- `inline code`
- [link](https://github.com/hachian/chirpy-blog)

## 画像

![Alt text](/assets/img/2023-09-07-first-post/avatar.webp)

![Alt text](/assets/img/2023-09-07-first-post/draw.svg)

## リスト

- aaa
- bbb
    - ccc
    - ddd
- eee

## 番号付きリスト

1. 111
1. 222
    1. 333
    1. 444
1. 555

## コードブロック

```python
from pathlib import Path

p = Path(rf"{123}456.png")
print(f"p: {p}")  # this code means nothing
```

```bash
jekyll build --future
```

> Example line for prompt.
{: .prompt-tip }

> Example line for prompt.
{: .prompt-info }

> Example line for prompt.
{: .prompt-warning }

> Example line for prompt.
{: .prompt-danger }
