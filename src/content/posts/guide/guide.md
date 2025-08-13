---
title: Guide for First Posting
published: 2025-08-13
author: Tuple
description: 'The guide about Markdown and Github'
image: 'https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F26053538586482B414'
tags: ["Blogging", "Customization"]
category: 'Guides'
draft: false
---

## 게시물의 Front-matter

```yaml
---
title: My First Blog Post
published: 2023-09-09
description: This is the first post of my new Astro blog.
image: ./cover.jpg
tags: [Foo, Bar]
category: Front-end
draft: false
---
```

| Attribute     | Description                                                                                                                                                                                                 |
|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `title`       | 게시물의 제목                                                                                                                                                                                      |
| `published`   | 게시글 발행 날짜                                                                                                                                                                            |
| `description` | 인덱스 페이지에 보여지는 짧은 설명                                                                                                                                                   |
| `image`       | 게시글의 커버 이미지의 경로<br/>1. `http://` 또는 `https://`로 시작하는 경우: 웹 이미지 사용<br/>2. `/`로 시작하는 경우: `public` 디렉토리의 이미지 사용<br/>3. 접두어가 없는 경우: MD 파일로부터 상대 경로 |
| `tags`        | 게시물의 태그                                                                                                                                                                                       |
| `category`    | 게시물의 카테고리                                                                                                                                                                                   |
| `draft`        | 게시글 작성 중인 경우, 보여지지 않으려면                                                                                                                                                    |

## 게시물 파일의 위치



게시물의 파일은 `src/content/posts/` 디렉토리에 위치한다. 원한다면 효율적인 게시물과 자원의 관리를 위해서 서브 디렉토리를 만들 수 있다.

```
src/content/posts/
├── post-1.md
└── post-2/
    ├── cover.png
    └── index.md
```

# h1 헤더
## h2 헤더
### h3 헤더

단락은 빈 줄로 구분됩니다. 한 번 더 줄바꿈을 넣고 싶다면 `<br>` 태그를 넣으세요.

2단락. _Italic_, **bold**, 그리고 `monocpace`는 당연히 사용 가능합니다.

목록화도 다음과 같이 가능합니다:

- 이것
- 저것
- 나머지 것

> 인용구입니다.<br>
> 이렇게 작성됩니다.
> > 더 인용할 수 있습니다.<br>
> > 너가 원한다면

1. 넘버 리스트도
2. 당연히
3. 이렇게
5. 숫자는 정렬됨.

코드는 백틱 3개로 감싸 표현합니다.

```
print("Hello, world!")
```

언어별 구문 강조도 됩니다.

```py
import time
for i in range(10):
    time.sleep(0.5)
    print(i)
```

여기 링크가 있습니다. [a website](http://foo.bar) 여기 각주도 있습니다. [^1].

[^1]: 각주는 이렇게 작성합니다.

사이에 줄을 넣을 수도 있습니다.

---

인라인 수식은 옆과 같이 작성됩니다: $\omega = d\phi / dt$.<br>
두 줄 이상의 경우:

$$I = \int \rho R^{2} dV$$

$$
\begin{equation*}
\pi
=3.1415926535
 \;8979323846\;2643383279\;5028841971\;6939937510\;5820974944
 \;5923078164\;0628620899\;8628034825\;3421170679\;\ldots
\end{equation*}
$$

그리고 특수 기호들을 문자 그대로 사용할 수 있습니다: \`foo\`, \*bar\*, etc.

## YouTube

유튜브 영상의 경우 아래 양식을 사용하세요.

<iframe width="100%" height="468" src="https://www.youtube.com/embed/ICXB0Vs_lTQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

`url`에 보이다시피 `/embed/~` 꼴로 작성하여야 합니다.

### Editor & Terminal 프레임

#### 코드 에디터 프레임

```js title="my-test-file.js"
console.log('Title attribute example')
```

```html
<!-- src/content/index.html -->
<div>File name comment example</div>
```

#### 터미널 프레임

```bash
echo "This terminal frame has no title"
```

```powershell title="PowerShell terminal example"
Write-Output "This one has a title!"
```

#### 프레임 타입 덮어쓰기

```sh frame="none"
echo "Look ma, no frame!"
```

```ps frame="code" title="PowerShell Profile.ps1"
# Without overriding, this would be a terminal frame
function Watch-Tail { Get-Content -Tail 20 -Wait $args }
New-Alias tail Watch-Tail
```

## GitHub Repository Cards
깃허브 API로 덩적 깃허브 레포 카드를 작성할 수도 있습니다.

::github{repo="TRUST-DIMIGO/trust-dimigo.github.io"}

`::github{repo="<owner>/<repo>"}`로 만듭니다.

```markdown
::github{repo="TRUST-DIMIGO/trust-dimigo.github.io"}
```

## Admonitions

콜아웃: `note` `tip` `important` `warning` `caution`

:::note
노트
:::

:::tip
팁
:::

:::important
중요!
:::

:::warning
워닝~
:::

:::caution
경고.
:::

### Basic Syntax

```markdown
:::note
Highlights information that users should take into account, even when skimming.
:::

:::tip
Optional information to help a user be more successful.
:::
```

### Custom Titles

커스텀화될 수 있음.

:::note[MY CUSTOM TITLE]
커스텀 타이틀
:::

```markdown
:::note[MY CUSTOM TITLE]
커스텀 타이틀2
:::
```