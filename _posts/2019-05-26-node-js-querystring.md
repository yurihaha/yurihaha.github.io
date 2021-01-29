---
layout: post
title: "[node js] 쿼리스트링을 이용한 페이지출력"
comments: true
date: 2019-05-26 20:00:00 +0900
categories: 프론트엔드챕터
tag: [node js, querystring]
---

### 01. 쿼리스트링(querystring)이란?

예시) http://a.com/topic?id=1 <br/>
물음표 뒤에 나타나는 `id=1`을 ‘쿼리스트링’ 이라고 부른다.<br/>
쿼리스트링(querystring)은 경로(Path)를 통해서 정보를 다르게 보여 줄 수 있다.
위 예시는 topic 이라는 라우트를 가지고 있고, ?id=1 이라는 값을 전달하고 있기 때문에 이를 화면에 표현해 주면 된다. <br/>

- URL이란: `http://a.com/topic?id=1`
- Path란: http://a.com`/topic`?id=1
- Querystring 이란: http://a.com/topic?`id=1 `

### 02. 쿼리스트링을 이용한 페이지 출력

{% raw %}

```javascript
var express = require("express");
var app = express();
app.locals.pretty = true;
app.set("view engine", "jade");
app.set("views", "./views");
app.use(express.static("public"));
app.get("/topic", function (req, res) {
  // 다른정보를 배열에 담아둔다.
  var topics = [
    // 실제 프로그래밍 할때 이부분을 파일, 데이터 베이스로 교체한다.
    "JavaScript is...",
    "Node.js is ...",
    "Express is ..."
  ];

  var output = `
<a href="/topic?id=0">JavaScrpit</a><br>
<a href="/topic?id=1">Node.js</a><br>
<a href="/topic?id=2">Express</a><br><br>
${
  topics[req.query.id]
} //topics에 저장되는 값을 출력하게 된다. (Query string 방식)
`;
  res.send(output);
});
```

{% endraw %}

### 03. 쿼리스트링 없이 시멘틱한 URl 만들기

`:id`를 사용해서 적용가능
{% raw %}

```javascript
app.get("/topic/:id", function (req, res) {
  // :id를 사용해서 적용가능
  var topics = ["JavaScript is...", "Node.js is ...", "Express is ..."];

  var output = `
<a href="/topic?id=0">JavaScrpit</a><br>
<a href="/topic?id=1">Node.js</a><br>
<a href="/topic?id=2">Express</a><br><br>

${
  topics[req.params.id]
} // 시멘틱은 Params를 통해 나타낼수있다. (Semantic URL 방식)
`;
  res.send(output);
});
```

{% endraw %}

#### Uncleaned URL과 Clean URL(=시멘틱)의 차이

{% raw %}
| <center>Uncleaned URL</center> | <center>Clean URL</center> |
|---|:---:|
| <center>http://example.com/index.php?page=name</center>| http://example.com/name |
| <center>http://example.com/about.html</center>| http://example.com/about |
| <center>http://example.com/kb/index.php?cat=8&id=41</center>| http://example.com/kb/8/41 |
{% endraw %}

###### 출처: <https://en.wikipedia.org/wiki/Clean_URL>

- 쿼리스트링 여러개일때 전달방법

  - 예시) https://www.a.com/topic?id=1&name=yurihaha <br>
    시작 값과 값을 구분하는 구분자 `&`를 써서 여러개를 전달한다.

  {% raw %}

  ```javascript
  app.get("/topic/:id/:mode", function (req, res) {
    res.send(req.params.id + "," + req.params.mode);
  });
  ```

  {% endraw %}

### 04. 결과

아래 내용들을 검색창에 치면 다르게 화면이 배열에 담은 화면으로 보여질것이다.

```
1) https://www.a.com/topic?id=0
2) https://www.a.com/topic?id=1
3) https://www.a.com/topic?id=2
```
