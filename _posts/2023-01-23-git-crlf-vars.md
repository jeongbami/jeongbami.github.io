---
title:  git window/mac 개행 문자 차이로 인한 upload issue
date: 2023-01-23 14:30:00 +/-0900
categories: [variation, some var things]
tags: [git, spring, mac, windows, crlf]     # TAG names should always be lowercase
---



# 개행문자

windows에서는 line ending으로 CR(Carriage-Return, \r) 과 LF(Line-Feed, \n)을 사용하고, Unix 계열은 LF만 사용한다. 이는 실제 코드는 변경된 것이 없는데 소스의 CR/LF때문에 변경으로 착각하여 commit을 하게 될 수 있으며 변경 로그를 보거나 merge마다 문제가 생긴다.

이런 문제를 방지하기 위해 OS가 달라도 문제 없도록 CRLF 처리 방법을 결정해야 한다.

# 해결책

os별 CRLF 차이로 인한 문제를 막기 위해 별도의 처리 방법을 권장한다.

1. windows
    windows에서는 CRLF를 사용하므로 저장소에서 가져올 때 `LF -> CRLF`로 변경하고 저장소로 내보낼 때는 `CRLF -> LF`로 변경하도록 설정한다.

    ```bash
    git config --global core.autocrlf true
    ```

2. Linux, Mac os
    Unix 계열은 LF만 사용하므로 input으로 설정한다

    ```bash
    git config --global core.autocrlf input
    ```

