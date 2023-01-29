---
title:  RequestMapping을 class에 쓰기 
date: 2023-01-21 21:52:00 +/-0900
categories: [studyplace, Hello-Spring!]
tags: [spring]     # TAG names should always be lowercase
---


1. 클래스에 붙이는 @RequestMapping 

    ```java

2. @RequestMapping의 URL 패턴

3. URL Encoding
    - URL에 포함된 non-ASCII문자를 문자 코드 (16진수) 문자열로 변환하는 것 
        - ex: http://localhost:8090/ch2/login?id=정승혜
            - '정승혜' == non-ASCII 
            - URL 요청 -> URLEncoder.encode() -> 해당 ASCII에 맞는 16진수로 변환 -> server 전달 
            - server -> URLDecoder.decode() -> 응답 -> "정승혜" 
