---
title:  MVC 패턴 4) DefaultServlet(Servlet) & DispathcerServlet(spring)
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