---
layout: post
title: "javascript toFixed() 0 없애기 "
date: 2021-03-03 20:00:22 +0900
categories: chapter
# image: assets/images/11.jpg
toc: true
comments: true
tag: [javascript, tofixed, parseFloat]
---

## 자바스크립트에서 숫자를 정확한 자릿수로 표현하기 위해 toFixed()를 사용한다.

- `toFixed()` 는 지정한 자릿수보다 짧은 수일 때 뒤를 `0`으로 채우는데, 경우에 따라서 `0`을 제거할 경우가 생긴다.
- `1` 이나 `1.1` 을 `toFixed(2)`로 처리를 하면 `1.00`, `1.10` 으로 지정한 자릿수까지 0이 붙게 된다.

## 자바스크립트에서 숫자를 정확한 자릿수로 표현하기 위해 toFixed()를 사용한다.

1. parseFloat() 사용

```javascript
parseFloat(number.toFixed(2));
```

2. 정규식 사용

```javascript
number.toFixed(2).replace(/(0+$)/, "");
```
