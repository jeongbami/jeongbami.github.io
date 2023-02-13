---
title: DispathcerServlet 파헤치기 
date: 2023-02-06 19:12:00 +/-0900
categories: [studyplace, Hello-Spring!]
tags: [spring]    
 # TAG names should always be lowercase
---

<h>DispacherServlet 파헤치기 </h>


> Request

> DispathcerServlet

```markdown
! Method 호출
- HandlerMapping(mappedHandler)
: 요청을 받으면 어떤 method가 처리하면 좋을지 데이터를 넘긴다. HandlerMapping은 Key와 Value로 되어있고 Key는 URL / values는 method를 담고 있다.
    ! Method 반환
```
> DispatcherServlet

```markdown
! Controller 호출
- HandlerAdapter
: 이 Adapter가 존재하면서 Controller와 느스한 연결을 갖게되고 이는 변경에 유리한 조건을 갖추게 한다. HandlerAdapter는 Controller에 맞는 Adapter를 연결해주며 큰 틀을 수정하지 않아도 된다.
    ! View값 반환 
```
> DispatcherServlet

```markdown
! View값 전달 
    - ViewResolver
    : InternalResourceViewResolver에 따라 접두사 / 접미사가 붙은 view url를 전달
    ! View URL 반환
```
> DispatcherServlet
- JstlView를 통해 전달한다. (== HandlerMapping과 같은 역할)
- Model(data)를 전달하며 해당 값의 view를 호출한다.
- .jsp는 model을 가지고 응답 결과를 만든 후 client에게 응답
> Response
