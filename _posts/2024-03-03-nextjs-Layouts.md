---
title : "Layouts"
excerpt : "Layouts"
toc : true
toc_sticky : true
toc_label : "Layouts"
categories:
- Nextjs
tags:
- [Nextjs, Routing]
last_modified_at: 2024-03-03T08:00:00-10:00:00
---

# 날짜 : 2024-03-03 16:58

# 태그 : #Nextjs #Routing
---

# 내용

## 개요 
- Layouts.js 파일의 정의를 알 수 있습니다.
> [!ques] Layout 을 배워야 하는 이유?
> application을 빌드할 때 재사용하는 요소(elements)들이 있기 때문
> 한 개의 component를 여러 페이지에서 호출하지 않아도 자동으로 보일 수 있게 하기 위함
> 복사 붙여넣기 없이 어디서나 사용할 수 있는 레이아웃 시스템

> Layout component 작동법
> next.js는 layout component에 있는 export 된 디폴트 컴포넌트를 렌더링 함
> 그 다음 url을 확인함 -> URL 을 통해 about 컴포넌트를 렌더링 해야 한다는 것을 인식함
> **우리가 /aboutp-us로 이동하면 nextjs는 layout 컴포넌트를 렌더링 하고
> 이동하려는 페이지를 url을 통해 인식하여 layout 컴포넌트 안에 해당 페이지를 렌더링 하는 것**
> 어떤 페이지로 이동할 때마다 이 레이아웃 컴포넌트가 렌더링 되고 사용자가 가려는 페이지는 layout 컴포넌트의 children prop이 되는 것

```js 
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

``` js
import AboutUs from "./about-us/page"

export const metadata = {
  title: 'Next.js',
  description: 'Generated by Next.js',
}

export default function RootLayout({ children }) {//내부에 있는 컴포넌트들은 자동으로 children이라는 props로 바뀌게 된다는 말
 return (
    <html lang="en">
      <body>{children}</body> 
      //children은 next.js 규칙이 아닌 리액트의 규칙
    </html>
  )
}
//실제로 아래와 같이 렌더링 되고 있는 거임
<Layout>//레이아웃 컴포넌트 안에 
	<AboutUs />//url로 인식한 페이지 컴포넌트가 있는 거임
	//AboutUs 컴포넌트가 레이아웃 컴포넌트의 children이 되는 것
</Layout>
```

> app에는 하나의 레이아웃이 아닌 여러개의 레이아웃을 가질 수 있다!
> app/about-us/company/jobs/sales/page.jsx 생성

``` js
export default function Page(){
    return(
        <div>
            <h1>Sales jobs</h1>
        </div>
    )
}
```
> app/about-us/layout.js 생성

``` js
export default function AboutUsLayout({ children }) {
 return (
    <div>
        {children}
        &copy; Next JS is great!!
    </div>
  )
}
```
> 렌더링 되는 순서

``` js
<Layout> //app 폴더 레이아웃내 children render
	<AboutUsLayout> 
	//app 하위폴더 about-us에 무언가 있는지 확인 -> layout 
	//파일 확인 후 render AboutusLayout
	//about-us 하위 폴더 company/jobs/sales까지 확인
	 <Sales/> //sales 폴더에 page.jsx 확인 후 render
	</AboutUsLayout>
</Layout>
```

##### 정리
- nextJs는 URL을 통해 폴더로 들어가서  그 폴더에 레이아웃이 있는지 확인
- 있으면 그 레이아웃을 밖에 있는 다른 레이아웃 안에 rendering 함
- AboutUsLayout을 밖에 있는 layout에 렌더링 해 줌
- 그리고 sales 밑에도 layout.js가 있다면, SalseLayout도 렌더링됨

---

# 연결문서
- [SSR vs CSR](../../nextjs/nextjs-SSR-vs-CSR)
- [Hydration](../../nextjs/nextjs-Hydration)
- [Metadata](../../nextjs/nextjs-Metadata)
- [Dynamic Routes](../../nextjs/nextjs-Dynamic-Routes)
- [Recap(SSR & CSR & Hydration)](../../nextjs/nextjs-Recap(SSR-&-CSR-&-Hydration))

# 참고 사이트
- https://nomadcoders.co/nextjs-for-beginners/lectures/4699