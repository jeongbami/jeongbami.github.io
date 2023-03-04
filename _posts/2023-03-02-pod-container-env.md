---
title: pod env 설정 및 실습 
date: 2023-03-02 10:00:00 +/-0900
categories: [iaas, Hello-k8s!]
tags: [kubernetes, k8s,docker]     # TAG names should always be lowercase
---


# create hello-app

## 실습 내용
### 쿠버네티스 값을 컨테이너로 전달할 환경변수와 값 참조 경로
  - POD_NAME: metadata.name
  - NAMESPACE_NAME: metadata.namespace
  - POD_IP: status.podIP
  - NODE_IP: status.hostIP
  - NODE_NAME: spec.nodeName

### Pod 템플릿 선언 시 컨테이너로 전달할 환경변수와 값
  - STUDENT_NAME: 본인이름
  - GREETING: STUDENT_NAME을 참조한 인삿말

