---
layout: post
title:  "JavaScript code collection"
categories: JavaScript code-collection
tags: 代码集锦 JavaScript
author: 若水三千
---

* content
{:toc}

浮点数取整
```js
const num = 214.56
num >> 0;
~~num;
num | 0;

```
 


Anagrams of string

```js
const anagrams = str => {
    if(str.length <= 2) {
        return str.length === 2 ? [str, str[1] + str[0]]:[str];
    }
    return str.split("").reduce((acc, letter, i) => acc.concat(anagrams(str.slice(0, i) + str.slice(i + 1)).map(val =>letter + val)), []);
}
```

anagrams('abc') ==> 

数组平均数

```js
const average = arr => arr.reduce((acc, val) => acc + val, 0) / arr.length);

``` 

大写每个单词首字母
```js
const capitalizeEveryWord = str => str.replace(/\b[a-z]/g, char => char.toUpperCase());

```

首字母大写
```js
const capitalize = (str, lowerRest = false) => str.slice(0, 1).toUpperCase() + (lowerRest ? str.slice(1).toLowerCase() : str.slice(1));
 
```

```js
```


附录：  
[1] 原文请参考：https://github.com/Chalarangele/30-seconds-of-code#anagrams-of-string-with-duplicates


