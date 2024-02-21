---
title : "Static"
excerpt : "Static"
toc : true
toc_sticky : true
toc_label : "Static"
categories:
- Java
tags:
- [미완료]
last_modified_at: 2024-02-07T08:00:00-10:00:00
---

# 날짜 : 2024-02-07 17:56

# 태그 : #미완료 
---

# 내용

## 개요
- Static 의 정의를 알 수 있습니다.

#### static  멤버란?
- 인스턴스 멤버와는 달리 객체를 생성할 필요없이 접근할 수 있는 클래스 멤버 (변수 혹은 함수)
- Ex.
-   
![image](../../assets/images/Pasted%20image%2020240207180759.png)
-   
![image](../../assets/images/Pasted%20image%2020240207180809.png)

#### static 멤버가 필요한 이유?
- 전역 변수로 쓰일 수 있음
- ex.
- **System.out.println / System.in 처럼 java.langSystem 클래스의 in, out 필드**
- 클래스의 객체 인스턴스 간ㄴ에 멤버를 공유할 필요가 있을 때

#### static 멤버의 제약조건
- static 메소드는 객체가 생성되지 않은 상황에서도 실행될 수 있기 때문에, 객체가 생성된 후에 사용할 수 있는 인스턴스 멤버를 사용할 수 없음

#### public static void main(String[] args) 의미?
- public
	- 다른 클래스에서 이 메소드를 호출 할 수 있도록 접근권한을 부여함
- static
	- 자바가상기계(JVM-이 프로그램을 시작시키는)가 프로그램을 시작시킬 때, main() 함수를 포함한 클래스에 대한 객체 생성없이 접근하기 위한 목적 
- void
	- main 함수는 반환값이 없음 -> return X
- String[] args
	- args는 문자열 배열로써 프로그램 실행 시에 명령행 인자(command lin parameter)로 전달된 문자열들을 포함

---

# 연결문서 

# 참고 사이트
