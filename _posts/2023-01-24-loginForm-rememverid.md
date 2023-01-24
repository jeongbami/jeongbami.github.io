---
title: loginForm - remember ID 
date: 2023-01-24 20:45:00 +/-0900
categories: [studyplace, Hello-Spring!]
tags: [spring]     # TAG names should always be lowercase
---


# login 화면에서 "아이디 기억" 활성화하기

1. if (cookie==!null) : 쿠키가 있다면?
    1.1 기억한 id를 "id입력란"에 넣어준다.

    ```js
    <input type = "text" name ="id" placeholder="이메일 입력" autofocus value="{기억한id}">
    ```

    1.2 "아이디 기억"에 checked 해준다.

    ```js
    <input type ="checkbox" name= "rememverId" checked/>
    ```

    - 먼저 쿠키가 있을 때의 최종 결과물.jsp를 만들어 준다 .
    - 그 후에 cookie 값의 여부에 따른 뷰를 설정해준다.
        : 이렇게 하면 결과값에 더 빨리 도달 할 수 있음
        : 그리고 chrome의 개발자모드에서 임시로 cookie를 만들어 test 할 수 있다.
        (application>Cookies>http:/localhost)
2. if(cookie==null) : 쿠키가 없다면?
