---
title:  "*.xml"
date: 2023-01-15 18:56:00 +/-0900
categories: [studyplace, Hello-Spring!]
tags: [spring]     # TAG names should always be lowercase
---
d

프로젝트 실행 -> Server > web.xml  -> WEB-INF > web.xml

1. web.xml
    - Server > Tomcat > web.xml
        : 모든 web-app의 공통 설정
    - src > main > webapp > WEB-INF > web.xml
        : 해당 프로젝트에 대한 개별 설정
        : servlet 및 URL 등록
            - Servlet 등록 ---spring --> @Controller
            - Servlet 등록 --- servlet --> @WebServlet 
            - URL연결       ---spring--> @RequestMapping
        : <servlet>원격 프로그램 등록</servlet> 
        : <servlet-mapping>URL pattern 등록 </servlet-mapping>



