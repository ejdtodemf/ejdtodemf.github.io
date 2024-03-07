---
title : "Next.js 문법"
excerpt : "Next.js 문법"
toc : true
toc_sticky : true
toc_label : "Next.js 문법"
categories:
- Nextjs
tags:
- [Nextjs]
last_modified_at: 2024-02-23T08:00:00-10:00:00
---

# 날짜 : 2024-02-23 10:11

# 태그 : #Nextjs  
---

# 내용

## 개요
- Next.js를 알 수 있습니다.

#### React libray
- UI 인터페이스를 build 하는데 사용하는 라이브러리
- 반응형 사용자 인터페이스를 구축하는데 도움이됨
-  CSS에 Style component를 사용할 수도 있고, SAS를 사용할 수도 있음
- Routing을 위해 React Router를 사용하거나또는 Expo Router를 사용할 수 있음
- 어떤 폴더, 파일, 구조에서 React를 사용할지 사용자가 결정할 수 있음

#### React Framework
- 주도권이 없음 프레임워크가 주도함
- 여러가지 결정을 사용자 대신해 주고 자동화 하도록 할 수 있음
- 폴더 이름을 지정할 필요없고, application을 시작할 필요없음

#### Next.js
- 제작자가 사용자들에게 Route Handlers, Server Components, CSS Supprot 등 이러한 항목에 대해서 도와주기로 결정했다는 것, implement해 줄 것임
- 규칙을 지켜야 함 -> 프레임워크
-  Ex. 사용자가 올바른 방법으로 올바른 위치에 파일을 넣는다는 전제하에 next.js가 풀스택 웹 어플리케이션을 만들어 줄 것임
- 사용자가 Next.js를 import하고 사용한다는 개념이 아님
- Next.js가 사용자들의 code를 call할 거임

##### Next.js / React.js 차이점
- React.js에서는 사용자가 원하는 방식으로 사용했음 Import하고 사용함
- Next.js 프로젝트를 시작하고 프레임워크를 시작하면, 프레임워크가 코드를 찾아서 실행함
- 코드를 올바른 위치에서 배치하고, 함수에 올바른 이름을 지정하고, 변수를 올바른 모양으로 export 하면 next.js가 웹 사이트를 구축해줌 
- Next.js에서 사용자가 해야 할 건 무언가를 Export 하면 next.js가 그걸 받아와서 모양과 이름이 맞다면 페이지의 title을 알아서 바꿔줌 -> 프레임워크
- React.js만 사용하는데 title을 바꾸려면 사용자가 스스로 다른 것을 설치하고 실제로 어딘가로 가서 작업을 해야함

###### 라이브러리는 사용자들이 사용하는 것, 주식 거래를 위해서 통화 변환기능이 필요하다면, 라이브러리에서 그걸 도와줄 패키지를 찾을 수 있음. 필요할 때 라이브러리만 호출하면 사용할 수 있음. 라이브러리가 아닌 사용자들이 모든 결정권을 가짐

###### 프레임워크는 우리가 결정을 내리거나 import 하지 않음. 대신에 코드를 올바른 위치에 넣으면 프레임워크가 그 코드를 가져와서 사용하고 Next.js의 경우에는 이를 이용해 풀 스택 웹 애플리케이션을 빌드해줄거임

###### 라이브러리는 사용자가 사용하고, 프레임워크는 사용자의 코드를 사용함

##### react-router 작동방식
- url 지정하고 home이라는 컴포넌트 render를 요청하는 것
- 아래 url은 이 컴포넌트를, 저 url은 저 컴포넌트를 렌더링 하게끔 지정하는 것

```react
/ ---> <Home/>
/about-us ---> <AboutUs/>
/movies/:id ----> <Movie/>
```

##### next-router 작동방식
- 사용자가 직접 url을 적어줄 필요가 없음

```js
/app/page.jsx or tsx
export default function Tomato(){
    return <h1>Hello</h1>
}
// home이자 root로 가는 것
```

