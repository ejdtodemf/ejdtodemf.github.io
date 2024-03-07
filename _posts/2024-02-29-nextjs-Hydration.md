---
title : "Hydration"
excerpt : "Hydration"
toc : true
toc_sticky : true
toc_label : "Hydration"
categories:
- Nextjs
tags:
- [Nextjs, Routing]
last_modified_at: 2024-02-29T08:00:00-10:00:00
---

# 날짜 : 2024-02-29 15:42

# 태그 : #Nextjs #Routing
---

# 내용

## 개요
- client / server components의 정의와 차이점을 알 수 있습니다.
- Hydration의 정의를 알 수 있습니다.

#### Hydration
- JavaScript가 비활성화되거나 느리게 load되어도 최소한의 HTML은 존재함
- 사용자가 최초 HTML을 본 뒤에 어떤 일이 발생하는지
- React가 언제 활성화되는지 
- 이러한 과정들을 뜻함
- HTML을 React application으로 초기화하는 작업

###### state 사용한다고 가정한다면?

```js
"use client"

import Link from "next/link";
import {usePathname} from "next/navigation";
import {useState} from "react";

export default function Navigation(){
    const path = usePathname();
    const [count, setCount] = useState(0);//초기값 0
    return(
        <nav>
            <ul>
                <li>
                    <Link href="/">Home</Link> {path === "/" ? "❤" : ""}
                </li>
                <li>
                    <Link href="/about-us">About Us</Link>{path ===
                    "/about-us" ? "❤" : ""}
                </li>
                <button onClick={() => setCount((c)=>c + 1)}>{count}
                </button>
                //버튼 클릭 시 카운트 1씩 증가
            </ul>
        </nav>
    )
}
```

- button 태그 안에 0으로 render 되어있음
- button과 state의 초기값으로 넣었던 0 때문에
- 만약 javascript가 비활성화 되어있거나 로드에 시간이 오래 걸리는 경우 사용자들은 원하는 만큼 클릭은 할 수 있지만 카운트는 증가되지 않음 -> 0에서 멈춰있음
- 이유 : 위 코드에는 버튼에 eventListener가 연결되어 있지 않기 때문
- 그 후에 JavaScript가 로드되면???
	- js 즉, react가 버튼에 event Listenerfmf를 연결시킴
	- 그리고 state 등과 연결시킴
	- 그리고 사용자의 componet가 interactive 해 진다
- /about us --> 사용자에게 button 주어짐 (현재까지 사용자가 볼 수 있는 유일한 것) -->뒤 쪽에서 우리는 next.js 프레임워크를 로드하고, 프레임워크가 Initialize 되는 때에 우리가 만든 button은 우리가 만든 onClick eventListener가 연결된 버튼이 됨 --> 페이지는 interactive(상호작용) 하게 됨
- React나 프레임워크가 client에 로드되면 우리는 그 application을 hydrate하는 것임 --> 완전한 functional interactive app으로 변환시킬 수 있음

###### 이 과정들이 hydration 프로세스!!!

###### 다만, hydration 과정이 모든 component에 대해 발생하지 않음!!
- server side render는 모든 컴포넌트에 발생해 모든 컴포넌트들이 server side에서 먼저 랜더가 됨
- client에서 hydrate되는 컴포넌트, client에서 interactive하게 만들어질 컴포넌트는 오직 **use client** 지시어를 맨 위에 갖고 있는 컴포넌트들 뿐임
- Ex. page를 보면 두 개의 React component가 있음
-   
![image](../../assets/images/Pasted%20image%2020240301002231.png)
- one page : navigation --> use client 작성 O
- use client 는 framework에게 이 컴포넌트는 client에서 interactive 해야 하고, hydrated 되어야 한다고 요청함
- 초기 load에서 next.js는 이 컴포넌트를 초기 state에서 render 하게 됨 -->HTML을 사용자에게 주고 나서 eventListener들을 추가할 컴포넌트를 hydrate 하게됨

###### use client는 언제 넣어야 하지?
- 우리는 그저 app을 프로그래밍 하고, 컴포넌트를 만들면 에러가 발생
- Ex. useState 를 하려는데, use client 문구를 쓰지않았다면
-   
![image](../../assets/images/Pasted%20image%2020240301005513.png)
- 위와 같은 에러 발생하기에 해결할 수 있음

### use client는 오직 client에서만 render된다는 것을 의미하지 않음

### backend에서 render 되고, frontend에서 hydrate 및 interactive  되는 것을 의미함

