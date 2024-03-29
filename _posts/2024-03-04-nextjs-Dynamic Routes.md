---
title : "Dynamic Routes"
excerpt : "Dynamic Routes"
toc : true
toc_sticky : true
toc_label : "Dynamic Routes"
categories:
- Nextjs
tags:
- [Nextjs, Routing]
last_modified_at: 2024-03-04T08:00:00-10:00:00
---

# 날짜 : 2024-03-04 16:02

# 태그 : #Nextjs #Routing 
---

# 내용

## 개요
- Dynamic Routes의 정의를 알 수 있습니다.
<br>
> Dynamic Routes
> /about-us 처럼 항상 똑같이 보이는 route는 정적 라우트 Static route
> 동적 라우트 /폴더/사용자가 입력한 숫자(변수)
> ex. /movies/:id ---> <Movie/>

<br>

> [!ques] URL이 동적(dynamic)이 되도록 어떻게 표현할까?
> 1. /app/movies 폴더 생성
> 2. /app/movies/[id] 폴더 생성
> 3. [id] 폴더가 하는 일은 --> next.js에게 movies/ 뒤에 무엇이 들어가도 괜찮다고 알려주는 것 (대괄호가 굉장히 중요)
> 4. 페이지를 만들어 url을 띄울 수 있음

``` js (/app/(movies)/movies/[id]/page.jsx)
export default function MovieDetail(){
    return(
        <div>
            <h1>Movie</h1>
        </div>
    )
}
```

-   
![image](../../assets/images/Pasted%20image%2020240304165238.png)
<br>
> [!ques] ID 데이터 값이 필요하다면??
> 1. MovieDetail 페이지에서 어떤 props을 받는지 알아본다

``` js
export default function MovieDetail(props){
    console.log(props)
    return(
        <div>
            <h1>Movie</h1>
        </div>
    )
}
```
> 2. 클라이언트 컴포넌트가 아니기에 프론트에서 실행되지 않고, 백엔드에서 렌더링 되어(hydration이 이뤄지지 않는다는 말) 터미널 창에 보인다 --> 자바스크립트는 브라우저가 아닌 백앤드에서 실행됨
> 3. 두 개의 파라미터를 얻을 수 있음 param : 변수 id 값 / searchParams : 필터
> Ex. url : /movies/1234567?region=kr&page=2
>   

![image](../../assets/images/Pasted%20image%2020240305104330.png)
<br>

#### 정리
- 리액트 라우터와 비슷하지만, 훅을 사용하지 않아도 되는 점이 상이함
- Nextjs는 URL을 이용하여 페이지를 렌더링 해줌
- 그러면 Moviedetail 페이지로 넘어감
- prop으로 유저가 보낸 id를 받고 렌더링 하게됨
- <MovieDetail param={{id: 12131}} /> 이런 방식으로
- 파라미터를 보내는 방식 : 

```js
export default function MovieDetail({params: {id}}){ //<<이렇게 옆에 코드처럼 보내기
    return(
        <div>
            <h1>Movie {id}</h1>
        </div>
    )
}
```

---

# 연결문서
- [SSR vs CSR](../../nextjs/nextjs-SSR-vs-CSR)
- [Hydration](../../nextjs/nextjs-Hydration)
- [Layouts](../../nextjs/nextjs-Layouts)
- [SSR vs CSR](../../nextjs/nextjs-SSR-vs-CSR)
- [Recap(SSR & CSR & Hydration)](../../nextjs/nextjs-Recap(SSR-&-CSR-&-Hydration))

# 참고 사이트
- https://nomadcoders.co/nextjs-for-beginners/lectures/4701