- aboutus 페이지를 가고싶다면?
- 1. app/about-us 폴더 생성
- 2. about-us 폴더에 page.jsx 생성

``` js
export default function AboutUs(){
    return <h1>AboutUs</h1>
}
```

- 1. about-us/company/sales 폴더 생성
- 2. sales/page.jsx 파일 생성

``` js
export default function Sales(){
    return <h1>Sales team</h1>
}
```

- 이 폴더들의 의미는 url 경로 일부분 설정해주는 것
- **매번 React-router와는 다르게 Next.js는 next.js에게 어떤 경로에서 어떤 컴포넌트를 불러오라고 작성할 필요없음**

###### app 폴더에는 다른 폴더를 만들어 넣어도 되는 건가요?
- page라는 파일을 만들지 않는 이상 실제 경로에 포함되지도 렌더링 되지도 않기 때문에 만들어도 됨
- 선호하지는 않음

##### Not-Found 
- 1. app/not-found.jsx 파일 생성

``` js
export default function NotFound(){
        return <h1>Not found!!!</h1>
}
```

- 존재하지 않는 경로로 가면 위 페이지가 보여짐

##### navigation bar
- Next.js에는 사용자에게 url에 관한 정보를 알려주는 hook들이 존재함
- router까지 접근 가능하게 해줌
- navigation.jsx에서 사용할 hook은

###### usePathname
- path name : 현재 사용자가 머물고 있는 url
- 사용자가 "/" home에 있는지, /about-us 등 다른 url 경로에 있는지를 알려주는 훅

``` js
import Link from "next/link";
import {usePathname} from "next/navigation";

export default function Navigation(){
//이렇게 아래와 같은 문구만 추가한다면, 에러 발생
//client components 문구를 추가하여 사용하라.
    const path = usePathname();
    console.log(path);
    return(
        <nav>
            <ul>
                <li>
                    <Link href="/">Home</Link>
                </li>
                <li>
                    <Link href="/about-us">About Us</Link>
                </li>
            </ul>
        </nav>
    )
}
```

- 상단에 "use client" 작성

```js
"use client"
import Link from "next/link";
import {usePathname} from "next/navigation";

export default function Navigation(){
//이렇게 아래와 같은 문구만 추가한다면, 에러 발생
//client components 문구를 추가하여 사용하라.
    const path = usePathname();
    console.log(path);
    return(
        <nav>
            <ul>
                <li>
                    <Link href="/">Home</Link>{path === "/" ? "❤" : ""}
                    // 사용자가 위치한 곳이 홈이면 하트를 옆에 표시
                </li>
                <li>
                    <Link href="/about-us">About Us</Link>
                    {path === "/about-us" ? "❤" : ""}
                    // 사용자가 위치한 곳이 /about-us이면 하트를 옆에 표시
                </li>
            </ul>
        </nav>
    )
}
```

###### 더 자세한 use client 설명은?!! [Hydration](../../nextjs/nextjs-Hydration) 참고해 주세요!!

#### react, next 문법
- return() 안에 HTML 넣을 때
	- 1개 <태그>로 시작해서 끝나야 함
	- <div'><./div>
	- <div'><./div>
	- 이런식으로 평행으로 태그 값 사용 불가
	- 하나의 태그 값으로 묶어줘야 함
- style 집어넣기
	- class 넣고 싶으면?
	- **class X -> className 이렇게 써야 함**
- HTML 안에 변수를 넣으려면 데이터 바인딩
	- js : document.getElementsByClassName('.title-sub')[0].innerHTML = name
	- react : { name }
- 모든 속성에 { 변수 } 적용 가능
- -기호는 X ex.font-size XXX -> fontSize

#### page.js (메인페이지) 보여줄 때
- 1. 옆에 layout.js 있으면 그걸로 page.js 감싸서 보임
- 2. 상위 폴더에 layout.js 있으면 그걸로 1번을 감싼다
- 3. 상위 폴더에 또 상위폴더 layout.js 있으면 그걸로 2번 감싼다
- page.js 보여줄 때는 옆, 상위에 있는 모든 layout.js 합쳐서 보여줌 