```js
"use client"
import Link from "next/link";
import { usePathname } from "next/navigation"
import { useState } from "react";
  
export default function Navigation(){
    const path = usePathname();
    const[count, setCount] = useState(0);

return(
        <nav>
            <ul>
                <li>
                    <Link href="/">Home</Link> {path === "/" ? "🐱‍🐉" : ""}
                </li>
                <li>
                    <Link href="/about-us">About Us</Link>
                    {path === "/about-us" ? "🐱‍🐉" : ""}
                </li>
                <li>
                    <button onClick={()=> setCount((c) => c + 1)}>{count}
                    </button>
                </li>
            </ul>
        </nav>
    )
}
```

- two page : About us - title --> use client 작성 X

``` js
import Navigation from "../../componets/navigation";

export default function AboutUs(){
    return(
        <div>
            <Navigation/>
            <h1>About Us</h1>
        </div>
    )
}
```

- framework가 initialize된 후든 hydration이 완료된 후든 About us 타이틀은 hydrate 되지 않음. --> 그럴 필요가 없기에 그냥 HTML 그대로 남아있음 사진과 같이 --> React component가 되지 않음 --> user client를 넣는 이유
-   
![image](../../assets/images/Pasted%20image%2020240301004832.png)

#### Next.js 컴포넌트는 종류 2개

##### server component
- 그냥 아무곳에 만든거
- html에 자바스크립트 기능 넣기 불가능
- ex. <h4 onClick{}>
- useState, useEffect 등 사용 불가
- 자바스크립트 기능이 없기 때문에 페이지 로딩이 빠름
- server에서 먼저 render되고, hydrate 되지 않음 --> 사용자가 javascript를 더 적게 다운 받아도 된다는 의미
- 검색 엔진 노출 유리
- 큰 페이지 권장
- data fetching을 할 때 React applications에서 data fetching을 해온 방식과 비교하면 server client data fetching은 엄청난 결과를 가져옴  

##### client component
- **파일 맨 위에 'use client' 넣고 만든거**
- html에 자바스크립트 기능 넣기 가능
- useState, useEffect 등 사용 가능
- **자바스크립트 많이 필요하기에 로딩 속도 느림**
- hydration 필요하기에 로딩 속도 느림 : 
	- 리액트 문법을 쓰기 위해선 html 유저에게 보낸 후에 자바스크립트로 html 다시 읽고 분석하는 일
- JS 기능 (클릭 등) 필요한 곳만 client component
- use client components도 server에서 먼저 render되고 나서 hydrate됨

## 정리
- 만약 어떤 page 를 interactive하게 만들 필요가 없다면
- 만약 page 가 client에 딱 한 번만 render되고 다시는 render 될 일이 없다면, 
- 어떠한 useState 나 onClick events 같은 것들이 없을 경우
-  사용자에게 해당 컴포넌트를 위한 코드를 다운로드 받게끔 할 필요가 있을까? 
- 그럴 필요 없음. 사용자가 받아야 할 javascript 코드의 양이 줄어든다는 의미
- 사용자는 use client를 가진 컴포넌트의 javascript 코드만 다운받게 되기 때문에 페이지 로딩 속도가 빨라짐
- 만약 use client가 없는 컴포넌트는 그 server 컴포넌트에 대한 javascript 코드를 다시 다운로드 할 필요가 없음
- server components 안에 client components 는 가질 수 있지만, 그 반대는 안됨
- **모든 것이 첫 번째로 server side rendering된다는 점을 기억!!**
- **모든 것이 pre render되어서 HTML로 변환됨**
- HTML이 사용자에게 넘어가고 그 후에 client components만이 hydrate 되고, interactive 하게 되는 것!
- 그 외의 다른 component들 예를 들어 about us 같은 건 interactive하게 되지 않음 --> 다양한 일들을 할 수 있음을 의미!! --> Ex. DB와 통신할 수 있음. 이 코드는 server에서만 실행되니까. API key를 사용해서 API를 fetch한다고 하면 이 코드는 client로 절대 가지 않기 때문에 보안을 신경쓰지 않아도 됨 / 브라우저로 절대 가지않음. 서버에서만 랜더됨!!

---

# 연결문서
- [SSR vs CSR](../../nextjs/nextjs-SSR-vs-CSR)
- [Metadata](../../nextjs/nextjs-Metadata)
- [Layouts](../../nextjs/nextjs-Layouts)
- [Dynamic Routes](../../nextjs/nextjs-Dynamic-Routes)
- [Recap(SSR & CSR & Hydration)](../../nextjs/nextjs-Recap(SSR-&-CSR-&-Hydration))

# 참고 사이트
- https://nomadcoders.co/nextjs-for-beginners/lectures/4696
- https://nomadcoders.co/nextjs-for-beginners/lectures/4698