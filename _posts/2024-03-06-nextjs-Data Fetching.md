---
title : "Data Fetching"
excerpt : "Data Fetching"
toc : true
toc_sticky : true
toc_label : "Data Fetching"
categories:
- Nextjs
tags:
- [Nextjs, Fetching]
last_modified_at: 2024-03-06T08:00:00-10:00:00
---

# 날짜 : 2024-03-06 10:13

# 태그 : #Nextjs #Fetching 
---

# 내용

## 개요
- MovieDetail 페이지에서 영화에 대한 정보와 영화에 대한 영상들의 목록을 fetch할 수 있습니다.
- async로 만들어 데이터를 fetch 할 수 있습니다.

#### 복습
> 한 개의 데이터라면 (복습)
> page에서 fetch를 하기
> 해야 할 일은 async를 넣고, 데이터를 fetch하고, loading 파일을 만들면 됨

#### 여러개의 데이터를 fetch 하는 방법

##### 1. Promise.all 사용하기
- 한 개의 데이터 작업이 끝나면 다음 작업으로 넘어가게 되면 시간이 오래 걸릴 수 있기 때문에 두 개의 데이터 fetch를 병행 작업해야 함
> Promise.all을 사용하기

``` js app\(movies)\movies\[id]\page.jsx
import { API_URL } from "../../../(home)/page"
//fetch 할 함수 작성
async function getMovie(id){
    console.log(`Fetching movies: ${Date.now()}`)
    await new Promise ((resolve) => setTimeout(resolve, 5000));//5초 대기 트릭코드
  
    const response = await fetch(`${API_URL}/${id}`);
    return response.json();
}

async function getVideos(id){
    console.log(`Fetching videos: ${Date.now()}`);
    await new Promise((resolve) => setTimeout(resolve, 5000));
    const response = await fetch(`${API_URL}/${id}/videos`);
    return response.json();
}

export default async function MovieDetail({params: {id}}){
    console.log("start fetching");
    const [movie, videos] = await Promise.all([getMovie(id),
    getVideos(id)])
    console.log("end fetching");
    
    return(
        <div>
            <h1>{movie.title}</h1>            
        </div>
    )
}
```

- 이 접근의 문제점은 두 Promise가 다 끝날때까지 UI가 보이지 않아서 유저가 항상 로딩 상태를 봐야 한다는 점
- ex. 요청이 3개가 있고, 하나가 5분이 걸린다면 사용자가 로딩 화면을 5분동안 봐야됨. 다른 두 요청이 1초 안에 끝나더라도

##### 2. Rect js의 컴포넌트 Suspense 사용하기
- getMovie가 준비되면 movie에 대한 UI 보여주고, getVideos가 준비되면 videos에 대한 UI를 보여줌
- 어느 한 쪽도 기다릴 필요없이 두 함수가 끝나야 UI가 보임
- streaming을 사용하여 next js가 getMovie 결과가 준비되면 같은 시간에 getVideos 함수가 로딩중이더라도이 데이터와 연결된 UI가 사용자에게 보내지도록 할 수 있음.

> React js의 component인 Suspense를 사용하는 법
> 1. components/movie-videos.jsx, movie-info.jsx 생성 두 개의 컴포넌트 생성

``` js
import { API_URL } from "../app/(home)/page";

async function getVideos(id){
    console.log(`Fetching videos: ${Date.now()}`);
    await new Promise((resolve) => setTimeout(resolve, 3000));
    const response = await fetch(`${API_URL}/${id}/videos`);
    return response.json();
}

export default async function MovieVideos(id){
    //videos에 관한 UI만 가짐 -> videos에 대한 것만 fetch
    //이유 : 페이지가 있으면 여러 개의 컴포넌트를 가지겠지만, 
    // 이건 videos만을 렌더링하는 컴포넌트이기 때문에
    //ex. 예고편이나 영화의 특징 같은
    
    const videos = await getVideos(id);
    return <h6>{JSON.stringify(videos)}</h6>
} 
```

``` js
import { API_URL } from "../app/(home)/page";
async function getMovies(id){
    console.log(`Fetching videos: ${Date.now()}`);
    await new Promise((resolve) => setTimeout(resolve, 3000));
    const response = await fetch(`${API_URL}/${id}`);
    return response.json();
}

export default async function MovieInfo(id)
    //Movies에 관한 UI만 가짐 -> Movies에 대한 것만 fetch
    //이유 : 페이지가 있으면 여러 개의 컴포넌트를 가지겠지만, 
    // 이건 Movies만을 렌더링하는 컴포넌트이기 때문에
    //ex. 영화 제목
    const movie = await getMovies(id);
    return <h6>{JSON.stringify(movie)}</h6>
}
```
> suspense가 데이터를 fetch 하기 위해 이 안의 컴포넌트를 await 하는 거고
> 로딩 상태를 분리할 수 있도록 해줌
> page 파일에서 직접 fetch 한다면, 프레임워크는 전체 페이지를 loading component로 바꿀거임
> 하지만, suspense를 사용하면 우리의 컴포넌트를 await할 수 있게 됨

> Next.JS 데이터 fetch하는 최적화 방식
> server component 사용 -> API를 사용할 필요없음, 데이터베이스와 직접 통신 or API 키로 API와 통신
>  fetch 하기 위해 우리의 페이지(component)를 async로 만들었음
>  원하는 곳에서 fetch하고, 데이터를 await 하고, UI를 return 했음
>  만약 fetch하는 함수가 시간이 오래 걸린다면, 브라우저에서 로딩하고 있기에 사용자는 아무것도 보고있지 않다는 것을 알았음
>  loading component는 프레임워크에 의해 사용됨
> 사용자가 처음으로 페이지에 요청하면, 프레임워크가 즉시 사용자에게 page 파일의 UI 대신 loading component를 줌 -> 페이지가 기다리고 있기에 무언가를 fetch하고 있기에 프레임워크는 layout을 렌더함 -> 때문에 navigation bar 같은 것들은 볼 수 있음
> fetch가 끝나면, 프레임워크가 loading component를 page 파일의 UI로 바뀜

---

# 연결문서 
- [Data Fetching Introduction](../../nextjs/nextjs-Data-Fetching-Introduction)

# 참고 사이트
- https://nomadcoders.co/nextjs-for-beginners/lectures/4707
