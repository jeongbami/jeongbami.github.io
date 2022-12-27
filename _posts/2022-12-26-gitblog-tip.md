---
title: gitblog - ruby
date: 2022-12-26 21:56:00 +/-0900
categories: [tip, Hello-blog!]
tags: [spring]     # TAG names should always be lowercase
---



# ruby install
- git commit 과정에서 deployment 오류
    + ruby install에서 오류가 난다면 ? 
        * gemfile.lock  확인하기 
        gemfile.lock는 gem install 혹은 bundle 명령어로 불필요한 file까지 설치되는 경우가 있음. 그럴 때 build에서 오류가 난다.
        이 때는 gemfile.lock 파일을 삭제 후 다시 bundle install을 해준 후 add file edit한 후 commit 하면 정상 설치 된다.