---
title : "Github 블로그"
excerpt : "Github 블로그 포스팅 하기"
toc : true
toc_sticky : true
toc_label : "Github 블로그 포스팅 하기"
categories:
- GithubBlog
tags:
- [미완료]
last_modified_at: 2024-01-02T08:00:00-10:00:00
---

## 날짜 : 2024-01-02 10:18

# 태그 : #미완료 
---

# 내용

## 개요
- 블로그에 게시글을 포스팅 할 수 있습니다.

## 블로그 생성 시 필요한 Utility / Tool
- Git / Visual Studio Code

## 게시글 포스팅 하기
[tip] 해당 테마의 포스터 양식 확인 
- 테마별로 포스터 양식이 따로 존재함!
- 모든 테마가 그런 건 아니지만, 대부분 테마에는 docs 폴더에 게시글 양식을 확인할 수 있는 파일이 존재합니다. 테마 적용 시 지웠던 docs 폴더내에 예시 파일을 확인 할 수 있습니다.
	-   
![image](../../assets/images/Pasted%20image%2020231228112115.png)
- 더 자세한 내용은 [minimal mistakes 페이지](https://mmistakes.github.io/minimal-mistakes/post%20formats/post-gallery/_)에서 확인 가능합니다!

# 1. 포스팅을 위한 posts 폴더 생성

## 1) VSC 내에서 폴더 생성
-   
![image](../../assets/images/Pasted%20image%2020231228112325.png)

## 2) 로컬 폴더 경로에서 생성
-   
![image](../../assets/images/Pasted%20image%2020231228112355.png)

* 파일 명 : yyyy-mm-dd-title.md
* 내부 양식 :   
![image](../../assets/images/Pasted%20image%2020231228114007.png)

| Name             | Mean                                                   |
| ---------------- | ------------------------------------------------------ |
| title            | 포스터 제목                                            |
| excerpt          | 포스터 내용 요약                                       |
| categories       | 포스터 소속 카테고리                                   |
| tags             | 포스터를 정의할 수 있는 태그                           |
| toc              | Table of content 의 약칭, 우측에 표시할 상단의 목차    |
| date             | 포스터 날짜                                            |
| last_modified_at | 게시글 마지막 수정일, 포스터에는 yyyy-mm-dd까지 나타남 |

* 작성 시 문자 정렬 방법
   
![image](../../assets/images/Pasted%20image%2020231228144218.png)
   
![image](../../assets/images/Pasted%20image%2020231228144133.png)

# 2. 포스터 작성 후 Sourcetree를 사용하여 Push
- jekyll server 명령어 입력 후 로컬 및 웹 페이지 주소로 확인하시면 됩니다!! 
	* jekyll server로 접속 시 :   
![image](../../assets/images/Pasted%20image%2020240102153810.png)
	* username.github.io로 접속 시 :   
![image](../../assets/images/Pasted%20image%2020240102153855.png)		

### 다음 포스터는 이미지 추가하는 내용을 올릴 예정입니다!!

![image](../../assets/images/Pasted%20image%2020231228155042.png)

---

# 연결문서
날짜 : 2023-12-28
	