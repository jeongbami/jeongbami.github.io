---
title: paasta>vars.yml
date: 2022-12-17 19:38:00 +/-0900
categories: [PaaS-TA, operation]
tags: [paasta, paas]     # TAG names should always be lowercase
---

deployment_name: "paasta" # Deployment Name
network_name: "default" # VM에 별도로 지정하지 않는 Default Network Name
haproxy_public_ip: "203.255.255.124" # HAProxy IP (Public IP, HAproxy VM 배포시 필요)
- bosh core ip
haproxy_public_network_name: "vip" # PaaS-TA Public Network Name
haproxy_private_network_name: "private" # PaaS-TA Private Network Name (vSphere use-haproxy-public-network-vsphere.yml 포함 배포시 설정
필요)
cc_db_encryption_key: "db-encryption-key" # Database Encryption Key (Version Upgrade 시 동일 KEY 필수)
cert_days: 3650 # PaaS-TA 인증서 유효기간
private_ip: "10.244.0.34" # Proxy IP (Private IP, BOSH-LITE 사용시 설정 필요)
uaa_login_logout_redirect_parameter_disable: "false"

아래 ip는 portal ui ip.nip.io
uaa_login_logout_redirect_parameter_whitelist: ["http://portal-web-user.203.255.255.123.xip.io","http://portal-web-user.203.255.255.123.xip.io/callback","http://portal-web-user.203.255.255.123.xip.io/login"] # 포탈 페이지 이동을 위한 UAA Redirect Whitelist 등록 변수
uaa_login_branding_company_name: "PaaS-TA R&D" # UAA 페이지 타이틀 명
uaa_login_branding_footer_legal_text: "Copyright © PaaS-TA R&D Foundation, Inc. 2017. All Rights Reserved." # UAA 페이지 하단 영역 텍스트
uaa_login_links_passwd: "http://portal-web-user.203.255.255.123.xip.io/resetpasswd" # UAA 페이지에서 Reset Password 누를 시 이동하>는 링크 주소
uaa_login_links_signup: "http://portal-web-user.203.255.255.123.xip.io/createuser" # UAA 페이지에서 Create Account 누를 시 이동하>는 링크 주소
uaa_client_portal_redirect_uri: "http://portal-web-user.203.255.255.123.xip.io,http://portal-web-user.203.255.255.123.xip.io/callback" # UAA Portal Client의 Redirect URI 지정 변수, 포탈에서 로그인 버튼 클릭 후 UAA 페이지에서 성공적으로 로그인했을 경우 이동하는 URI 경로

