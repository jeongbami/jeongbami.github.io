---
title:  Servlet 과 JSP (2) URL-Pattern , El문
date: 2023-01-01 14:16:00 +/-0900
categories: [studyplace, Hello-Spring!]
tags: [spring]     # TAG names should always be lowercase
---

# DefaultServlet & DispathcerServlet
@Webservlet
- URL-Pattern에 따른 Mapping 방법\
- Servlet Context를 통해 Request된 서블릿 이름을 통해 @Webservlet에 등록된 URL-Pattern과 mapping시킨다.
- "/"로 설정된 ServletContext는 모든 요청을 뜻하는데 이는 DefaultServlet으로 매핑된다.
    : 이것이 후에 Spring으로 연결되고 RequestMapping으로 통홥되어 DispatherServlet으로 발전된다.

 @RequestMapping
- web.xml에 등록된 <app-servlet>에 등록된 patter으로 request된 모든 요청을 받는다.

# EL (Expression Language)

- 문법: ${ 값 }의 형태로 *.jsp파일에서 간단하고 편리하게 쓸 수 있게 해준다.
- STS에서 deploy를 할 때 임시 파일이 생성되는 폴더
    1. Run > Run Configurations > Deploy= "경로"
        - 해당 경로로 이동 후 `cd ../tmp0/work/Catalina/localhost/ch2/org/apache/jsp`
    2. .java, .jsp의 파일이 자동 생성되어 있음을 알 수 있다.
    3. 가끔 .jsp파일을 수정했을 때 web에서 반영이 되지 않는다면 이 폴더의 임시 파일을 삭제 후 다시 deploy 해주면 즉각 반영됨을 알 수 있다. (STS내부에서 server>tomcat 우클릭 > Clean Tomcat work Directory를 클릭하면 같은 효과.)
    4. 임시파일을 자동생성 및 삭제로 보아 첫 jsp파일을 deploy할 때는 init() method를 통한 하나의 객체를 생성 하기 때문에 컴파일 과정의 처리 시간이 필요함을 알 수 있고 그 이후로는  init()을 재활용 함으로서 처리 시간이 단축됨을 알 수 있다. 자동파일을 삭제 후 다시 실행하면 새로운 init()객체가 만들어 지기 때문에 처리 시간이 필요해진다.

- <%=값%> , ${값}

    ```java
    //1
    id=<%=request.getParameter("id")%> <br>
    //2
    id=${pageContext.request.getParameter("id")} <br>
    ```

    1. 1번은 java 문법으로 request라는 기본객체 즉 local variable이 쓰일 수 있으므로 request.getParameter가 가능하다.
    2. 하지만 el문에서는 지역변수가 쓰일 수 없으므로 el문이 쓰일 수 있는 저장소인 pageContext > page 에 저장되어 있는 기본객체인 Request를 호출 해 사용 해야한다.

- java의 "1"+1 el의 "1"+1

    1. Java: 1이 "1"으로 변환되어 "1"+"1"로 해석되어 출력값은 "11"이 된다.
    2. El: "1"이 1로 변환되어 1+1로 해석되어 출력값이 "2"가 된다.
        - 여기서 "11"이 되고싶으면 "1"+="1"로 표기해야한다.

- null

    1.Java : null 자체가 출력.
    2. El: 숫자 0 혹은 "" (빈문자)로 출력.