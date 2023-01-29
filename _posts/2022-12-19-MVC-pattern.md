---
title: MVC 패턴 1) 관심사의 분리
date: 2022-12-17 15:03:00 +/-0900
categories: [studyplace, Hello-Spring!]
tags: [spring]     # TAG names should always be lowercase
---


# 서론
1. 예제 == YoilTeller
    - 날짜를 입력하면 요일을 알려주는  이 method는 여러개의 관심사를 가지고 있다. 
    (여기서 관심사는 개발자가 관심을 가지고  '해야 할 일' '해야 할 작업'으로 해석한다.)

1) 입력 : 날짜를 입력한다 .
2) 작업 : 요일을 계산한다
3) 출력 : 계산한 요일을 출력한다

# 본론
-  객체지향 프로그래밍(Object Oriented Programming)의 5대 원칙이 있다.
    1) S    =   SRP (단일 책임의 원칙)
    - '하나의 method는 하나의 책임(관심사)만 맞는다'
    2) O
    3) L
    4) I
    5) D
    
    - 예시로든 YoilTeller는 위의 첫번째 원칙을 거스르고 있다.  그래서 좋은 설계라고 할 수 없다.
    - 좋은 설계를 하기 위해서는 분리를 하는것이 중요하다.
        * 관심사를 분리한다.
        * 변하는 것 , 자주 변하지 않는 코드를 분리한다. (common code/uncommon code)
        * 공통 (중복) 코드를 분리한다. (분리하여 따로 빼둔다)
        
        1) 공통 코드의 분리
            - 입력
            입력은 통상적으로 request.getparameter()를 쓴다. 이는 공통적으로 쓰는 method로 본다.
            
            ```java
            public void main(HttpServletRequest request) {
                String year = request.getParameter("year");
                String year = request.getParameter("month");
                String year = request.getParameter("day");
            }
            public void main(String year, String month, String day){
                int yyyy = Integer.parseInt(year);
                int mm = Integer.parseInt(month);
                int dd = Integer.parseInt(day);
            }
            
           public void main(int year, int month, int day){ //String을 int로 자동변환해준다.(spring이 해줌)
                Calendar cal = Calndar.getInstance();
                cal.set(year, month - 1, day);   
            }
            ```
            : 이렇게 되면  입력의 부분이 사라진다.
            
            2) common/uncommon을 분리.
            변하지 않는 것, 자주 변하지 않는 코드를 분리. 처리와 출력 부분을 분리한다
            -> 결론적으로 관심사가 분리된다.
            
            ```java
            //처리 
            public void main(int year, int month, int day) { //String을 int로 자동변환해준다.(spring이 해줌)
            Calendar cal = Calndar.getInstance();
            cal.set(year, month - 1, day);
            
            int dayOfWeek = cal.get(Calendar.DAY_OF_WEEK);
            char yoil = "일월화수목금토".charAt(dayOfWeek);
            
            //출력
            // 이하 출력 부분  
            .
            .
            .                  
            }
            ```
            
            이를 예로 들었을 때 같은 method 안에서는 "yoil"이라는 변수를 호출 할 수 있지만 처리/출력 부분을 분리 될 때는 method를 자유롭게 호출하지 못한다. 이 때 처리와 출력 부분을 연결 해주는것이 "Model"이다.
            
            > 이렇게 연결(Model) / 처리(Controller) / 출력 (View)을 구분 한 것을 MVC Pattern 이라 부른다.


# 결론
- Spring MVC pattern
request   -> DispathcerServlet(입력) - 결과를 저장할 객체생성  ->  Model  -> Controller(처리) 
response <------ View(출력) ----- DispathcerServlet(입력) <------------------------------   Model <----- 결과 저장  ---┘
- 순서
    1) Request 
    2) DispathcherServlet
        - 입력을 받고 변환, Model생성 (new Model();)
    3) Controller
        - Model model 매개변수로 받는다. 어떠한 View를 통해 출력 할 지를 지정해준다 (return값 )
        > 이는 상황에 따른 view를 지정해 줄 수 있다는 장점을 가진다 (error page가 한 예이다.)
    4) View
        - return 값으로 저장된 View로 전달. (xxx.jsp)
    5) Response