---
title : "Github Private Repository Clone"
excerpt : "Github Private Repository Clone"
toc : true
toc_sticky : true
toc_label : "Github Private Repository Clone"
categories:
- Github
tags:
- [github, 블로그, Private]
last_modified_at: 2024-01-07T08:00:00-10:00:00
---

# 날짜 : 2024-01-07 23:21

# 태그 : #github #블로그 #Private
---

# 내용

## 개요
- ssh 키를 받아 private Repository도 Clone 할 수 있습니다.

## 블로그 생성 시 필요한 Utility / Tool
- Git / Visual Studio Code

## SSH
- SSH(Secure Shell)의 줄임말 (보안이 강화된 Shell 접속을 뜻함)
- Git/Github 연동 시 필요한 보안 키
- 네트워크 상 다른 컴퓨터의 쉘을 사용할 수 있게 해주는 프로그램 or 프로토콜을 의미
- SSH를 사용하면 원격에서 네트워크 상의 컴퓨터에 접속할 수 있으며, 강력한 보안을 제공하기에 안전하지 못하거나 개방된 네트워크에서도 통신할 수 있음
- 서버 관리자는 원격지에서 SSH를 통해 서버에 접속해 서버를 관리하게 됨
- 원격지 (우리집 or 회사라고 생각하시면 편할 거 같아요!)
- 양측 간의 인증 후 비대칭 키를 이용하여 교환할 수 있음
- 교환된 대칭 키를 이용해 SSH 서버와 클라이언트 간 모든 통신은 암호화로 진행되어 매우 안전함

## GUI Tool
- Sourcetree

## CLI Tool
- Git bash

### 기존 방식처럼 Clone 진행할 시! Error!!
-   
![image](../../assets/images/Pasted%20image%2020240107232832.png)
- private 한 repository 를 [Github 블로그 계정 생성](../../github/github-Github-블로그-계정-생성) 에서 클론한 방식처럼 진행하면 **Error => Sourcetree github clone error 유효한 소스 경로/URL 이 아닙니다. ** 와 같은 오류가 발생합니다.
- public이 아닌 private 한 repository 이기 때문이죠!! 그래서 이번 글에서는 private repository  clone 하는 법을 알려드리려고 합니다!! 
- 저는 깃허브에 현재   
![image](../../assets/images/Pasted%20image%2020240108135645.png) 사진과 같이 ejdtodemf.github.io, obsidian 이렇게 두 개의 Repository 가 존재합니다.
- Obsidian은 git과 연동되어있는 Private 저장소이고, ejdtodemf.github.io는 지금 이 블로그입니다.
- 회사 컴퓨터에는 두 개의 저장소 둘다 클론이 되어있는 상태이지만, 집 pc 에는 클론이 되어있지 않아 찾아보고 해결한 방식입니다!!
- 저처럼 private 저장소를 두 군데에서 봐야할 때 필요한 방식이니 참고 하시면 될 거 같습니다!!

### Private Repository Clone 하기
1. SSH 키를 발급하기 위하여 git과 같이 설치된 Git bash를 실행시켜 아래 명령어를 입력해 줍니다.
- ssh-keygen
- 엔터 엔터 쭉쭉
- 아래 사진과 같이 발급 완료 및 저장된 경로도 나옵니다.
-   
![image](../../assets/images/Pasted%20image%2020240108142007.png)
- 파일을 VS 코드에서 오픈하면   
![image](../../assets/images/Pasted%20image%2020240108142133.png) 사진과 같이 열리는 것을 확인할 수 있습니다.
2. Github 홈페이지 메인에 접속 후 우측 상단의 프로필을 클릭해 주세요
	1) Setting 클릭
	-   
![image](../../assets/images/Pasted%20image%2020240108152400.png)
	2)  SSH and GPG keys 클릭 > New SSH key 클릭
	-   
![image](../../assets/images/Pasted%20image%2020240108152515.png)
	-   
![image](../../assets/images/Pasted%20image%2020240108152624.png)
	3) VS 코드에서 열었던 파일 내용 그대로 복사하셔서 key에다가 입력 후 Add SSH key 클릭합니다. **Title 값은 편하신대로!! 저는 집 pc 라서 home으로 작성했어용!**
	-   
![image](../../assets/images/Pasted%20image%2020240108153812.png)
	4) 아래와 같이 Github 에 SSH key 등록이 완료됐습니다!
	-   
![image](../../assets/images/Pasted%20image%2020240108154051.png)
    
3. 이제 클론을 준비합니다!
   1) 저장소 메인 페이지 접속하여 code 클릭
   2) ssh!! 클릭
   3) 복사 아이콘 클릭
   -   
![image](../../assets/images/Pasted%20image%2020240108154719.png)
     
4. Sourcetree (GUI) key 등록하기
	1) 소스트리 실행 > 메뉴바 도구 > 옵션 클릭
	2) SSH 클라이언트 putty를 쓰지않았기에 OpenSSH로 바꿔줍니다.
	3) SSH 키 경로 : Git Bash 에서 key 생성 시 나타난 경로!! VS코드에서 열어준 그 파일!! 경로를 넣어주시면 됩니다.
	4) 경로 넣어주신 후 확인 클릭!!
	-   
![image](../../assets/images/Pasted%20image%2020240108155745.png)

5. 마지막 단계!! 클론하기!! 
   1) sourcetree 메인 화면 > clone > 2번에서 복사한 암호로 보호된 SSH 키!! 입력 후 클론!! 클릭!!!!!!!
   2) 클론된 경로로 가시면 해당 Repository가 Clone 된 것을 확인하실 수 있습니다!!!!!

## 이렇게 오늘은 나만의 Private 한 저장소 SSH 키를 발급받아 클론하는 방법을 진행해 보았습니다~!!

## 저는 Sourcetree <-> Github 방법으로 포스팅 했지만, 더 많은 방법들이 있습니다. 제가 참고한 사이트들은 참고 사이트에 등록 해놨으니 참고 부탁드려용~

## 제가 이해한 부분에서만 포스팅 하다보니 상이한 점이 있을 수 있습니다. 혹시 그런 부분 또는 오타가 있다면 댓글 부탁드립니다!!

---

# 연결문서
- https://ansohxxn.github.io/blog/pro/
- https://heekangpark.github.io/ssh/01-introduction
- [PuTTY Key 사용하여 Sourcetree 에 키 등록하는 방법](https://old-developer.tistory.com/122)