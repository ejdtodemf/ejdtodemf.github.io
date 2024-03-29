---
title : "Data Fetching Introduction"
excerpt : "Data Fetching Introduction"
toc : true
toc_sticky : true
toc_label : "Data Fetching Introduction"
categories:
- Nextjs
tags:
- [Nextjs, Fetching]
last_modified_at: 2024-03-05T08:00:00-10:00:00
---

# 날짜 : 2024-03-05 11:57

# 태그 : #Nextjs #Fetching 
---

# 내용

## 챕터 소개
- client와 server component로부터 데이터를 fetch하는 법을 알 수 있습니다.
- streaming, suspense, loading fallback, error boundary를 사용하는 법을 알 수 있습니다.

#### React 앱에서 fetch 하던 방법
- 외부 라이브러리나 패키지 없이 하던 방법
- 사용자에게 로딩 상태를 보여줘야 함
- fetch는 항상 클라이언트에서 일어남 --> 브라우저가 API에 요청을 보낸다는 뜻
- 개발자 도구 -> Network 탭
-   
![image](../../assets/images/Pasted%20image%2020240305135834.png)
- 이 말은 보안 데이터 API 키 같은 것을 넣을 수가 없다는 뜻 --> 데이터베이스와 통신할 수 없다는 이야기
- 클라이언트에서 fetch 한다고 생각하면, 보안을 위해 항상 API를 넣어야 하고 데이터베이스와 직접 통신할 수 없기에 먼저 API에 요청을 보내야 하고, API가 안전한 환경에 있다면, 그 뒤에 데이터베이스에 요청을 보냄
- 백엔드가 API를 구현해야 프론트엔드(react)는 API와 통신할 수 있었음

``` js (home)/page.jsx
"use client"
import { useEffect, useState } from "react"

export default function Page(){
    const [isLoading, setIsLoading] = useState(true);
    //현재 로딩중인지 아닌지 체크하는 코드
    //SWR이나 React Query를 사용할 수 있음
    const [movies, setMovies] = useState([]);
    const getMovies = async ()=> {
        const response = await fetch
        ("https://nomad-movies.nomadcoders.workers.dev/movies");
        //니콜 쌤이 만들어놓은 API
        const json = await response.json();
        setMovies(json);
        setIsLoading(false);
    };
    useEffect(()=>{
        getMovies();
    }, []);
    return(
        <div>
            {isLoading ? "Loading..." : JSON.stringify(movies)}
             //현재 로딩중인지 아닌지 체크한 후 브라우저에 띄움 
        </div>
    )
}
```
> React JS가 나온 뒤로 하던 방식
> React App <=**> API <**=> DB
> React App이 API와 통신 API가 DB와 통신
> DB에서 다시 API 이용해 React앱에 응답 전달

> NEXT.js
> next.js, server component가 있다면, API 필요없음
> 서버 컴포넌트에서 fetch를 하면, useState, useEffect를 사용하지 않아도 되고, 로딩 상태를 직접 구현하지 않아도 됨
> 프레임워크가 직접해 주기에

<br>

#### Next 앱에서 fetch 하는 방법
- React fetch하던 코드를 next.js로 바꾸면

``` js (home)/page.jsx
export const metadata = {
    title: "Home",
};

const URL = "https://nomad-movies.nomadcoders.workers.dev/movies";

async function getMovies(){
//여기부터 안전한 코드
	await new Promise((resolve) => setTimeout(resolve, 5000));
	//프로그램을 멈춰서 느리게 만드는 간단한 트릭
	//백엔드의 응답까지 기다리는 시간
    const response = await fetch(URL);
    const json = await response.json();
    return json;
    //return fetch(URL).then(response=>response.json());
}//여기까지
//async를 사용해서 함수를 만드는 이유 : await을 사용하기 위해
//어떤 일이 발생하기를 기다리려고 await을 사용할 때 async를 무조건 써야 함 부모 함수에 무조건 async가 있어야 함
export default async function HomePage(){
//HomePage component가 async여야 하는 이유는 Next.js가 이 컴포넌트에서 await해야 하기 때문
//사용자가 우리 웹 사이트에 도착하는 순간 nextjs는 즉시 사용자에게 로딩 상태를 줄거고, 하지만 nextjs는 기본적으로 우리의 페이지를 작은 HTML부분으로 나눠서
    const movies = await getMovies();
    return(
        <div>
           {JSON.stringify(movies)}
        </div>
    )
}
```

-   
![image](../../assets/images/Pasted%20image%2020240305142650.png)
- 같은 페이지를 구현하지만, useState, useEffect, 로딩 화면등을 구현하지 않았음
- 매우 빨라서 보이지 않음. 브라우저가 어떤 것도 fetch하지 않았음
- 이유 :
	- Next js는 프레임워크이기 때문
	- 단지 서버 컴포넌트에서 Next js가 사용자의 첫 번째 API 요청에서 fetch된 캐싱된 데이터를 받고, 나머지는 데이터를 기억하고 있기에 API를 재요청하지 않음
	- 서버 컴포넌트를 사용한다면, fetch된 url을 자동으로 캐싱시켜줌
