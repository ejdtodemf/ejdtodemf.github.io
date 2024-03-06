---
title : "Event part One  Form Submission"
excerpt : "Event part One  Form Submission"
toc : true
toc_sticky : true
toc_label : "Event part One  Form Submission"
categories:
- 자바스크립트
tags:
- [자바스크립트]
last_modified_at: 2024-02-28T08:00:00-10:00:00
---

# 날짜 : 2024-02-28 16:08

# 태그 : #자바스크립트  
---

# 내용

## 개요
- form 형식을 알 수 있습니다.

#### input
- input 태그를 사용하여 value 값을 넣어줄 때 유효성 검사가 필요함
<br>
방법1.

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
    <div id="login-form">
        <input required maxlength="15", type="text" placeholder="what is 
        your name?"/>
        <button>Log In</button>
    </div>
    <script src="app.js"></script>
</body>
</html>
```

``` js
// const loginForm = document.querySelector("#login-form");
// const loginForm = document.getElementById("login-form");
// const loginInput = loginForm.querySelector("input");
// const loginButton = loginForm.querySelector("button");
//위 처럼 작성할 수도 있고,

const loginInput = document.querySelector("#login-form input");
const loginButton = document.querySelector("#login-form button");
  
function onLoginBtnClick(){
    const userName = loginInput.value;
    if(userName === "")//userName이 빈 값이라면, 아래 문구 팝업 발생
        alert("Please write your name!");
    else if(userName.length > 15) // userName이 15글자를 넘는다면,
        alert("Your name is too long.");//해당 문구 팝업 발생
    else
        console.log(userName)
}
loginButton.addEventListener("click", onLoginBtnClick);
```

#### form 형식으로 바꾼다면?
- input 태그는 form 안에 있어야 함!

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
    <form id="login-form">
        <input required maxlength="15", type="text" placeholder="what is 
        your name?"/>
        <input type = "submit" value="Log In"/>
    </form>
    <script src="app.js"></script>
</body>
</html>
```

``` js
const loginInput = document.querySelector("#login-form input");
const loginButton = document.querySelector("#login-form button");
	function onLoginBtnClick(){
	    const userName = loginInput.value;
	   console.log(userName)
	}
	loginButton.addEventListener("click", onLoginBtnClick);
```

- input 필드에 값을 입력하지 않으면,
	-   
![image](../../assets/images/Pasted%20image%2020240228163320.png)
- 15글자를 넘길 수 없음
	-   
![image](../../assets/images/Pasted%20image%2020240228163345.png)
- input 안에 있는 button을 누르거나 submit type의 input 을 작성한 후 클릭 또는 엔터를 누르면?
	- url이 계속 새로고침 되고 있음
	- 유저가 작성한 form이 submit이 된다.
	- button과 상관없이 form이 value값을 submit 해줌

#### form을 submit 할 때 입력값을 받아내는 방법

``` js
const loginInput = document.querySelector("#login-form input");
const loginForm = document.querySelector("#login-form");
  
function onLoginSubmit(){
   const userName = loginInput.value;
   console.log(userName)
}
loginForm.addEventListener("submit", onLoginSubmit);
```

- 새로고침이 발생하는 건 form submit의 기본 동작(브라우저가 그러라고 프로그래밍 되어있음)

#### ()를 추가하는 건
- function을 즉시! 실행한다는 뜻임
	- loginForm.addEventListener("submit", onLoginSubmit());
	- onLoginSubmit();
	- () 이것들을 더하면 브라우저가 보자마자 자동으로 function을 실행하기에 이렇게 작성하지 않음
	
- onLoginSubmit(info) 브라우저는 브라우저 내에서 event로부터 정보를 잡아내서 onLoginSubmit function 실행 버튼을 누르고 있음

```js
//"submit" 같은 event가 발생할 때 브라우저가 작성한 function을 호출하게 됨
//onLoginSubmit() 이렇게 비어있는 채로 호출하지 않고,
//onLoginSubmit(xxxxx) 첫 번째 argument로써 추가적인 정보를 가진 채로 호출함
const loginInput = document.querySelector("#login-form input");
const loginForm = document.querySelector("#login-form"); 

function onLoginSubmit(tomato){
    tomato.preventDefault();// 어떤 event의 기본 행동이든지 발생하지 않도록 하는 것, 기본 행동이란? 어떤 function에 대해 브라우저가 기본적으로 수행하는 동작을 말함
 // 사용자가 form을 submit하면 브라우저는 기본적으로 페이지를 새로고침 하도록 되어있는데, 이 function 추가함으로써 막아짐
    console.log(tomato)
    console.log(loginInput.value)//로 바꿔주면, 버튼을 클릭해도 새로고침이 안되는 것을 확인할 수 있음
}
loginForm.addEventListener("submit", onLoginSubmit);

// 위 코드를 실행하면
//   
![image](../../assets/images/Pasted%20image%2020240228165740.png) 
// 콘솔창에 위 사진과 같이 출력됨
// onLoginSubmit function이 하나의 argument를 받도록 하고 그걸 JS에 넘겨주는 것 
```

## 모든 EventListener function의 첫번째 argument는 항상 지금 막 벌어진 일들에 대한 정보가 됨(JS가 우리들에게 제공해줌)
- ex. 대상은 무엇인가. submit 정보는 무엇인가 등등

---

# 연결문서 

# 참고 사이트
- https://nomadcoders.co/javascript-for-beginners/lectures/2901