#### layout.js
- 상단바 작성
- head 부분이기에 모든 페이지에 상단바가 보이면 좋겠다라고 생각한다면, layout.js(tsx) 에 작성해주면 됨
- 페이지 변경과 상관없이 계속 보여줄 UI는 layout.js에 작성하면 됨

#### Routing
- url로 페이지를 나누는 행위
- URL과 페이지 만들고 싶으면
	- app 폴더 안에 폴더 만들기
	- 그 안에 page.js(tsx) 넣고
	- 그 안에 레이아웃 넣기

#### Link 만들고 싶을 때?
- Link << import Link from "next/link"
- ex. <'Link href="/">홈</Link'>
- ex. <'Link href="/list">상품목록</Link'>
- 부드럽게 페이지 전환해줌

#### map() 함수
- map(param1, param2)

``` map
let array = [2,3,4]
array.map((param1, param2)=>{
	console.log(param1)
	console.log(param2)
}) 
**> 2 \n 3\n 4 출력
**> 0 \n 1 \n 2 출력됨
array.map(function(){
	
})
```

- param1 : 배열 안에 값들을 인덱스 순서대로 출력해줌
- param2 : 증감하는 변수(반복될 때 마다 0부터 1씩 커지는 정수 카운트 같은 개념?)
- return에 적은 걸 array로 담아줌
- map 반복문 사용 시 key[ 유니크한 값'] 넣으면 좋음
- ex. div className="" key={}
- 서로 요소들을 구분하기 헷갈려 하기 때문에 반복 생성되는 html 요소마다 유니크한 값을 갖게 하는 게 좋음
-   
![image](../../assets/images/Pasted%20image%2020240223150504.png)

#### 이미지 등록

```html
1. <img src="/이미지.png"></img>

2. 최적화된 이미지를 등록하고 싶다면
import Image from "next/image";
import 변수 from "/public/가져오고싶은 이미지.png";
<Image src={변수} alt="써도되고 안써도됨 혹시 오류가 난다면 써야함"/>

3. 외부 이미지 등록 => width, height 요소는 무조건 넣어줘야 함
1) <Image src="외부 이미지 링크" width={500} height={500} /> 
2) next.config.js 파일 세팅 필요함 (도메인, 경로 등록)
images: {
	remotePatterns: [{
		protocol: 'https',
		hostname: 's3.amazonaws.com',
		port: '',
		pathname: '/my-bucket/**',
	}],
},
```

#### component 만드는 법
1. function 작명(){}
2. return(축약할 긴 HTML)
3. html 부분에 <작명/> 사용

``` html

<CartItem/> --> 컴포넌트 사용 방법

function CartItem(){
	return(
		<div className="">
			<p>상품</p>
			<p>$40</p>
			<p>1개</p>
		</div>
	)
}
```

#### function 문법 쓰는 이유
- 긴 코드 한 단어로 축약 가능
- 같은 코드 재사용 가능

#### component 문법 쓰는 이유
- 긴 코드 한 단어로 축약 가능
- 같은 코드 재사용 가능
- 큰 page.js 만들 때
- component 많이 사용하면 데이터 공유가 어려움

#### import 작명 from 
- 변수나 파일 등 가져오고 싶을 때 사용하는 방법
- 가져와야 하는 파일에 **export default!!** 기입 다른데에서 써도 된다는 허락

```js
file : page.js
import {age, name} from './data.js' // ./<< 현재 파일 위치 
//상위폴더 >> './../'
//하위폴더 >> './하위폴더명/'
file : data.js
let age=0;
let name="kim"

export default {age, name};
```

---

# 연결문서 

# 참고 사이트
- https://nomadcoders.co/nextjs-for-beginners/lectures/4694