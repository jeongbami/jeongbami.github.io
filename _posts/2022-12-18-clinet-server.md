---
title: client와 server 
date: 2022-12-17 15:00:00 +/-0900
categories: [studyplace, Hello-Spring!]
tags: [spring]     # TAG names should always be lowercase
---


1. 클라이언트와 서버는 역할에 따라 구분된다

    Client
      서버를 요청하는 애플리케이션(프로그램)
            client application (url)
            client computer
    Server
            서비스를 제공하는 애플리케이션(프로그램)
             server application (WAS:tomcat)
            server computer

2. 서버의 종류
     제공하는 서비스에 따라 달라진다
        1. email server
        2. file server
        3. web server (browser로 받을 수 있는 모든 활동)

    - 하나의 PC에는 여러 서버가 존재하기 때문에 ip만으로는 구분하기 어렵다. 이때 필요한 것은 port이다. port는 server와 binding 되어 있어야 하며 listening 상태일 때 client의 요청을 받을 수 있다.
    - 대표 port 번호 
        Email server = 25
        File server = 22
        Web server = 80 (생략가능함)
        0~1023는 예약 포트로 지정되어 있다.

3. WAS?
    웹 애플리케이션을 서비스를 제공
    server에 program을 설치하고 사용자가 이용할 수 있게 한다.
    client --->원격 호출 --> WAS --> server program 실행 및 이용

    3-1) Server(Tomcat)
        client의 요청
           -> Server : Thread pool에 있는 Thread 하나가 실행된다 
            -> Service : Request된 protocol을 해석해 Connector를 실행한다
            -> Engine(Catalina) Host(domain name)를 해석해 맞는 웹을 실행한다
            -> Context : Web appclication / STS의 project가 해당됨 서로 영향을 주지 않는 독립적인 공간에서 운영된다.
            -> Servlet : 작은 server program (==controller) 
            



1. Request
    - HttpServletRequest
        URL을 통한 요청으로 server내에서 매개변수로 이용된다.
            getScheme()
            getRequestURL()
            getServerName()
            ...
            +
            getQueryString()
            등 여러 메소드가 있음.
                getQueryString()은 추가 전송되는 데이터로 server에서 getParameter()로 값을 받는다.



