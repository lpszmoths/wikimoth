---
title: CSS
summary: CSS tricks and code snippets
---

# CSS

## Importing a local or relative font in @font-face

```
@font-face {
    font-family: 'My Font';
    src: local("My Font"), url("./fonts-my-fonts.ttf") format("truetype");
}
```
