---
title : "Github 블로그 계정 생성"
excerpt : "Github 블로그 계정 생성"
toc : true
toc_sticky : true
toc_label : "Github 블로그 계정 생성"
categories:
- Github
tags:
- [github, 블로그]
last_modified_at: 2023-12-29T08:00:00-10:00:00
---

# 날짜 : 2023-12-29 14:47

# 태그 : #github #블로그
---

# 내용

## 개요
- Github 블로그를 생성할 수 있습니다.
- jekyll 테마를 적용할 수 있습니다.

## 블로그 생성 시 필요한 Utility / Tool
- Git / Visual Studio Code

## Jekyll 테마 사용을 위해 필요한 언어  및 디렉터리
- Ruby
- Bundler

## GUI Git 툴
- Sourcetree

## 계정 생성
1. Git 설치 URL : [깃 다운로드 링크](https://git-scm.com/downloads)
2. Github 접속 URL : [깃허브주소](https://github.com/)
3. Github  접속 후 로그인 (없을 시 생성)
	- Git 계정 있을 시 Sign in
	- Git 계정 없을 시 Sign up
	-   
![image](../../assets/images/Pasted%20image%2020231227143749.png)
4. ** Dashboard > New  버튼 클릭 **
	-   
![image](../../assets/images/Pasted%20image%2020231227135617.png)
5. Create a new repository 빨간 테두리 부분 작성
	1) Repository name : UserName/github.io로 생성하기!!!
	- UserName.github.io >> github.io 블로그는 계정당 한 개만 생성 가능합니다!
	2) Public / Private 선택
	- 모두에게 공개해도 되는 블로그 -> Public
	- User에게만 보이는 블로그 - Private
	3) Initialize this repository with : 
	- Add a README file 체크
	- 체크 시 : 그 다음 작업 Clone 할 때 편하기에 체크 권장
	- 언체크 시 : Clone 할 때 다른 작업이 필요함
	4) Create repository 클릭
	-   
![image](../../assets/images/Pasted%20image%2020231227143017.png)
6. GUI git 툴 사용을 위하여 Sourcetree  설치
	- [Sourcetree](https://www.sourcetreeapp.com/)
	- SourceTree 외 사용할 수 있는 툴 
		- [Github Desktop](https://desktop.github.com/)
		- [GitKraken](https://www.gitkraken.com/download)
		- [SmartGit](https://www.syntevo.com/smartgit/)
		- [Git Extensions](https://gitextensions.github.io/)
7. Sourcetree 사용하여 Clone 하기
	1) 계정 생성 후 보이는 페이지에서 code 클릭
	2) 복사 아이콘 클릭하여 URL 복사
	-   
![image](../../assets/images/Pasted%20image%2020231227165344.png)
	3) Sourcetree 사용하여 Clone 하기
		3-1) Clone 클릭 
		3-2) 복사한 URL 붙여넣기
		3-3) 클론
		-   
![image](../../assets/images/Pasted%20image%2020231227171404.png)
	4) 해당 경로 클론 확인
		-   
