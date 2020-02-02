---
title: 무료 SSL 인증서 발급, 갱신
date: 2020-02-02 21:04:86
category: ssl
draft: false
---

![ssl](./letsencrypt.svg)

개인적으로 라즈베리파이에 NodeJS API 서비스를 만들었는데 이게 netlify.com 에서 api call이 https방식만 가능해서 접속이 안됩니다.
그래서 라즈베리파이에서 쓰는 ASUS ROUTER DDNS 서비스에 SSL을 등록했는데, Let's Encrypt 무료 Cert는 3개월이 유효 기간이고 자동 갱신이 안됩니다.
그리고 ASUS ROUTER ADMIN Page 에서도 갱신이 안됩니다.

#### 직접 CERT 를 받기로 결정했죠

일단 라즈베리파이에 ssh로 접속해서 certbot을 설치합니다.

```bash
sudo add-apt-repository ppa:certbot/certbot﻿
sudo apt-get install certbot﻿
```

그리고 certbot을 실행해서 ssl을 생성합니다.
certbot 실행방식은 제 방식에서는 standalone방식입니다.

```bash
sudo certbot certonly --standalone -d cpro95.asuscomm.com
```

성공하면 /etc/letsencrypt 폴더 밑에 생성됩니다.
우리가 필요한거 cert.pem 과 privkey.pem 입니다. 이름은 나중에 변경하셔도 됩니다.

```bash
/etc/letsencrypt/live/cpro95.asuscomm.com/cert.pem
/etc/letsencrypt/live/cpro95.asuscomm.com/privkey.pem
```

혹시 포트트리거로 라우터 포트를 막아 놓으셨으면 80, 443 포트만 잠시 열어 두셔야 ssl cert를 발행할 수 있습니다.
certbot이 잠시 간이 웹서버를 돌려서 도메인 인증을 처리하기 때문입니다.
ssl cert를 발급 완료했으면 원하지 않는 포트는 삭제하시면 됩니다.

끝.
