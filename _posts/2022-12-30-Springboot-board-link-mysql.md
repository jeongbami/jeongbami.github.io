---
title: springboot를 이용한 게시판 및 mysql 연동 - mac과 localhost 연결 issue 
date: 2022-12-29 10:01:00 +/-0900
categories: [studyplace, Hello-Spring!]
tags: [spring]     # TAG names should always be lowercase
---


1. 아무리 재설치를 하고 brew services start mariadb를 해도 mariadb상태가 stopped에서 started로 변경되지가 않았다.

MySQL을 삭제한다고 했지만 잔존 파일이 남아 있었다.

3.해결방법
: 설치한 mysql, mariadb를 삭제 후 재설치를 한다. 이 과정에서 잔존 파일을 무조건 제거해야한다. 
	•	brew services stop mariadb
	•	brew remove mariadb
	•	brew cleanup -> 이러면 일단 brew list 시 mariadb 혹은 mysql이 사라진 것을 볼 수 있습니다. 여기서 바로 재설치 하지 말고 잔존 파일을 찾습니다.
	•	저는 아래 사진과 같이 mysql, mariadb를 finder에 검색해서 전부 다 지웠습니다
	•	
	•	이렇게 지웠으면 이제 my.cnf 파일을 찾아서 지워야합니다.😤 (이것때매 고생함 ㅠ)
	•	->저의 경우에 my.cnf 파일 경로가 /opt/homebrew/etc/my.cnf 이렇게 있었습니다. my.cnf.d, my.cnf.default와 같이 my.cnf가 포함되어 있으면 다 지웁니다
	•	이제 다시 brew install mariadb 을 통해 재설치합니다.
	•	brew services start mariadb로 실행하고 brew services list를 보면 mariadb가 started인 것을 볼 수 있습니다.


```shell
 sh_j@jeongbam-book  ~  brew install mariadb
==> Downloading https://ghcr.io/v2/homebrew/core/mariadb/manifests/10.9.4
Already downloaded: /Users/JEONG/Library/Caches/Homebrew/downloads/5f5ea53491fad13c123906ed44b8f404113c393c2418253cf0028cf28b9a3a2c--mariadb-10.9.4.bottle_manifest.json
==> Downloading https://ghcr.io/v2/homebrew/core/mariadb/blobs/sha256:ceb1ff5294
Already downloaded: /Users/JEONG/Library/Caches/Homebrew/downloads/9899003f70670f3f07f1c5b420a7ae872a3796466eca37c331943443eac7655d--mariadb--10.9.4.arm64_ventura.bottle.tar.gz
==> Pouring mariadb--10.9.4.arm64_ventura.bottle.tar.gz
==> /opt/homebrew/Cellar/mariadb/10.9.4/bin/mysql_install_db --verbose --user=sh
==> Caveats
A "/etc/my.cnf" from another install may interfere with a Homebrew-built
server starting up correctly.

MySQL is configured to only allow connections from localhost by default

To restart mariadb after an upgrade:
  brew services restart mariadb
Or, if you don't want/need a background service you can just run:
  /opt/homebrew/opt/mariadb/bin/mysqld_safe --datadir=/opt/homebrew/var/mysql
==> Summary
🍺  /opt/homebrew/Cellar/mariadb/10.9.4: 926 files, 175.8MB
==> Running `brew cleanup mariadb`...
Disable this behaviour by setting HOMEBREW_NO_INSTALL_CLEANUP.
Hide these hints with HOMEBREW_NO_ENV_HINTS (see `man brew`).
 sh_j@jeongbam-book  ~   brew services restart mariadb
==> Successfully started `mariadb` (label: homebrew.mxcl.mariadb)
 sh_j@jeongbam-book  ~  brew services list
Name    Status  User File
mariadb started sh_j ~/Library/LaunchAgents/homebrew.mxcl.mariadb.plist
tomcat  none
 sh_j@jeongbam-book  ~  mysql -uroot
ERROR 1698 (28000): Access denied for user 'root'@'localhost'
 ✘ sh_j@jeongbam-book  ~  sudo mysql -u root
Password:
Sorry, try again.
Password:
Sorry, try again.
Password:
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 4
Server version: 10.9.4-MariaDB Homebrew

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> use mysql
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
MariaDB [mysql]> select user, host, plugin from mysql.user
    -> select user, host, plugin from mysql.user;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near 'select user, host, plugin from mysql.user' at line 2
MariaDB [mysql]>
MariaDB [mysql]>
MariaDB [mysql]>
MariaDB [mysql]>
MariaDB [mysql]>
MariaDB [mysql]> select user, host, plugin from mysql.user;
+-------------+---------------------+-----------------------+
| User        | Host                | plugin                |
+-------------+---------------------+-----------------------+
| mariadb.sys | localhost           | mysql_native_password |
| root        | localhost           | mysql_native_password |
| sh_j        | localhost           | mysql_native_password |
|             | localhost           |                       |
|             | jeongbam-book.local |                       |
+-------------+---------------------+-----------------------+
5 rows in set (0.002 sec)

MariaDB [mysql]>


MariaDB [mysql]> set password for 'root'@'localhost' = password('1234');
Query OK, 0 rows affected (0.018 sec)

MariaDB [mysql]> flush privileges;
Query OK, 0 rows affected (0.010 sec)
```

# trobleshooting
- BEANS를 못찾는다고 자꾸 뜨거나 .. jdbc 어쩌고 드라이버어쩌고 뜨면 내가 mysql로 연결했는데 mariadb를 찾진 않는지 Driver와 내가 맵핑한 db가 맞는 타입인지 그리고 localhost는 8080임을 잊지 않았는지 생각 
