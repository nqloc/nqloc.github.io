---
layout: wiki
title: Markdown cheatsheet
categories: Markdown cheatsheet
description: Markdown cheatsheet
keywords: Markdown cheatsheet
mermaid: true
sequence: true
flow: true
mathjax: true
active: true
---

**Table Of Contents**

* TOC
{:toc}

### Hyperlinks

```
[ClickMe](https://nqloc.github.io)

<https://nqloc.github.io>
```

[ClickMe](https://nqloc.github.io)  

<https://nqloc.github.io>

### List

```
1. Sequence entry 1

2. Sequence entry 2

3. Sequence entry 3 3
```

1. Sequence entry 1

2. Sequence entry 2

3. Sequence entry 3

```
* Unordered entry 1

* Unordered entry 2

* Unordered entry 3
```

* Unordered entry 1

* Unordered entry 2

* Unordered entry 3

```
- [x] Task list 1
- [ ] Task list 2
```

- [x] Task list 1
- [ ] Task list 2

### Emphasize

```
~~Strikethrough~~

**With black**

*Italics*
```

~~Strikethrough~~

**With black**

*Italics*

### Heading

| Markdown | HTML | Rendered Output |
| ------- | :------ | :-----: |
| ```# Heading level 1``` | ```<h1>Heading level 1</h1>``` | <h1>Heading level 1</h1> |
| ```## Heading level 2``` | ```<h2>Heading level 2</h2>``` | <h2>Heading level 2</h2> |
| ```### Heading level 3``` | ```<h3>Heading level 3</h3>``` | <h3>Heading level 3</h3> |
| ```#### Heading level 4``` | ```<h4>Heading level 4</h4>``` | <h4>Heading level 4</h4> |
| ```##### Heading level 5``` | ```<h5>Heading level 5</h5>``` | <h5>Heading level 5</h5> |
| ```###### Heading level 6``` | ```<h6>Heading level 6</h6>``` | <h6>Heading level 6</h6> |

### Table

```
| HEADER1 | HEADER2 | HEADER3 | HEADER4 |
| ------- | :------ | :-----: | ------: |
| content | content | content | content |
```

| HEADER1 | HEADER2 | HEADER3 | HEADER4 |
| ------- | :------ | :-----: | ------: |
| content | content | content | content |

1. :----- indicates left alignment
2. :----: indicates medium alignment
3. -----: indicates right alignment

### Code block

```python
print 'Hello, World!'
```

1. list item1

2. list item2

   ```python
   print 'hello'
   ```
   
### Blockquotes

```
> Dorothy followed her through many of the beautiful rooms in her castle.
```

> Dorothy followed her through many of the beautiful rooms in her castle.

```
> Dorothy followed her through many of the beautiful rooms in her castle.
>
> The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.
```

> Dorothy followed her through many of the beautiful rooms in her castle.
>
> The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.

```
> Dorothy followed her through many of the beautiful rooms in her castle.
>
>> The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.
```

> Dorothy followed her through many of the beautiful rooms in her castle.
>
>> The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.

### Image

```
![favicon](/favicon.ico)
```

![favicon](/favicon.ico)

### Anchor point

```
* [Table of Contents](#catalog)
```

* [Table of Contents](#catalog)

### Emoji

```
:camel:
:blush:
:smile:
```

:camel:
:blush:
:smile:

### Footnotes

```
This is a text with footnote[^1].
```

This is a text with footnote[^1].

### mermaid

```
<div class="mermaid">
sequenceDiagram
    Alice-->>John: Hello John, how are you?
    John-->>Alice: Great!
</div>

```

<div class="mermaid">
sequenceDiagram
    Alice-->>John: Hello John, how are you?
    John-->>Alice: Great!
</div>

### Sequence


```sequence
Andrew->VietNam: Says Hello
Note right of VietNam: China thinks\nabout it
VietNam-->Andrew: How are you?
Andrew->>VietNam: I am good thanks!
```

### Flowchart


```flow
st=>start: Start
e=>end
op1=>operation: My Operation
sub1=>subroutine: My Subroutine
cond=>condition: Yes
or No?
io=>inputoutput: catch something...

st->op1->cond
cond(yes)->io->e
cond(no)->sub1(right)->op1
```

### Mathjax

```
When $$(a \ne 0)$$, there are two solutions to $$(ax^2 + bx + c = 0)$$ and they are

$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$

[^1]: Here is the footnote 1 definition.
```

When $$(a \ne 0)$$, there are two solutions to $$(ax^2 + bx + c = 0)$$ and they are

$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$

[^1]: Here is the footnote 1 definition.
