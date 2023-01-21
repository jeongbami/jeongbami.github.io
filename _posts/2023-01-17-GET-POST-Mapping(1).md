---
title:  RequestMapping->GET/POST
date: 2023-01-17 18:09:00 +/-0900
categories: [studyplace, Hello-Spring!]
tags: [spring]     # TAG names should always be lowercase
---


# RequestMapping / POST 방식

- POST 방식으로 Mapping 할 때는  아래와 같은 tag를 적어주어야 한다.
    @RequestMapping(values="/register/save", method=RequestMethod.POST)
    - 그러나 spring 업데이트로 PostMapping이 생김
        @PostMapping("/register/save) --> 4.3 부터 가능

# 회원가입 화면이 하는 일 ?

- 회원가입 화면은 실질적으로 하는 일이 없다.  submit을 통한 처리만 있을 뿐 "회원 가입 창" 자체는 하는 일이 없음.g
- 그래서 굳이 @GetMapping이나 method를 만들어 view를 return하는 등의 수고스러움은 필요 없다.

    - view 화면만을 띄워주기 위한 servlet-context 설정
        : servlet-context.xml ( web관련 설정 페이지 )에 view controller를 추가해주기

        ```xml
        <view-controller path="/register/add" view-name="registerForm"/>
        ```

        path에는 @RequestMapping의 value 값을 , view-name은 registerForm.jsp의 이름을 적어주면 된다. 

        :view-controller는 GET요청만 허용한다.

# spring으로 전환 후 오류 메세지 출력

1. `return "redirect:/register/add?msg="+msg;`
    model을 추가하지 않고 URL재작성 방법인 rewriting 방법을 통해 URL에 오류 메세지를 출력한다
2. Model model 선언 / model.addAttribute("msg" ,msg) / return "redirect:/register/add"
    model에 오류메세지를 추가하여 출력해주기
    오류 메세지를 여러개 출력하기
- 가끔 msg가 표시 되지 않을 때

    ```js
    <i class="fa fa-exclamation-circle"> ${URLDecoder.decode(param.msg)}</i>
    ```
    
    :: URLDecoder에서 decoding을 해주어야한다
    :: 이는 java class로 `<%@ page import="java.net.URLDecoder"%>` 를 inport 해주어야함.