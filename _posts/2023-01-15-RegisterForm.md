---
title:  Make Register Form
date: 2023-01-15 18:09:00 +/-0900
categories: [studyplace, Hello-Spring!]
tags: [spring]     # TAG names should always be lowercase
---


# 경로 설정 파일

- src > main > webapp > resources > 정적resource.

1. web 관련 설정파일 : Servlet-context.xml
    - src > main > webapp > WEB-INF > spring > appServlet > Servlet-context.xml 
    - resources Mapping 태그폼을 바꾸어주면 된다.
2. non-web 관련 설정파일 : root-context.xml
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

1. `Form` : 데이터를 사용자에게 입력 받기 위한 양식
    - attribute
        - action : 전송할 URL (default==자기 자신에게 전송 (화면 refresh))
        - method : "get(==default)" - Body가 없어 query string으로 전송되는 방식 / "post"
            : Query string으로 지정된 이름은 input tag의 name=""이다.
2. `input` : 사용자가 값을 입력.
3. `submit` : form에 action attribute의 주소로 전송
4. `{param.Values}` : jsp에서 넘어온 값들 중 name이 같은 이름은 중복되어 전송 되기 때문에 모든 값이 넘어오지 못한다. 그 때 EL문에 있는 param.Values를 사용하면 그 값들을 배열에 담아 저장한다. param.Values[0],[1],,로 출력 할 수 있다. 
5. `onsubmit` : form형식을 제출할 때 호출 될 function을 지정하는 곳
    - "return FUNCTION_NAME(this) { }" 으로 작성
    - this 는 onsubmit이 속해있는 <Form> 자체
    - 원래는 function() { return function(this) }; 로 호출 해야하는데 생략하고 return 값만 적어준다.
    - true (form 전송)  / false (form 전송 안함 ) 


# spring 전환 시 msg 표시 에러
- .jsp에서 쓰인 ${}는 Template Literal으로 Browser에서 쓰이는 JS 언어이다. 
- 서버에서 쓰이는 EL문과 같은 형태를 띄고 있다.
- 하지만 RAM에서 파일을 읽을 때 서버를 먼저 읽고 브라우저로 넘어가기 때문에 프로그램에서는 EL문으로 인식한다
- 그래서 이를 보완하기 위해 EL문으로 한 번 더 감싸주어야 한다.

# <c:url>
- context-root 자동 추가
    context-root는 자주 변하는데 <c:url>은 그 root를 자동으로 추가 해주기 떄문에 form의 action태그에서 쓰인다.
    <c:url value="">
- session id 자동 추가 