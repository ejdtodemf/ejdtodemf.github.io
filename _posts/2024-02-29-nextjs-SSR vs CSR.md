---
title : "SSR vs CSR"
excerpt : "SSR vs CSR"
toc : true
toc_sticky : true
toc_label : "SSR vs CSR"
categories:
- Nextjs
tags:
- [Nextjs, Routing]
last_modified_at: 2024-02-29T08:00:00-10:00:00
---

# 날짜 : 2024-02-29 14:38

# 태그 : #Nextjs #Routing  
---

# 내용

## 개요
- SSR과 CSR의 정의 및 차이점을 알 수 있습니다.

##### CSR(Client Side Rendering)
- 모든 rendering, 즉 모든 UI 구축 작업이 모두 client측에서 일어남
- client는 javascript를 로드하고, 그 후에 js가 UI를 빌드함

###### 단점
- 유저는 무언가를 보기 위해서는 모든 JavaScript 파일을 다운받아야 하고 모든 파일이 다운로드 완료될 때까지 기다려야 함.
- 아무 UI 없는 빈 화면을 오래 보게될 수 있음. 자바스크립트를 기다려야 하기 때문에
- SEO 검색 엔진 최적화
- 만약 유저의 웹 사이트가 Google에 노출되기를 바란다면, Google에게 빈 페이지를 보여주지 않은 것이 좋음 -> Google은 페이지의 HTML을 보기 때문에
- 만약, 어떠한 프레임워크도 사용하지 않고, 보통의 create-react-app으로 설치해 사용한다면, 모든 것이 Client Side Rendering 되는 것임 

##### SSR(Server Side Rendering)
- next.js로 웹 사이트를 빌드할 때는 자동으로 ssr이 됨
- 페이지의 소스 코드를 보면 페이지의 내용들이 모두 실제로 브라우저 코드에 있음
- 즉, 브라우저가 JS가 로드될 때까지 기다릴 필요가 없다는 것을 의미함
- 이미 화면에 표시할 HTML을 가지고 있기 때문에
- 자바스크립트가 활성화 되어있지 않아도 사용자가 HTML을 볼 수 있음 

##### Next.js가 application을 render 하는 방식?!
- rendering : next.js가 사용자의 react component를 가져와서 브라우저가 이해할 수 있는 html로변환하는 작업을 뜻함
- next.js application의 모든 page 안의 모든 component들은 next.js가 그것들을 우선 서버에서 render한다는 것
- ex. 사용자가 /about-us로 접속하면, 사용자에게 어떠한 HTML을 주기전에 next.js는 server 즉, backend에서 application을 render할 것임
- next.js는 사용자의 모든 컴포넌트를 render 해서 그 html을 갖고 브라우저 request에 대한 response로 줄 것임
- 때문에 사용자가 about us 페이지에 접속해도 비어있는 html을 보게될 일은 없음
- 사용자는 next.js가 backend에서 생성한 html을 보게됨
- 최초 application의 UI 빌드에서는 자바스크립트에 의존하지 않는다는 것

###### 모든 컴포넌트는 우선 SSR이 될 것임

```js
"use client"
import Link from "next/link";
import {usePathname} from "next/navigation";

export default function Navigation(){
    const path = usePathname();
    console.log(path);
    return(
        <nav>
            <ul>
                <li>
                    <Link href="/">Home</Link> {path === "/" ? "❤" : ""}
                </li>
                <li>
                    <Link href="/about-us">About Us</Link>
                    {path === /about-us" ? "❤" : ""}
                </li>
            </ul>
        </nav>
    )
}
```

- "use client"가 작성되어 있다고 해서 이 컴포넌트는 server측에서가 아니라 client 단에서만 render 되는 것이라고 생각하지만, 실제로 server에서 render되었다는 것을 의미함

#### 정리
- 모든 컴포넌트와 페이지들은 먼저 backend에서 render 된다는 것
- 그것들은 HTML로 변환됨
- 그 HTML이 브라우저에 남겨짐
- 사용자들이 페이지에 접근해서 바로 UI 보기 가능
- 자바스크립트 활성화 여부에 상관없이 볼 수 있음

---

# 연결문서 
- [Hydration](../../nextjs/nextjs-Hydration)
- [Layouts](../../nextjs/nextjs-Layouts)
- [Metadata](../../nextjs/nextjs-Metadata)
- [Dynamic Routes](../../nextjs/nextjs-Dynamic-Routes)
- [Recap(SSR & CSR & Hydration)](../../nextjs/nextjs-Recap(SSR-&-CSR-&-Hydration))

# 참고 사이트
- https://nomadcoders.co/nextjs-for-beginners/lectures/4691
