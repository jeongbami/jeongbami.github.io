---
title: cf CLI (service-broker)
date: 2022-12-23 14:38:00 +/-0900
categories: [cloud, Hello-cloud!]
tags: [cloud, cloudfoundry]     # TAG names should always be lowercase
mermaid: true
---



1.  개념파악 
    MySQL 설치를 통해 알아보기 
    == 명령어들이 어떤 역할을 하는지 알고 활용 해보기
       
       1. service broker 
            service를 사용하기 위해 만든 API
                1) `cf service-brokers`      사용할 수 있는 borker의 목록을 확인한다
                2) `cf create-service-broker username userpassword http:{mysql-broker-ip}:8080`
                        등록되어있는 service-broker가 없다면 생성해준다
                3) `cf enable-service-access`
        service broker 개발 환경
            1. Cloud Foundry instance에 대한 관리자 권한이 있어야 함.
                    `In order to run many of the commands below, you must be authenticated with Cloud Foundry 
                    as an admin user or as a space developer.`                                                   - cloudfoundry docs
                        cloud foundry에서 인증 받은 admin as SpaceDeveloper만 개발 가능 
            2. admin 계정에 등록된 mysql-service-broker 접근 권한 부여
                admin이 cf enalbe-service-access <service name> -o <org-name> 를 통해 access를 부여해야만 
                해당 org내의 사용자들이 접근 가능하다.
                 {: .prompt-tip}
        대체 방법
             ```shell
            cf create-user-provided-service my-db-mine -p '{"username":"admin","paasword":"pa55woRD"}'
            name         service         plan   bound apps   last operation   broker   upgrade available
            my-db-mine   user-provided 
            cf restage MY_APP
                    Downloaded go_buildpack
                    Downloaded r_buildpack
                    Cell 170ecd8b-ee1c-4cf1-9af6-8638046bae30 creating container for instance e93872c1-d317-4eda-a9ea-73ae73a1ec3d
                    Security group rules were updated
                    Cell 170ecd8b-ee1c-4cf1-9af6-8638046bae30 successfully created container for instance e93872c1-d317-4eda-a9ea-73ae73a1ec3d
                    Downloading app package...
                    Downloading build artifacts cache...
                    Downloaded build artifacts cache (43.1M)
                    Downloaded app package (52.6M)
                    -----> Java Buildpack v4.50 | git@github.com:cloudfoundry/java-buildpack.git#5fe41f89
                    -----> Downloading Jvmkill Agent 1.17.0_RELEASE from https://java-buildpack.cloudfoundry.org/jvmkill/bionic/x86_64/jvmkill-1.17.0-RELEASE.so (found in cache)
                    -----> Downloading Open Jdk JRE 1.8.0_352 from https://java-buildpack.cloudfoundry.org/openjdk/bionic/x86_64/bellsoft-jre8u352%2B8-linux-amd64.tar.gz (found in cache)
                    Expanding Open Jdk JRE to .java-buildpack/open_jdk_jre (0.7s)
                    JVM DNS caching disabled in lieu of BOSH DNS caching
                    -----> Downloading Open JDK Like Memory Calculator 3.13.0_RELEASE from https://java-buildpack.cloudfoundry.org/memory-calculator/bionic/x86_64/memory-calculator-3.13.0-RELEASE.tar.gz (found in cache)
                    Loaded Classes: 20985, Threads: 250
                    -----> Downloading Client Certificate Mapper 1.11.0_RELEASE from https://java-buildpack.cloudfoundry.org/client-certificate-mapper/client-certificate-mapper-1.11.0-RELEASE.jar (found in cache)
                    -----> Downloading Container Security Provider 1.19.0_RELEASE from https://java-buildpack.cloudfoundry.org/container-security-provider/container-security-provider-1.19.0-RELEASE.jar (found in cache)
                    Exit status 0
                    Uploading droplet, build artifacts cache...
                    Uploading droplet...
                    Uploading build artifacts cache...
                    Uploaded build artifacts cache (43.1M)
                    Uploaded droplet (95.8M)
                    Uploading complete
                    Cell 170ecd8b-ee1c-4cf1-9af6-8638046bae30 stopping instance e93872c1-d317-4eda-a9ea-73ae73a1ec3d
                    Cell 170ecd8b-ee1c-4cf1-9af6-8638046bae30 destroying container for instance e93872c1-d317-4eda-a9ea-73ae73a1ec3d

                    Restarting app spring-music in org bami-org / space bami-space as bami...

                    Stopping app...

                    Waiting for app to start...

                    Instances starting...
                ```
                {: .terminal}

        2. service & app
            service instance    
                cloud foundry에서 제공하는 서비스인 marketplace에 등록되어있는 resources를 service instance라 한다.
                Services >  service instances
                    marketplace :   cloud foundry service
                                         it provide resources services 
                                         that called 'service instance'
             service binding
                일부 서비스에 한해 제공된다.
                `cf bind-service MY_APP MY_DB`
                `cf bind-route-service DOMAIN`
                    1) Service instance bind App
                        deliver credentials for the service instace to the app
                        - binding app Manifest
                            service instace와 bind 하는 방법 외에  app의 manifest file을 읽어 bind하는 방법도 있다.  (during push)
                    2) Service instance bind Route
                
                
                
                사용 방법
                    1) cf create-service-broker     
                    2) cf marketplace
                    2) cf create-service SERVICE PLAN SERVICE_INSTANCE
                    3) cf apps
                    4) cf services
                    5) cf bind-service --

