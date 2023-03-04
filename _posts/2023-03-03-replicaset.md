---
title: ReplicaSet
date: 2023-03-02 12:00:00 +/-0900
categories: [iaas, Hello-k8s!]
tags: [kubernetes, k8s,docker]     # TAG names should always be lowercase
---

 # ReplicaSet
 ##
 ### pod 복제본을 생성하고 관리한다.
- N개의 Pod를 생성하기 위해 생성 명령을 N번 실행 할 필요 없다.
- ReplicaSet 오브젝트를 정의하고 원하는 Pod 개수를 replicas 속성으로 선언한다.
- 클러스터 관리자 대신 pod수가 부족하거나 넘치지 않게 Pod수를 조정한다 
    :: Pod 관리


### 결함에 내성을 가진 서비스 환경 만들기
- pod에 문제가 생겼을 때 
    - pod는 즉시 종료되고 클라이언트 요청을 처리할 수 없다. 
    - 클러스터 관리자가 24시간 monitoring 하고 정상 복구 해야한다.
    - N개의 pod를 실행하고 이상 상태에 대비할 필요가 있는데 누가 하는게 좋을까 ?
- " 소프트웨어는 내결함성을 가진다"
    - 소프트웨어나 하드웨어가 필해가 발생하더라도 소프트웨어가 정상적인 기능을 수행 할 수 있어야 한다는 뜻.
    - 모든 소프트웨어는 이러한 기능을 구성해야한다.
    - google은 이런 기능을 사람의 개입없이 내결함성을 가진 소프트웨어를 구상한다.
    > 이 기능을 하는 것이 ReplicaSet이다.

### ReplicaSet의 역할
- ReplicaSet을 이용해 Pod 복제 및 복구 작업을 자동화 한다.
- 클러스터 관리자는 ReplicaSet을 만들어 필요한 Pod 개수를 쿠버네티스에게 선언한다.
- 쿠버네티스가 ReplicaSet 요청서에 선언된 replicas를 읽고 그 수만큼 Pod 실행을 보장하게 된다. 

### Replicas, Pod Selector, Pod Template 
- Replicas : 원하는 replicas의 개수
- Pod Selector : 어떤 Pod를 replicas 할 것인지 label value
- Pod template: 따로 pod.yaml을 생성하지 않아도 되는 template

로 구성 되어 있다. 이 세가지를 정의해서 ReplicaSet을 배포하게 되면 pod를 자동으로 생성해준다. 

```yml
apiVersion: app/v1       # Kubernetes API 버전
kind: ReplicaSet         # 배포하고자 하는 object type
metedata:             # 오브젝트를 유일하게 식별하기 위한 정보 
  name: blue-app-rs    # object name
  labels:             # object 집합을 구할 때 사용할 label
    app: blue-app
spec:        # user가 원하는 pod의 상태 정의
  selector:       # ReplicaSet이 관리해야하는 pod를 선택하기 위한 label query / 선언된 label를 가진 pod들만 복구하게 된다.
    matchLabels:      # label name 선언 
      app: blue-app    #(key-value)형태 
  replicas:             # 실행하고자 하는pod복제본 개수 
  template:          # app .yaml 파일을 그대로 적어주면 됨.
    metadata:       # 이미 kind - Replicaset 에 "pod"의 template 이므로 kind는 정의할 필요 없다 
      labels:       # label을 꼭 정의해야 하는데 이유는 replicaset에 선언된 selector의 label이름과 일치해야 하기 때문이다. 
        app: blue-app
    spec:
      container:
      - name:
        image:
```

### Replicaset 의 변경된 PodTemplate
- 기존에 replicas를 3개로 deployment 한다.
- 3개의 pod가 생성된다.
> yaml 파일을 replicas 2개로 선언해본다 (선언 후 재배포 해야함.)
- 하나의 pod를 삭제한다 
- rs는 pod개수를 유지하려는 속성이 있기 때문에 하나의 pod가 삭제된다.

> yaml파일을  replicas 4개로 선언해본다.(선언 후 재배포)
- 하나의 pod가 생성되며 이 때 다른 변경된 yaml파일 형식이 있다면 적용되어 생성된다.
- 재배포 후 replicas 수를 하향시 마지막에 생성된 pod들 먼저 삭제된다.

<h4>이는 pod replicaset이 상태가 변경 되더라도 기존의 pod에는 영향을 주지 않으며 변경된 이 후에 생성된 pod들만 영향을 끼친다. <h4>

### replicaSet의 Rollback
1. ReplicaSet이 생성한 파드로 통신하기  
    - 롤백을 위해 ReplicaSet의 PodTemplate 변경 (Pod는 변경하지 않고 Template만 변경한다.)
    - 기존의 pod Label을 새로이 fix될 이름으로 변경을 해준다.  
        - 에러난 pod를 기존의 replicaset으로 부터 분리시키는 작업.
        - 이 때 생성되어있는 pod는 Rs의 label범주를 벗어나기 때문에 owner object가 존재하지 않는다. (분리작업)
    - 새롭게 배포 (Rollback)
        - label name을 변경한 label name로 바꿔주고 배포한다.

        - error 발생
        ```shell
         k apply -f replicaset.yaml -n bami
         k get pod -L app -n bami
         k port-forward rs/myapp-replicaset -n bami  8080:8080
         for i in {0..5}; do curl -vs localhost:8080; done
         ```

         - 새롭게 배포될 label이름으로 변경 
         
        ```shell
         k set image rs/myapp-replicaset -n bami  my-app=my-app:1.0
         k get rs -n bami -o wide
         k label pod myapp-replicaset-phjrl app=to-be-fixed --overwrite
         k label pod myapp-replicaset-px2s5 -n bami app=to-be-fixed --overwrite
         k label pod myapp-replicaset-txq6r -n bami app=to-be-fixed --overwrite
         ```

         - 바뀐 라벨명 확인 후 scale up/down으로 재배포 실행 
         
         ```shell
         k get pod -n bami --show-labels.
         k scale rs/myapp-replicaset -n bami --replicas=0
         k scale rs/myapp-replicaset -n bami --replicas=3
         ```
        - label명이 바뀐 것을 확인하고 이전의 app이 이전의 label 에서 각각 running중인 상태인 것을 확인
        
        ```shell
         k get pod -n bami --show-labels -o wide
         k logs myapp-replicaset-8lhns -n bami
        ```
2. replicas 수를 조정하는 통한 롤백
    - ReplidcaSet이 생성한 pod수를 0으로 변경
    - `kubectl scale rs <RSNAME> --replicas 0`
    - pod Template를 변경한다
    - `kubectl sclae rs <RSNAME> -- replicas <number-of-pods>`

### 결론
- ReplicaSet을 이용해 Pod 복제본을 생성하고 관리한다. 
    - 여러 노드에 걸쳐 배포된 pod의 Up/Down 상태를 감시하고 replicas 수만큼 실행을 보장한다.
- ReplicaSet의 spec.selector.matchLabels 는  Pod template 부분의 tspec.template.metadata.labes와 같아야한다
- 선언되지 않은 replicas는 default 1이다.
- 하지만 replicaset은 pod의 관리만 할 뿐 loadbalancing이 일어나지는 않는다.

##
> 기존의 replicaSet에 포함되지 않은 미리 배포된 pod도 해당 pod의 label과 matchLabel name과 같게 해주면 replicaSet의 관리 범위에 들어오게 된다.

