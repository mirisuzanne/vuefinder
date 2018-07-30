---
public: true
title: 'Agile Design Systems'
subtitle: 'in Vue'
view: 'grid'
author:
  name: 'Miriam Suzanne'
  url: 'http://oddbird.net/authors/miriam/'
org:
  name: 'OddBird'
  url: 'http://oddbird.net/'
---

Style Guides & Pattern Libraries
are great tools for documenting
the relationships between code and design,
but beautiful docs are only half the battle.

<!-- more -->

We don’t all have dedicated teams and budgets
to build a centralized system.
How can we incorporate patterns into our code,
using templates and pre-processors to iterate and automate
living design systems in an agile and integrated process?

<!-- slide -->

## Design **Systems**
**Style** Guides + **Tool**kits + **Pattern** Libraries + **???**

<!-- slide -->

---
alt: 'OddBird siblings (Jonny, Carl, and Miriam) in 1994'
style:
  'background-image': "url('https://dl.dropbox.com/s/98zl3nxde444otp/oddbird-w-logo.jpg')"
  'background-size': 'contain'
  'background-position': 'center'
---

<!-- slide -->

![](https://dl.dropbox.com/s/76e55964w8nvx3y/oddbird.png)

## [OddBird](http://oddbird.net)
est. **2008**

<!-- slide -->

---
alt: Lonely Planet Design System
style:
  'background-image': "url('https://dl.dropbox.com/s/3oyfw1kdtz2qzih/lonely-planet-colors.jpg')"
  'background-size': 'cover'
  'background-position': 'top'
---

<!-- slide -->

## Code Patterns **Add Meaning**

<div class="code-caption">
  scss - Showing your math is good…
</div>

```scss
.grid-span {
  width: ((3*4em) + (2*1em)) / ((12*4em) + (11*1em)) * 100%; // 23.7288136%
  margin-right: 1em / ((12*4em) + (11*1em)) * 100%; // 01.6949153%
  padding-left: ((1*4em) + (1*1em)) / ((12*4em) + (11*1em)); // 08.4745763%
}
```

<div class="code-caption">
  scss - Making it readable is even better…
</div>

```scss
.grid-span {
  width: span(3);
  margin-right: gutter();
  padding-left: span(1 wide);
}
```