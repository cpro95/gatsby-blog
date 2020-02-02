---
title: Github Pages 사용법
date: 2020-02-02 21:02:33
category: github
draft: false
---

![github](./github_image.jpg)

## 나만의 홈페이지 만들기

NodeJS, ReactJS를 만지다 보면 내가 만든 SPA앱을 온라인에 호스팅하고 싶은데요. 제가 쓰는 호스팅 도메인은 netlify.com입니다. 무료이고 속도도 제일 빠르더라구요.

netlify는 heroku와 함께 프론트엔드, 백엔드 무료 서비스의 대주자라고 생각하는데요. 잘 이용하시면 나만의 웹앱을 꽁짜로 온라인 퍼블리싱 할 수 있습니다..

물론 상업적으로 론칭할려면 AWS 같은 유료 호스팅 서비스로 가야겠지만요.

## 나만의 홈페이지인데 블로그를 만들고 싶다면

ode나 React를 배우게 되면 홈페이지도 그냥 HTML로 만들기가 뭔가 손해 같은데요. 배운게 아까워서. React 진영에는 블로그로 Gatsby가 기능도 많고 많이 사용됩니다. 그래서 배워볼 겸 사실 하나 만들어 봤습니다. netlify에 호스팅했었는데 한번 방문 해 보세요.

cpro95.netlify.com

사실 Gatsby 블로그 시스템도 성능이나 속도면에서 좋지만 좀 무거운 면이 없지 않아서 다른 걸 생각했었는데 우연히 reddit을 보다가 새로 발견한게 있는데 James K Nelson의 "npx create-react-blog"입니다. React용 라우터인 Navi를 만든 사람 같은데 블로그 템플릿도 같이 만들어서 배포했더라구요. 조금 만져 보니까 가볍고 쉽다는 느낌이 들었습니다.

그래서 드디어 내 계정의 github.io에 호스팅할 블로그로 결정하게 되었습니다.

cpro95.github.io

## Github Pages 본격 사용법

### 리포지터리 만들기

일단 github.io에 정적 사이트를 호스팅 할려면 먼저 리포지터리를 만들어야 겠죠? 일단 github.com 에서 자신의 아이디로 된 리포지터리를 github pages용으로 만듭니다. 제 경우 아이디가 cpro95이기 때문에 cpro95.github.io 이란 좀 긴 리포지터리를 만들었습니다. 이제 터미널에서 클론 해보죠

```
git clone https://github.com/cpro95/cpro95.github.io.git
```

username.github.io 의 호스팅은 master 브랜치에 저장된 데이터만 정적 호스팅됩니다. 로컬에서 데이터 수정후 remote 로 push 하면 github.io가 자동으로 호스팅 합니다.

여기서 헷갈리는게 있는데 github pages는 사용자 페이지와 프로젝트 페이지가 있습니다. 사용자 페이지는 username.github.io 와 같이 자신의 github.io 페이저 첫 부분입니다. 사용자 페이지는 master 브랜치를 통해서만 편집할 수 있구요.

프로젝트 페이지는 쉽게 설명하면 본인이 만들고 있는 웹앱이나 홈페이지가 있는데 이걸 자신의 github 프로젝트 페이지 밑에 정적으로 호스팅하고 싶을때 사용하는 페이지입니다.

예를 들어 카카오톡 링크보내기 웹앱을 만들었고 github.io에 호스팅하고 싶다면 즉, kakao-cpro95.git 이라는 프로젝트를 github pages로 정적 호스팅하고 싶다면https://cpro95.github.io/kakao-cpro95/ 란 웹경로로 호스팅 됩니다.

프로젝트 페이지는 gh-pages란 브랜치를 만들고 package.json 의 homepage란을 적절히 작성하면 gh-page deploy로 바로 퍼블리싱할 수 있습니다.

gh-page란 브랜치가 자동으로 자신의 github.io 밑에 퍼블리싱되구요.

```
#install gh-pages package
npm install --save gh-pages
```

#### package.json 수정하기

```
...
"homepage": "https://cpro95.github.io/kakao-cpro95",
...
﻿
"scripts" : {
    "predeploy" : "npm run build",
    "deploy" : "gh-pages -d build"
}
```

gh-pages 로 발행하고 싶을때는 npm run deploy 를 실행하면 자동으로 predeploy도 실행 되면서 자신의 프로젝트 페이지 밑에 사용자 페이지가 만들어 집니다.