![image](../../assets/images/Pasted%20image%2020231227171800.png)
8. jekyll 테마 다운받기
	- 여러가지 테마가 있지만, 각 테마마다 적용하는 법, 버전이 상이하기에 적용 방법이 잘 나와있는 테마를 다운 받는 걸 권장하며, 추후 테마 적용이 익숙해졌을 때 더 다양하게 적용해 보세요!!
	- 저는 가장 많이 사용되는 minimal mistakes 테마를 적용해 보겠습니다.
	- [jekyll 테마 다운로드 링크](http://jekyllthemes.org/page3/)
	- 다운 받은 후 테마 폴더내 모든 파일들을 Clone 된 폴더 경로에 붙여넣어주세요.
		- ** 이미 존재하는 README.md 파일은 덮어씌우셔도 되고, 건너뛰셔도 됩니다.
		- test, docs 폴더는 삭제해 주세요.
		-   
![image](../../assets/images/Pasted%20image%2020231227172514.png)
9. Ruby 설치하기
	- [Ruby 설치 링크](  
![image](../../assets/images/Pasted%20image%2020231227173315.png))
	- Ruby+Devkit 3.2.2-1 (x64) 파일 설치해 주세요. 
	- ** 저는 제일 최근 버전보단 하위 버전을 선호하는 편이라서요..ㅠㅠ 버전은 상관없습니다!!
	-   
![image](../../assets/images/Pasted%20image%2020231227173329.png)
	- ruby 설치 후 나오는 Interactive Ruby 창을 종료합니다.
10 . VSC 설치하기
	- [VSC 설치 링크](https://code.visualstudio.com/download)
	- 설치 안내에 따라 설치해 주시면 됩니다.
	- 설치 후 폴더 열기 > Clone된 폴더 경로 선택하여 열기하면 아래와 같이 열어집니다.
	-   
![image](../../assets/images/Pasted%20image%2020231227172942.png)
10. jekyll과 bundler 설치
	- 소프트웨어 및 일부 하드웨어와 함께 작동하는 데 필요한 모든 것을 포함하는 Package인 bundler를 설치해 준다.
	- VSC 터미널 실행 (단축키 Ctrl + ~)
	- 설치 및 버전 확인을 위하여 아래 명령어를 차례대로 입력해 주세요
		- gem install jekyll bundler
		- bundle update
		- jekyll -v
		-   
![image](../../assets/images/Pasted%20image%2020231227181055.png)
	- 작업 완료 후 jekyll server 명령어 입력
	- 생성된 http://로컬 경로 접속하기
	-   
![image](../../assets/images/Pasted%20image%2020231227181426.png)
	- 아래와 같이 실행되는 걸 볼 수 있습니다.
	-   
![image](../../assets/images/Pasted%20image%2020231227181538.png)
	- ** 명령어 입력 후 bundle 찾지 못하는 에러 발생 시 !!! ** 
	-   
![image](../../assets/images/Pasted%20image%2020231228100013.png)
		- gem install bundler
		- bundle install
		- gem clean
		- 명령어 입력!!
	- 이외 자주 발생하는 에러
		- Repository 생성 시 UserName.github.io.로 지정하지 않았을 경우 : 계정 삭제 후 재실행
		- 윈도우 user가 한글인 경우 : 윈도우 사용자 영어로 지정해야 함
			- Ex)C:\Users\한글\.bundle
		-  minimal mistakes 테마가 아닌 다른 테마 적용 시 Ruby 버전과 다운 받은 Ruby 버전이 상이할 경우 : 테마 적용법 꼼꼼하게 읽은 후 실행
			- minimal mistakes 테마를 설정한 이유가 여기에 있습니다. 많이 사용되는 테마이기에 적용법이 자세하게 설명되어 있으며, 커스터마이징 방법도 다른 테마들에 비해 참고 자료들이 많습니다!!

## 초기설정 완료!!

11. 접근 URL 설정
	- _config.yml : 블로그 설정파일 수정 필요
		- locale
		- title
		- url 값 변경 시 웹페이지에서도 접근 가능!!
		-   
![image](../../assets/images/Pasted%20image%2020231228100726.png)
12. Git Repository에 변경사항 Push
	- Sourcetree 실행
	- 파일 상태 > 변경사항 모두 스테이지에 올리기 > 
		1) 파일 상태
		2) 모두 스테이지에 올리기
		3) 커밋 (내용 입력 권장!!)
		4) Push
			-   
![image](../../assets/images/Pasted%20image%2020231228101353.png)
	- github 페이지에 모든 파일이 올라갔다면 성공!!!
		-   
![image](../../assets/images/Pasted%20image%2020231228101614.png)

## jekyll server 입력하여 로컬에서 접속되는지 확인해 보기! 
  
![image](../../assets/images/Pasted%20image%2020231228102802.png)

## https://username.github.io 페이지로도 확인해 보기!!
  
![image](../../assets/images/Pasted%20image%2020231228102837.png)

## 모두 들어가진다면 성공하신겁니다!!

> [tip]
> 혹시 404 에러가 발생한다면 _config.yml 파일 name, url 값을 확인해주세요!!!!!

## 다음 게시글은 포스팅 하는 방법을 알아볼 예정입니다!!!

---

# 연결문서