- 로딩 상태는 존재함 (사라진게 아닌 옮겨간거임) 
- 이유 :
	- API의 첫 번째 요청에 대한 응답이 느릴 수 있기 때문
	- 데이터베이스에 요청한다면 응답에 시간이 좀 걸릴수도 있음
	- 확인할 수 있는 코드는 위 코드에 기재되어 있음(await new...)
- 개발자 도구 > 네트워크 탭에도 url에 관한 정보가 없음
- API를 가져오는 건 없음
- 백엔드가 가져옴
-   
![image](../../assets/images/Pasted%20image%2020240305143108.png)
<br>

```js
async function getMovies(){
//여기부터 안전한 코드
	await new Promise((resolve) => setTimeout(resolve, 5000));
	//프로그램을 멈춰서 느리게 만드는 간단한 트릭
	//백엔드의 응답까지 기다리는 시간
    const response = await fetch(URL);
    const json = await response.json();
    return json;
    //return fetch(URL).then(response=>response.json());
}//여기까지
```

> 이 코드가 완료되지 않으면 백엔드에서 렌더링 작업이 이뤄지지않음
> 사용자는 아무것도 볼 수 없음.
> loading.jsx 파일을 만들어 로딩 시 UI를 구현해야 함
> **꼭 파일 이름은 loading 이어야 하고, page 파일과 같이 있어야 함**

``` js(home)/loading.jsx
export default function Loading(){
    return <h2>Loading..</h2>
}
```

- server component에서 fetch 하는 중에 loading 파일을 제공해 주면 그 파일이 페이지에 나타나게됨 (백엔드에서 로딩중 브라우저는 백엔드 작업이 완료되지 않았다고 생각해서 로딩중인 원이 보임) --> 하지만, next.js는 사용자가 페이지에 도착하는 순간 loading component를 볼 수 있게 함
- 그 후 server component가 fetch를 끝내면, Next.js가 loading component를 바꿔줌
- loading component는 페이지의 component로 바뀜(백엔드가 브라우저에 완료된 결과값을 보냄) 코드 <div>{JSON.stringify(movies)}</div>
- 이유 : 백엔드가 content를 streaming하기 때문

#### 정리
- Next.js가 하는 것은 웹 사이트의 일부를 천천히 보내는 것
- 첫 번째로 보내는 일부분은 레이아웃이나 navigation
- 그 다음은 loading component 하지만 아직 백엔드 작업이 완료되지 않았어 를 next.js가 보내고, 브라우저는 기다리게 됨 
- 함수의 작업이 완료되면 next.js가 끝났어. 이게 응답의 결과값이야
-  const movies = await getMovies(); next.js는 여기 있는 것으로 응답
- 프론트엔드의 프레임워크는 loading component 대신 아래 코드를 렌더링 함

``` js
return <div>{JSON.stringify(movies)}</div>
```

``` js
export default async function HomePage(){
    const movies = await getMovies();
    return(
        <div>
           {JSON.stringify(movies)}
        </div>
    )
}
```

> HomePage에 async를 사용하는 이유
> Next.js가 이 컴포넌트에서 await해야 하기 때문
> 사용자가 우리 웹 사이트에 도착하는 순간 nextjs는 즉시 사용자에게 로딩 상태를
> 줄거고, 하지만 nextjs는 기본적으로 우리의 페이지를 작은 HTML부분으로 나눠서
> 준비된 HTML 부분을 브라우저에 줄 수 있음
> navigation bar나 loading component 같은 거를..
> 사용자에게 보여질 준비가 된 컴포넌트는 브라우저에 즉시 전달됨
> 그리고 브라우저에게 백엔드에서 통신이 아직 마무리되지 않았고, 기다려줘야 한다고 함
> 따라서 우리는 컴포넌트를 await하고 있음
> await가 끝나면 브라우저에게 마지막 HTML 부분을 전달해줌
> 그러면 프레임워크가 loading component를 await된 컴포넌트로 바꿔줌

> 장점
> 1. 전처럼 사용자가 아무것도 볼 수 없었던 때와 달리 로딩 페이지를 볼 수 있다
> 2. 백엔드에서 데이터를 fetch 하면서 useState 같은 컴포넌트를 사용하지 않았음.
> 아직 즉각적인 로딩 상태를 사용자는 UI 로 볼 수 있음
> 3. 통신이 마무리되었을 때 프레임워크에 의해 실제 결과값으로 자동적으로 교체됨

---

# 연결문서 

# 참고 사이트
- https://nomadcoders.co/nextjs-for-beginners/lectures/4704
- https://nomadcoders.co/nextjs-for-beginners/lectures/4705
- https://nomadcoders.co/nextjs-for-beginners/lectures/4706
