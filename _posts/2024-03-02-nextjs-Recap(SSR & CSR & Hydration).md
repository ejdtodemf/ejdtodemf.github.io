---
title : "Recap(SSR & CSR & Hydration)"
excerpt : "Recap(SSR & CSR & Hydration)"
toc : true
toc_sticky : true
toc_label : "Recap(SSR & CSR & Hydration)"
categories:
- Nextjs
tags:
- [Nextjs]
last_modified_at: 2024-03-02T08:00:00-10:00:00
---

# 날짜 : 2024-03-02 22:22

# 태그 : #Nextjs  
---

# 내용

## 개요
- 앞서 배운 SSR & CSR & Hydration 개념을 복습해 봅시다.
-[Next.js 문법](../../nextjs/nextjs-Next.js-문법), [SSR vs CSR](../../nextjs/nextjs-SSR-vs-CSR), [Hydration](../../nextjs/nextjs-Hydration)

### Recap
> Next.js 가 맨 처음 하는 일은
> 우리가 언제 페이지로 가든지 사용자에게 응답이 주어지기 전에 next .js는 backend에서 우리 application을 pre render 할 거임 
> 모든 components를 가져가서 따분하고 non interactive 한 HTML로 바꿔서 사용자에게 줌
>   

![image](../../assets/images/Pasted%20image%2020240303163438.png)
> 이게 바로 위 포커스 된 거기서 우리의 모든 React component가 HTML로 바뀐 것을 볼 수 있는 이유임 -> 이 부분을 사용자가 보게 될 거임
> 사용자가 우리 웹 사이트에 도착하자마자 우리는 HTML을 전달하고 그리고 나서 프레임워크와 React.js를 initialize 할 거임
> 그리고 use client 명령어를 가진 component가 hydrate 될 거임 -> hydrate는 interactive 되어진다는 뜻
> 이전 Next.js는 모든 componentr가 hydrate 됐지만, 지금 버전은 **어떤 component를 hydrate 할 건지 선택한다는 점이 새로운 방식임**
> 모든 컴포넌트가 hydrate 될 필요가 없기에 use client로 구별할 수 있게 함
> hydration은 우리가 받은 HTML의 위에서 React application을 실행하는 뜻, eventListener를 추가하고, interactive 하게 만드는 것, 어떠한 HTML을 실제 interactive한 React component로 바꾸는 것 onClick, setState, useState 등을 사용해서

> [!ques] 이렇게 했을 때 이점은 뭘까?
> 사용자들이 다운바당야 하는 JavaScript 코드의 양이 줄어든다는 것
>   

![image](../../assets/images/Pasted%20image%2020240303164400.png)
> 위 사진과 같이 interactive 하지않을 페이지들의 javascript 코드를 모두 다운받는 대신 
>   

![image](../../assets/images/Pasted%20image%2020240303164516.png)
> navigation component만 interactive 할 것이라고 정할 수 있음
> 오직 navigation.jsx 코드만 사용자가 다운로드 하게 됨
> client component만 다루는 JavaScript 파일을 다운로드 받게됨

> 
> 1. use client는 client에서만 render 한다는 의미가 아님
> 2. client에서도!! render 한다는 의미임
> 3. 모든 component는 backend에서 먼저 render 됨
> 4. CSR, SSR backend 에서 먼저 SSR로 pre render 될 것임 -> use client 유무에 상관없이!
> 5. 어떤 component가 hydrate 되는지, 즉 어떤 것이 interactive를 필요로 하는지, 어떤 것이 JavaScript가 필요한지, 어떤 것이 불필요한지 등을 결정할 때 중요함
> 6. **server component 안에 client component 는 가질 수 있음**
> 7. **client component 안에 server component가 오는 건 불가능! 모든 children이 client component가 될 거임 한마디로 불가능**

---

# 연결문서
- [SSR vs CSR](../../nextjs/nextjs-SSR-vs-CSR)
- [Hydration](../../nextjs/nextjs-Hydration)
- [Layouts](../../nextjs/nextjs-Layouts)
- [Metadata](../../nextjs/nextjs-Metadata)
- [Dynamic Routes](../../nextjs/nextjs-Dynamic-Routes)

# 참고 사이트
- https://nomadcoders.co/nextjs-for-beginners/lectures/4698
