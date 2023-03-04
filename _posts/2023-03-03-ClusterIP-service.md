---
title: Service - ClusterIP
date: 2023-03-02 17:00:00 +/-0900
categories: [iaas, Hello-k8s!]
tags: [kubernetes, k8s,docker]     # TAG names should always be lowercase
---


# ClusterIP Type
##

### 1) Cluster type의 service 생성 및 단일 endpoint 노출
#### Service ClusterIP 생성 방법

1) yaml파일 (Service)
    
```yml
apiVersion: v1
kind: Service
metadata:
  name: order
  namespace: namespace
  labels:
    service: order
spec:
  type: ClusterIP
  selector:
    service: order  # Service가 order인 label을 가진  pod 집합을 선택
port:
  - port: 80    # 요청을 받을 port
  targetPort: 8080  # service가 order인 pod에서 container가 lisntening하고 있는 port를 조회하여 입력 
```

2) Service에 필요한 Deployment 생성

```yml
spec:
  replicas: 2
  selector:
    matchLabels:
      service: order
    template:
      metadata:
        labels:
          service: order    # 위와 같은 labels
    spec:
      container:
      - name: order
        image: yoonjeong/order:1.0
        ports:
        - containerPort: 8080   #Service targetPort와 같은 port 
```
- payment Service 생성시 payment Deployment도 함께 생성
 
3) endpoints
- endpoints를 조회시 각 pod들의 endpoint가 조회된다.
- 만약 selector와 매치되는 pod의 집합이 없는 경우에는 servicIP로 요청이 실패한다.
- 모든 요청은 service의 endpoint로 수신하게 되고 pod로 전달하기 때문에 endpoint에 선언되어있지 않은 ip로는 요청을 할 수 없다. 요청에 실패하는 오류를 만나면 꼭 endpoints를 조회해보아야 한다.

#### ClusterIP의 역할과 특징

##

### 2) Cluster 내부에서  Service IP 또는 Service 이름으로 통신하기
#### 환경변수 접근
#### DNS server
#### MSA 환경에서 다른 namespace에 있는 service domain 접근