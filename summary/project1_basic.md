# 웹의 동작(HTTP 프로토콜의 이해)

- HTTP (Hypertext Transfer Protocol)
    - 서버와 클라이언트가 인터넷상에서 데이터 주고받기 위한 protocol
    - 계속 발전하고 있다. 버전 별 차이를 정리해보는 것도 좋을듯 하다.
- HTTP 작동방식
    - 장점
        - 불특정 다수를 대상 서비스에 적합
        - 클라이언트와 계속 연결된 상태가 아님
        - 그래서 클라이언트와 서버 간의 최대 연결 수보다 더 많은 요청과 응답 처리할 수 있음
    - 단점
        - 무상태 (stateless). 연결을 끊기 때문에 클라이언트의 상태를 알 수 없는 것
        - 그래서 Cookie와 같은 기술 등장
- URL (Uniform Resource Locator)
    - 인터넷 상 자원 위치
    - 특정 웹 서버의 특정 파일에 접근하기 위한 경로 혹은 주소
    - URI: 요청하는 자원의 위치 명시

# FE와 BE

- Brower의 동작
    - 브라우저의 렌더링 과정
        - HTML 파싱 → DOM Tree
        - CSS 파싱 → CSS Tree(CSS Object Model)
        - DOM TREE + CSS Tree → Render Tree 조합 → Render Tree 배치 → Render Tree 그리기
        - 화면의 배치와 어떻게 색칠할지 과정을 거침
    - HTML과 CSS는 따로따로 파싱되기 때문에 화면이 움직일 때, 재사용가능한 레이아웃은 재사용하지 않을까? 생각함
- 웹서버
    - 웹 서버란
        - 보통 SW를 말하지만, SW가 동작하는 컴퓨터이다.
        - 메인기능
            - client가 요청하는 HTML이나 Resource를 전달
    - 종류
        - Apache, Nginx 등
            - Apache는 오픈소스 대부분 컴터에서 동작함
            - Nginx는 더 적은 자원으로 더 빠르게 데이터를 서비스. 오픈소스임 인기 많아짐
- WAS
    - 동적인 콘텐츠 제공
    - 웹서버 기능 포함
    - 규모가 커질수록 웹서버와 was를 분리
        - 자원 이용의 효율성, 장애 극복, 유지보수 등의 편의성
    

### HTML-FE

- HTML Tags
    - 목적에 맞게 검색해서 사용
- HTML Layout tag
    - 레이아웃 구성을 위한 태그
        - header
        - section
        - nav
        - footer
        - aside
    - 구글링하면 다양한 레이아웃 예시를 확인가능

- class와 id 속성
    - ID
        - 고유한 속성으로 HTML 당 하나만 존재
    - Class
        - HTML안에 중복으로 사용가능
        - 여러 태그에 동일한 class를 적용하여 사용가능 → 일관성
        - 하나의 태그에 공백을 기준으로 여러 Class를 정의 가능
        - 

### 개발환경 설정 - BE

Tomcat 다운받기 및 설치하기 

- dynamic web project란
    - 웹 프로젝트에는 static과 dynamic 두가지 존재.
        - 차이점은 웹 프로젝트가 클라이언트에 제공하는 리소스 차이
    - WAS를 만들 때 사용
    - target 설정에서 WAS를 설정. 톰캣을 사용하기 때문에 다운받은 톰캣의 위치를 설정

- web module 이란?
    - eclipse에서 dynamic web project를 만들 때, web module의 context root와 content directory를 설정하게 되서 뭘까 검색함
        - context root: 웹 어플리케이션 구분용
        - content directory: 리소스가 위치하는 폴더
        - http://localhost:8080/firstweb/HelloServlet 형태가 됨
        - http://localhost:8080/{프로젝트이름}/{URL Mapping 값}
    - 배포 가능한 단위
        - 하나 이상의 서블릿, JSP 그리고 정적 콘텐츠를 모두 포함(HTML, 이미지 등)
        - web.xml(deployment descriptor) 도 포함
            - deploy 시 servlet의 정보를 설정
            - 정보) servlet이 매핑 URL, servlet이 무엇을 제공하는지
    - 빌드 시 WAR(web application archive) 파일에 저장됨

### 서블릿이란

- java web application의 구성요소 중 동적인 처리를 하는 프로그램
- 서블릿은 WAS에서 동작하는 Java 클래스
- HttpServlet 클래스 상속
    - HTTP 통신과 관련된 중복 작업 처리
    - HttpServletRequest 클래스와 HttpServletResponse 클래스의 객체를 파라미터로 받음
    - service 메소드 8가지 분기
        - doPost(), doGet(), doPut(), doDelete() 등등
- 왜 HttpServlet 클래스를 상속할까
    - 일반 클래스가 서블릿 클래스가 되려면 필요한 API를 사용해야 한다. GenericServlet클래스가 Servlet 인터페이스와 ServletConfig인터페이스를 구현하기 때문이다.
    - 두 인터페이스를 구현해야 서블릿이 된다.
        - Servlet 인터페이스 **(생명주기)**
            - init(), service(), destroy()
        - ServletConfig 인터페이스
            - 초기화 로직
    - HttpServlet에는 HTTP에 더 특화되어 있다.
- 버전에 따른 Servlet 스펙 작성법
    - 3.0 스펙 이상
        - web.xml 사용안함
        - annotation 사용
    - 3.0 스펙 미만
        - servlet 등록 시 web.xml 등록

참고: https://lordofkangs.tistory.com/m/37

