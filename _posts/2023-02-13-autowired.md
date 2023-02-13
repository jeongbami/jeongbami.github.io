---
title: Spring DI 흉내내기 3 - Autowired,Resource
date: 2023-02-13 19:45:00 +/-0900
categories: [studyplace, Hello-Spring!]
tags: [spring]    
 # TAG names should always be lowercase
---

# Autowired 
- map에 저장되어있는 객체(by Type)와 자동 연결해주는 annotation
+ Autowired에 해당하는 method랑 같이 쓰인다.
    - map에 저장된 객체의 iv중에 @Autowired가 붙어 있으면 map에서 iv타입에 맞는 객체를 찾아서 연결해주는 Method
    
```java
Class Car {
    Engine engine;
    Door door;
}

Appcontext a = new Appcontext();
Car car = (Car)ac.getBean("Car");
Engine engine = (Engine)ac.getBean("Engine");
Door door = (Door)ac.getBean("Door");

// Car클래스에는 engine과 door가 선언되어있다.
// Appcontext 즉 객체 저장소에 세 개의 객체가 저장된다.
// 이 때 engine과 door는 car의 객체로서 참조를 해야한다

car.engine=engine;
car.door=door;
```

이렇게 수동으로 하는 방법이 아닌 자동으로 객체참조를 해주는 것이 Autowired이다.

```java
Class Car{
    @Autowired Engine engine;
    @Autowired Door door;
}
```



# Resource
- map에 저장된 Key값으로 찾아 연결해주는 annotation

```java
Class Car{
    @Resource Engine engine;
    // 특정적으로 이름이 지정되어있지 않다면 객체의 첫글자를 소문자로 바꾼 이름으로 자동 저장된다 
    // Engine -> engine
    @Resource(name=door2) Door door;
    //이름을 특별하게 지정해줄 수도 있다.
}
```