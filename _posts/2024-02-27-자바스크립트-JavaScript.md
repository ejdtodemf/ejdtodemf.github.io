---
title : "JavaScript"
excerpt : "JavaScript"
toc : true
toc_sticky : true
toc_label : "JavaScript"
categories:
- 자바스크립트
tags:
- [자바스크립트]
last_modified_at: 2024-02-27T08:00:00-10:00:00
---

# 날짜 : 2024-02-27 17:04

# 태그 : #자바스크립트 
---

# 내용

## 개요
- app.js가 있기 때문에 자바스크립트를 통해 HTML의 내용을 가져올 수 있습니다.

#### index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css">
    <title>Momentum</title>
</head>
<body>
    <div class="hello">
        <h1>Grab me!</h1>
    </div>  
    <script src="app.js"></script>
</body>
</html>
```

#### app.js

``` js
const title = document.querySelector(".hello h1");//아이디는 #hello
// hello라는 클래스 내부의 h1을 가지고 와줘
  
![image](../../assets/images/Pasted%20image%2020240227171212.png)
//사진과 같이 가져와짐 (console.dir(title))
  
![image](../../assets/images/Pasted%20image%2020240227171446.png)
//console.dir(title) objects 형식으로 가져와짐
// querySelector 가 제일 좋음

const title = document.querySelector(".hello:first-child h1");
// class hello 를 가진 div 내부의 first-child 인 h1을 찾아와줘
// css selector를 전달할 수 있음
const title = document.getElementById
const title = document.getElementByClassName
const title = document.getElementByTagName
// class or id or tagname을 가져오는 것
```

#### 중요한 점!
- app.js를 import 하지 않았으면, document는 존재할 수 없음
- document가 HTML이 app.js를 load하기 때문에 존재하는 것
- 그 다음에 browser가 우리가 document에 접근할 수 있게 해줌

#### Events
- 클릭, 마우스 스크롤, 입력, 엔터 등
- 모든 event들을 JavaScript는 listen할 수 있음
- on으로 시작하는 기능들은 이벤트
- console.dir를 사용하여 나오는 기능들 중 on으로 시작하는 이벤트들은 다 addEventListener(param1, param2) param1에 작성할 수 있음

``` js
const title = document.querySelector("div.hello:first-chile h1);
function handleTitleClick(){
	console.log("Title was Clicked);
}//2. handleTitleClick function 동작
				
//handleTitleClick();//곧바로 실행이 아닌

title.addEventListener("click", handleTitleClick);
//addEventListener(event, 클릭 시 실행할 기능)
//1. click event를 listen 하고, 이 click event가 발생
// 유저가 title을 click 할 경우에 JavaScript가 실행 버튼을 대신 눌러줌

title.onClick = handleTitleClick ;
// 위 방법처럼 실행할 수도 있음 
// 위 방법을 더 선호함
```

#### window Element

```js
function handleWindowResize(){
    document.body.style.backgroundColor = "yellow";
}
//태그 값에 대한 이벤트가 아닌 윈도우 엘리먼트 이벤트
window.addEventListener("resize", handleWindowResize);
```

####정리
- step1. element를 찾아라.

```js
const h1 = document.querySelector(".hello h1");
```

- step2. event를 listen 해라

```js
h1.addEventListener("click",handleTitleClick);
```

- step3. 그 이벤트에 기능을 추가해라

```js
function handleTitleClick(){
    const currentColor = h1.style.color ;
    let newColor ;

    if(currentColor == "lightpink") {
        newColor = "tomato";
    }else{
        newColor = "lightpink";
    }
    h1.style.color = newColor;
}
```

###### **스타일 변경 코드는 js 파일에서 연습했지만, js 가 아닌 html 파일 즉, css 파일에서 수정 및 추가하는 것을 선호** 

###### **animation에 적합한 도구는 JavaScript**
---

# 연결문서 
- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML)

# 참고 사이트
- https://developer.mozilla.org/en-US/docs/Web/HTML
