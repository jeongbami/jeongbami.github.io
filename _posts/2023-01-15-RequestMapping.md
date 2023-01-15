---
title:  Make Register Form
date: 2023-01-15 18:09:00 +/-0900
categories: [studyplace, Hello-Spring!]
tags: [spring]     # TAG names should always be lowercase
---


# 경로 설정 파일

- src > main > webapp > resources > 정적파일.html

1. web 관련 설정파일
    - src > main > webapp > WEB-INF > spring > appServlet > Servlet-context.xml 
    - resources Mapping 태그폼을 바꾸어주면 된다.
2. non-web 관련 설정파일
    - src > main > webapp > WEB-INF > spring > root-context.xml

# 회원가입 창

```js
<form> 
    <input type = text>
    <input type = password>
    .
    .
    .
    .
    <input type = submit>
</form>
```

1. <form> : 데이터를 사용자에게 입력 받기 위한 양식
    - attribute
        - action : 전송할 URL (default==자기 자신에게 전송 (화면 refresh))
        - method : "get(==default)" - Body가 없어 query string으로 전송되는 방식 / "post"
2. <input> : 사용자가 값을 입력
3. <submit> : form에 action attribute의 주소로 전송
