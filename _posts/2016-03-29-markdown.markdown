---
layout: post
title: "Markdown Gramma"
subtitle: "A brief introduction about Markdown Grammar. "
date: 2016-03-29
author: Benjamin
category: coding
tags: code markdown github
finished: true
---

## Heading

Heading is really simple in Markdown, you can use `#` or `=` or `-`. 

Like this:

`# H1. Heading`

# H1. Heading

`## H2. Heading`

## H2. Heading

`### H3. Heading`

### H3. Heading

`#### H4. Heading`

#### H4. Heading

`##### H5. Heading`

##### H5. Heading

`###### H6. Heading`

###### H6. Heading

And like this: 

{% highlight md %}
Heading
======
{% endhighlight %}

Heading
======

{% highlight md %}
Heading
-------
{% endhighlight %}

Heading
----------

See? Really easy. 

## Font

There are three kinds of font in Markdown.

### Italic：

`*Italic*`

*Italic*

`_Italic_`

_Italic_

### Bold：

`**Bold**`

**Bold**

`__Bold__`

__Bold__

### Italic & Bold：

`***Italic & Bold***`

***Italic & Bold***

`___Italic & Bold___`

___Italic & Bold___

You can also do this:

`**Markdown is _fun_**`

**Markdown is _fun_**


## List

### Ordered list:

`1. 2. 3. `

1. First
2. Second
3. Third

### Unordered list: 

There are three ways to make an unordered list:

`* AAA`

* AAA
* BBB
* CCC

`- AAA`

- AAA
- BBB
- CCC

`+ AAA`

+ AAA
+ BBB
+ CCC

## Block quote

`> War is Peace`

`> Freedom is Slavery`

`> Ignorance is Strength`

> War is Peace

> Freedom is Slavery

> Ignorance is Strength

You can also do this:

`> * War is Peace`

`> * Freedom is Slavery`

`> * Ignorance is Stength`


> * War is Peace

> * Freedom is Slavery

> * Ignorance is Stength

## Link

### Simple link

`<http://itisbenjamin.github.io>`

<http://itisbenjamin.github.io>

You can also do this when you insert an email address.

### Link

You can add your link just behind your words: 

`[Ben](www.itisbenjamin.github.io)`

[Ben](www.itisbenjamin.github.io)

And you can also do it like this: 

`[about this link][1]`

Then put this line at anywhere you want in your post:

`[1]: link address`

### Link description

Add the link description behind the link address like this: 

`[Ben](www.itisbenjamin.github.io "Ben")`

[Ben](www.itisbenjamin.github.io "Ben")

## Image

`![Codes](/img/code.png)`

![Codes](/img/code.png)

How to write the images' descriptions are the same way as how you do it in links: 

`![Codes](/img/code.png "Codes")`

![Codes](/img/code.png "Codes")

## Code

You can use <code>``</code> to show your codes:

`` `.default` ``

`.default`

If you wanna show a piece of codes, use 4 spaces or 1 tab.

{% highlight html %}
<div class="post-header-container>
  <div class="scrim {% if page.cover %}has-cover{% endif %}">
    <header class="post-header">
        <h1 class="title">{{ page.title }}</h1>
        <p class="info">by <strong>{{ page.author }}</strong></p>
    </header>
    </div>
</div>
{% endhighlight %}

## Others

### Breaker

`---`

---

`***`

***

`- - - -`

- - - -

They all show a breaker.

## Footnote

`Something needs a footnote[^1].`

`[^1]: This is a footnote.`

Something needs a footnote[^1].

[^1]: This is a footnote.

Then this footnote will show at the end of this post.

## Delete

`~~There is no tree waiting for me.~~`

<del>There is no tree waiting for me.</del>

## Table

### A simple way

`A     | B     | C     | D `

`----- | ----- | ----- | -----`

`a     | b     | c     | d`


A     | B     | C     | D 
----- | ----- | ----- | -----
a     | b     | c     | d

### Make words at left, center or right

`left      | center       | center       | right`
 
`:-------- | :----------: | :----------: | -----:`

`a         | b            | c            | d`


left      | center       | center       | right 
:-------- | :----------: | :----------: | -----:
a         | b            | c            | d


