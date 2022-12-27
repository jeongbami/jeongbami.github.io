---
title: 변수 (variable)
date: 2022-12-23 11:04:00 +/-0900
categories: [studyplace, Hello-java!]
tags: [java]     # TAG names should always be lowercase
mermaid: true
---


# 변수 variable

- 선언 위치에 따른 변수
    +클래스 영역 
        *클래스 변수 (class variable)
            1) static변수, 공유 변수라고도 불림 
            2) 변수 type 앞에 static이 붙음
            3) 생성시기
             클래스가 메모리에 할당될 때 자동으로 생성된다. (==클래스가 필요할 때 / 객체를 만들기 전 /설계도가 올라갈   때 
             ` > CPU    <----2.작업---->     RAM(메모리)    <---- 1. loading       SSD(저장장치)  ----> 3. save           SSD`

        *인스턴스 변수 (instance varialbe)
        1) 생성시기 
        클래스 내의 변수로  {% raw %}객체가 생성될 때{% endraw %}  변수가 선언된다 
        > 고로 "객체"란 instance var의 집합체라 말할 수 있다. 프로그래 관점에서 인스턴스 변수를 묶어놓은 것 그 이상 그 이하도 아니다! {: .prompt-info }

- 클래스 변수와 인스턴스 변수의 차이점
>  class var는 ram에 loading / save 가 되는 개념이고 instance var는 객체생성이 필요하다.

    + 클래스 영역 이 외의 영역 (method 영역)
        * 지역 변수 (local variable)