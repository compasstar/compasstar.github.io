---
layout: post
title:  "[JS] 4.JS URL 복사하기"
subtitle:   "JS URL 복사"
categories: JS
tags: JS
comments: true
date: 2021-07-22 00:16:53
---

현재 사이트의 URL을 복사하는 버튼을 만들어보겠습니다.<br><br>
3개 파트로 분류할 수 있습니다. <br><strong>버튼을 가져오고/url을 복사하는 함수/버튼을 누르면 함수를 실행시킵니다.</strong>
<br><br>

```
const copyBtn = document.querySelector('.copy_btn');
```
버튼은 이미 만들었다고 가정하고, `'.copy_btn'`이라는 버튼을 가져오겠습니다.<br><br>


```
function copyUrl(){
    let tmp = document.createElement('input');
    let url = window.location.href; // 현재 사이트의 url

    document.body.appendChild(tmp);
    tmp.value = url;
    tmp.select();
    document.execCommand("copy");
    document.body.removeChild(tmp);

    alert("URL이 복사되었습니다"); // 알림
}
```

`let tmp = document.createElement('input')`
> 임시로 `input`이라는 엘리먼트를 만들어 `tmp`에 저장합니다.

`document.body.appendChild(tmp)`
> 임시로 만들어진 `tmp`를 `<body>`안에 넣어줍니다.

`tmp.value = url;`
> `tmp`에 url을 저장해줍니다.

`tmp.select()`
> `tmp`에는 url이 저장되어 있으므로, url이 선택됩니다.

`document.execCommand("copy");`
> 선택된 url을 복사합니다.

`document.body.removeChild(tmp);`
> 임시로 만들었던 `tmp`를 지워줍니다.

<br><br>

```
copyBtn.addEventListener('click', copyUrl);
```
버튼을 클릭하면 위의 함수를 실행시키도록 이벤트를 만듭니다.