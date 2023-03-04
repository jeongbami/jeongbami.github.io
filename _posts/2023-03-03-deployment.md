---
title: deployment
date: 2023-03-03 11:00:00 +/-0900
categories: [iaas, Hello-k8s!]
tags: [kubernetes, k8s,docker]     # TAG names should always be lowercase
---


# Deployment
##
### pod의 삭제와 재배포를 k8s에게 위임
- pod 배포 자동화를 위한 오브젝트로  ReplicaSet + 배포전략이 담겨있다.
- 다양한 배포전략을 제공하고 ReplicaSet이 아닌 Deployment로 pod을 배포하고 관리한다.
- roll back과 roll out( 새로운 배포) 때 ReplicaSet 생성을 대신 해주는 역할을 한다.

### 전략
- Recreate 
    - 이전의 Pod를 모두 종료하고 새로운 Pod를 replicas 만큼 생성 
    - 롤아웃 진행중 하나씩 지워서 replicas를 모두 삭제 한뒤 재생성 한다
    - 이 때 모두가 삭제되는 순간이 발생하는데 이 때 service를 운영 중이라면 downTime이 발생 할 수 밖에 없다.
    - 개발 단계에서 사용하기엔 유용하지만 이 후 서비스 배포 단계에서는 사용하기엔 적합하지 않다.
- RollingUpdate (점진적 배포)
    - 새로운 Pod 생성과 이전 pod 종료가 동시에 일어나는 방식이다.
    - 모든 이전의 pod이 종료될 때까지 하나씩 지우고 하나씩 생성하는 방식이다.
    - 이 때에는 pod가 종료되는 순간에 존재하지 않기 때문에 안전하다. 
    - 서비스 다운 타임 최소화 시키지만 동시에 실행되는 pod의 개수가 replicas를 넘게 되므로 컴퓨팅 리소스가 더 많이 필요할 수 있다. 
    >  Rollingupdate 속도 제어 Option
    - maxUnavailable
        - 처음 deployment 할 때 rollingupdate를 수행하는 동안 유지해야 하는 최소 pod의 개수 지정
        - 최소 pod 유지 비율은 = 100- maxUnavailable값
            - ex: replicas:10, maxUnavailalbe: 30%
            1) 이전 버전의 replicas중 3개는 즉시 삭제한다.
            2) 10개 중 3개는 삭제된 상태로 롤링 업데이트를 진행한다.
            3) pod의 개수는 최초 7개는 유지 되어야 한다
    - maxSurge
        - 롤링 업데이트를 수행하는 동안 허용할 수 있는 최대 pod의 개수이다.
        - replicas의 개수를 늘려서 배포하는 것을 말한다.
        - 최대 pod 허용 비율 = maxSurge 값
            - ex: replicas:10 maxSurge: 30%
            1) deployment때 최소 3개까지 즉시 scale up 할 수 있다.
            2) 롤링 업데이트를 하는 순간 새로운 pod가 3개 생성되어 replicas는 13개로 증가한다.

### rollback
- Deployment는 rollOut history 를 Revision #으로 관리한다.
- 숫자가 커질수록 최신순이다.
- `kubectl rollout undo deployment <deployment-name> --to-revision=1`


### Deployment 생성과 실행
- ReplicaSet의 이름
    - `<deployment-name>-<pod-template-hash>`
- ReplicaSet이 생성하는 pod의 이름
    - `<deployment-name>-<pod-template-hash>-<임의의 문자열>`

    여기서 두 `<pod-template-hash>` 값은 같은 값을 띄고 있다.
> Pod Template이 변경되면 pod-template-hash값도 변경되며 이는 새로운 ReplicasSet이 생성되는 것을 알 수 있다. 

1. pod replicas 변경
    - ` k scale deployment/my-app -n bami --replicas=5`
1. pod Template image 변경
    - `k set image deployment my-app -n bami my-app=yoonjeong/my-app:2.0`
2. pod Template label 변경

