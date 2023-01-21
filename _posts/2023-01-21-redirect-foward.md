---
title:  redirect와 foward   (jsp&spring)
date: 2023-01-21 22:34:00 +/-0900
categories: [studyplace, Hello-Spring!]
tags: [spring]     # TAG names should always be lowercase
---


# jsp

1. redirect
    - 요청1
    - 응답1
    - 요청2
    - 응답2
    : 요청과 응답이 두 번 일어난다.
2. foward
    - 요청1
    - foward (request 객체)
    - 응답1

    : 요청과 응답이 각 각 한 번 일어난다.
    : 요청을 받은 파일이 controller 역할을 하고 , request 객체에 담아 (model) foward를 통해 응답한다(view). =>후에 spring의 MVC 모델로 채택.

# spring - redirect:/"" 

1. request

    ```java
    @Postmapping("/ch2/register/save") {
    return "redirect:/register/add" }
    ```

2. DispatcherServlet
    - Controller에게 전달
        : retrurn값을 전달
3. Controller
    - redirect될 View 이름을 Dispatcherservler에 반환
    - "redirect:/register/add"
4. RedirectView
    - Controller에게 받은 주소값을 전달 받음.
        : return 값을 응답.
        : redirect 응답 head 작성.
4. response
    - 생성된 redirect head를 view로 응답

# spring - return View

1. request

    ```java
    @Getmapping("/register/add") {
        return "registerForm"
    }

2. DispatcherServlet
    - Controller와 소통 ( 전달함 )
        : return값을 전달
3. Controller
    - InternalResourceViewResolver(appSesrvlet>servlet-context.xml에 있음)
        : view 이름을 전달
        : 그에 맞는 file url을 반환해줌.
        : response "/WEB-INF/view/registerForm.jsp"
        : DispatcherServlet이 전달 받음.
4. JstlView(Model)
    - DispathcerServlet에게 받은 응답값을 전달 받음
    - 전달받은 jsp data를 넘겨준다 (Model)
5. registerForm.jsp
    - 해당 값을 head/body를 만들어 response

# spring - foward:/""

1. request

    ```java
    @PostMapping("/register/save"){
        return "foward:/register/add";
    }
    ```

2. DispatcherServlet
    - Controller에게 전달
    : return 값을 전달 
3. Controller
    : foward될 View 이름을 Dispatcherservler에 반환
4. InternalResourceView
    : DispathcerServlet은 foward될 값을 전달
    : 내부적 요청
    : "register/add" 
    : 위와 mapping된 값을 찾음
5. Dispatcher <-> Controller (위의 과정과 같음)
    : "register/add"로 요청에 응한 method를 찾아 view 값을 전달하고 전달받음.
6. InternalResourceViewResolver
    : Dispatcher와 소통 및 응답.
    : "/register/add"로 mapping된 view값을 찾음.
    : "/WEb-INF/view/registerForm.jsp"
7. JstlView
    : 전달받은 jsp data를 넘겨준다 (Model)
8. registerForm.jsp
    : 해당 값을 head/body를 만들어 response.


    --- 실습 해야함 ( 230121 23:20)  영상 19:29--- 