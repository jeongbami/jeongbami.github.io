---
title: HTTP(Request/Response)
date: 2022-12-17 15:03:00 +/-0900
categories: [studyplace, spring]
tags: [spring]     # TAG names should always be lowercase
---


1. 프로토콜 (protocol)
    서로 간의 통신을 위한 약속 규칙
    주고 받을 데이터에 대한 형식을 정의 한 것

    ex ) 편지의 받는 사람/보내는 사람 주소 등 format이 정해져있는 형태

    - HTTP(Hyper Text Transfer Protocol)
        text를 전송하기 위한 procotol
            특징 
                1. 단순하고 읽기 쉽다 - 텍스트 기반의 protocol
                이는 사람이 읽고 수정하기 쉬운 형태로 human readalbe 형태라고 말함.
                2. 상태를 유지하지 않는다(stateless) -> 클라이언트 정보를 저장하지 않기 때문
                여러번 요청해도 client의 정보를 알 수 없다
                3. 확장 가능하다 
                    HTTP 응답 메세지에는 header / body로 이루어져 있고 표준 형식이 있다. 
                    이는 n개(여러개)로 작성되어 질 수 있어 사용자가 직접 수정 또는 추가가 가능하다 하여 custom header라 불린다.
                
    - HTTP 메세지 (응답메세지)
        상태라인(state line) - header가 시작되기 전 가장 첫번째줄. connector, 상태코드 + 상태 결과 등을 포함하고 있다.
            상태코드 
                1xx :   Infermational
                2xx :   Success
                3xx :   Redirect
                4xx :   Client Error
                    client가 요청을 잘못함.
                5xx :   Server Error
                    요청은 잘 됐으나 server가 처리하다가 에러남.
        Header
            를 구분하기 위해서 공백줄 하나가 추가되어있다.
        Body

    - HTTP 메세지 (요청메세지)
        1. GET
            요청라인(Request line)
            Header
            Body가 없고 URL의 QueryString으로 정보를 전달한다.
          
          
            - Server를 통해 resources를 얻어오기 위해 설계 (읽기/read)
            ex ) 검색엔진에서 검색단어 전송에 이용 
            - url을 통해 정보를 전달하므로 소용량이며 노출되므로 보안에 취약하다 
            - 데이터 공유에 유리하다.
            
        2. Post
            요청라인
            Header
            Body  : 서버에 전송할 data
           
           
            - Server에 데이터를 올리기 위해 설계. (쓰기/write)
            예 ) 글쓰기, 로그인, 회원가입, 파일첨부 등..
            - 전송 데이터 크기의 제한이 없어 대용량이 가능하고 보안에 유리하다. (HTTP+TLS (암호화)를 통한 HTTPS://일 때 보안에 유리한것임.)
            - 데이터 공유에는 불리하다.

        웹 > 개발자모드 > network > 요청한 task  클릭 > Header / Response 등 메시지를 볼 수 있음.