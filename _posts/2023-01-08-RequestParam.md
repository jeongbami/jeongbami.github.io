---
title:  RequestParam
date: 2023-01-08 17:22:00 +/-0900
categories: [studyplace, Hello-Spring!]
tags: [spring]     # TAG names should always be lowercase
---

# RequestParam

1. @RequestParam(String)

    ```java
    public String main(String year)
    ```

    ==

    ```java
    public String main(@RequestParam(name="year" required=false) String year)
    ```

    와 같다. 평소 표기방법은 변수 호출 시 변수 타입 앞의 @~()가 생략 된 것. String year의 값이 없다면 null, 'year'라는 parameter만 넘어왔다면 '빈문자열'이 출력된다. (이 둘은 명백히 다름 ) 그렇다면 변수 선언과 동시에 @Requestparam을 쓰면 어떨까  ?

2. RequestParam(required=true, String year)

    ```java
    public String main(@RequestParam String year)
    ```

    ==

    ```java
    public String main(@RequestParam(name="year", required=true) String year)
    ```

    와 같다. 차이점은 required의 true/false값인데 이는 "Parameter의 값이 필수로 true 있어야한다 / false 없어도 된다."  를 의미한다.
    이 때 String year의 출력은 Null과 함께 400 Bad Error가 출력된다. 클라이언트 쪽에서 값을 입력하지 않은 오류로 판단한다. 그리고 'year'라는 변수명만 넘어왔다면 '빈문자열'이라는 "값"을 인식해 year=""로 출력된다. 전자는 error 후자는 error가 아닌 것.

3. RequestParam(required=fasle , int year)

    ```java
    public String main(@Requestparam(required=false) int year)
    ```

    int값에 대한 requied = false가 주어질 때는 다른 상황이다. 빈문자열이든 null값이든 int로 변환되는 과정이 불가능 하기 때문이다. 필수 조건이 아닐 때 parameter에 대한 값이 주어지지 않은 경우에는 500 error코드(값이 주어지지 않아도 되지만 null을 int로 변환시키지 못한 서버탓.), year에 빈문자열 값이 입력됐다면 값이 입력 되었지만 잘못된 타입이므로 400 error코드가 출력된다.

4. RequestParam(required=true , int year)

    ```java
    public String main(@RequestParam(required=true), int year)
    ```

    반대로 필수 조건일 때 parameter값을 주어지지 않았을 때 클라이언트 에러로 400 error 코드, 마찬가지로 값을 입력했으나 빈 문자열이라면 이 때도 값을 주었지만 잘못된 값을 주었으므로 (int인데 빈문자열(String)을 입력함) 클라이언트의 잘못으로 400 error코드가 뜬다.

- Required가 false일 때는 Defaultvalue 값을 입력해 주어야한다.
- 또한 required 가 true일 때는 사용자가 값을 입력하지 못할 수 있으므로 예외처리가 필수적이다. 이를 이용해 값을 입력할 수 있도록 유도하는 것이 필요하다.

