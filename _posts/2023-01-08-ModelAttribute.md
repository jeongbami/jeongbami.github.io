---
title:  ModelAttribute
date: 2023-01-08 17:22:00 +/-0900
categories: [studyplace, Hello-Spring!]
tags: [spring]     # TAG names should always be lowercase
---

# ModelAttribute

- Model에 자동으로 저장되는 annotation
- @ModelAttribute가 붙은 변수는 addAttribute가 필요 없다.
- 반환 타입 혹은 컨트롤러 메소드의 매개변수에 적용 가능하다.

1. 참조형 매개변수
    - @ModelAttribute 생략가능
        - 컨트롤러 매개변수 :: RequestParam : 기본형 / String일 경우 생략되어 있다고 볼 수 있음.
        - 또 참조형일 때는 ModelAttribute가 생략 되어있다.

# WebDataBinder

- controller에서 요청 받은 값은 vaㅋlue값이 String이다. 이 때 실제 객체에 들어갈 값이 int라면  `webdatabinder` 이 그 사이에서 타입을 변환시키고 데이터에 대한 값이 결과값에 유효한 범위인지 데이터 검증을 한다. 
- 이후 binderResult에 값을 전달해 데이터로 쓰인다.
- WebDataBinder는 Binder받을 객체 바로 뒤에 선언되어야 한다.

    ```java
    public String main(@ModelAttribute Mydate date, BinderResult result)
    ```
    
- binderResult에는 타입 변환 및 검증을 거치며 나타난 애러를 result값에 담고 있다. 이를 활용하여 error를 검증하고 싶은 변수 뒤에 선언한 후 `FieldError` 타입의 변수를 선언 후 result에 들어있는 method를 통해 console창에 자세한 오류 정보를 담을 수 있다.

    ```java
    public String catcher(Exception ex, BindingResult result) {
        System.out.println("binderResult : "+  result);
        
        FieldError error = result.getFieldError();
        // 에러를 자세히 보는 방법 
        System.out.println("code = " + error.getCode());
        System.out.println("filed = " + error.getField());
        System.out.println("msg = " + error.getDefaultMessage());
        
        ex.printStackTrace();
        return "yoilError";
        }
    ```

    ```console
     binderResult : org.springframework.validation.BindException: org.springframework.validation.BeanPropertyBindingResult: 1 errors
     
     Field error in object 'myDate' on field 'day': rejected value [aa]; codes [typeMismatch.myDate.day,typeMismatch.day,typeMismatch.int,typeMismatch]; arguments [org.springframework.context.support.DefaultMessageSourceResolvable: codes [myDate.day,day]; arguments []; default message [day]]; default message [Failed to convert property value of type 'java.lang.String' to required type 'int' for property 'day'; nested exception is java.lang.NumberFormatException: For input string: "aa"]
     
     code = typeMismatch
     filed = day
     msg = Failed to convert property value of type 'java.lang.String' to required type 'int' for property 'day'
     ```
