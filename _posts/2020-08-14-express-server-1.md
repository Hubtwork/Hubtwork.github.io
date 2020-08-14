---
layout: post
title: Express js 로 Node 서버 만들기 ( 1 )
subtitle: Node.js 의 Express 프레임워크로 서버 만들기 ( 1 )
cover-img: /assets/img/path.jpg
tags: [node.js, express.js, express, node, server, express-generator ]
category: Node.js
---
<br>
<center>
  <h2>
    Express js 로 Node 서버 만들기 ( 1 )
  </h2>
</center>


---

<center>
  <h3>
    Intro
  </h3>
</center>


------

**Node.js** 는 v8 ( Javascript ) 기반의 서버-사이드 플랫폼입니다.  Node.js 기반의 웹 애플리케이션 프레임워크인 **Express Framework** 를 활용하면 <span style='color:skyblue'>GET, POST 와 같은 다양한 HTTP 동작들과 라우팅, 예외처리와 같은 복잡한 작업들을 간편하게 구현</span>할 수 있습니다. 또한 다년간 축적된 HTTP 유틸리티들과 미들웨어들을 지원하므로 빠르게 수준 높은 API 의 작성 또한 가능합니다. 본 시리즈는 **Express Framework 를 활용해 빠르게 API 서버를 구축하는 가이드라인을 제공**합니다.

<br>

---

<center>
  <h3>
    Node.js 설치하기
  </h3>
</center>


---

우선 OS 별로 터미널에서 다음과 같은 OS 패키지 매니저들을 통해 Node.js 의 설치를 진행합니다. 

< Linux >

```shell
# Install by curl
$ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
# Install by wget
$ wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```

< OSX >

```shell
# Install by Homebrew
$ brew install node
```

< Windows >

```shell
# Instal by Chocolatey
$ choco install nodejs-lts
```

<br>

---

<center>
  <h3>
    NPM ? 
  </h3>
</center>


---

위 과정을 통해 Node.js 를 설치했다면, **npm** 또한 함께 설치되었을 것입니다. npm 이란 **Node.js 패키지 매니저**인데, 누구든 Node.js 기반의 모듈들을 개발하고 이를 패키지화 하여 이를 통해 공유합니다. 우리가 생각하기에 이런 기능은 어떻게 구현할까? 싶은 대부분의 기능들은 이미 npm 상에서 다른 퍼블리셔들에 의해 제공되고 있고, 지속적으로 유지보수 되고 있다고 생각하면 됩니다. 누구든 npm 상에서 자신이 구현한 패키지를 공유하고 발전시킬 수 있습니다. 

위 Node.js 설치과정을 거쳤다면, 다음과 같은 명령어로 Node.js 와 npm  의 버전을 확인할 수 있습니다.

~~~bash
$ node -v
v14.4.0
$ npm -v
6.14.7
~~~

<br>

---

<center>
  <h3>
    IDE 선택하기 - VS code
  </h3>
</center>


---

이제 Node.js 를 활용한 프로그래밍을 진행하는 데에 있어 어떠한 **IDE** 를 선택할지 결정할 시간이 되었습니다. *IDE 는 프로그래밍 코드 편집기* 라고 생각하면 되는데 보통 **Sublime Text, Atom 등을 웹프로그래밍에 활용** 합니다.

필자는 보통 Node.js, Python 과 같은 언어로 작업을 진행할 떄, **VS code** 를 활용합니다. 다양한 확장 모듈들을 통해 원하는 대로 <span style='color:blue'>IDE 의 커스터마이징이 쉽고 간편하며, 가볍다는 장점</span> 때문에 한번 사용하면 끊을 수 없는 매력적인 IDE 입니다. 만약 따로 사용하는 IDE 가 없다면, 아래 링크를 통해 VS code 를 설치하도록 하자. 

<br>

<center><a href='https://code.visualstudio.com/'> VS code 설치 페이지 </a></center>

<br>VS code 를 설치했다면, 다음과 같은 화면이 우릴 반길 것이다. 이제 우리는 Node.js 와 만날 준비가 되었다. 좌측 탭의 박스 모양 아이콘을 눌러 **Extensions 에서 node, express 관련 확장프로그램들을 설치** 하면 Syntax Highlighting 과 같이 보다 가독성 높은 편집 환경을 만들 수 있을 것이다.

<center>
<img src="https://imgur.com/hvb9c6j.png" alt="Imgur" style="zoom:20%;" />
</center>

<br>

---

<center>
  <h3>
    Express js 프로젝트 생성하기
  </h3>
</center>


---

우리는 **express-generator** 를 활용해 빈 프로젝트를 생성할 것입니다. 이는 Express 서버를 구동하기 위한 모든 세팅을 마친 프로젝트 폴더를 생성해줍니다. 그럼 왜 이 모듈을 사용해야하느냐? Express 는 Intro 에서 설명한것과 같이 하나의 모듈입니다. 만약 node.js 프로젝트를 만들고, express 를 모듈로서 사용한다면 사용자가 일일이 필요 모듈들을 설치하고 Express 가 제공하는 프로젝트의 골격을 일일이 수정해야합니다.

**하지만 express-generator 는 Express 프레임워크를 사용하여 서버를 작성하기 위한 구조 및 필요 모듈들을 알아서 세팅해 프로젝트 폴더를 만들어줍니다.**

​	**express-generator ?**

> express-generator는 Express 웹프레임워 프로젝트를 손쉽게 시작할 수 있도록 도와주는 generator tool 입니다. 해당 툴을 이용하면, Express 프로젝트를 시작하기 위한 기본적인 세팅을 모두 마친 빈 프로젝트를 생성해줍니다. 

<br>

<h4>(1) npm 을 이용해 express-generator 를 설치해봅시다. </h4>

~~~bash
# -g : global option, 글로벌 옵션을 통해 설치한 패키지는 어디서든 사용할 수 있습니다.
$ npm install express-generator -g
~~~

<br>

<h4>(2) express 명령어를 이용해 프로젝트를 생성합시다. </h4>

~~~bash
# express '프로젝트명' [options]
$ express easy-api --view=ejs
...
create : easy-api/package.json
create : easy-api/bin/
create : easy-api/bin/www

change directory:
$ cd easy-api

install dependencies:
$ npm install

run the app:
$ DEBUG=easy-api:* npm start
~~~
<br>

~~~bash
# ls 명령어를 통해 해당 프로젝트가 생성되었음을 확인할 수 있습니다.
$ ls
easy-api
~~~

여기서 <span style='color:skyblue'>--view=ejs</span> 옵션은 뷰 엔진을 'ejs' 로 설정하겠다는 의미입니다. express-generator 의 default View Engine은 jade 를 채택하는데, 필자는 ejs 가 기존 html 의 골자 및 인자 전달을 활용하므로 보다 가독성 높고 적응하기 쉽다고 판단하여 이를 사용한 프로젝트를 생성했습니다. 이 두 엔진의 차이는 다음과 같습니다.

>- **ejs**
>
>- - html 태그 동일, <span style='color:skyblue'><% %>, <%= %>를 이용</span>해 서버와의 값의 전달이 가능하다.
>
>- **jade**
>
>- - Indentation 을 기반으로 한 html 코드를 사용한다.

<br>

<h4>(3) 프로젝트 폴더로 이동해 필요 패키지를 설치합니다. </h4>

프로젝트 폴더로 이동해 **npm install 명령어를 실행**하면, express-generator 가 정의한 package.json 의 Dependency 모듈들을 설치합니다. <span style='color:skyblue'>( npm install 명령어는 현재 터미널 상에서 커서가 위치해있는 프로젝트의 package.json 내의 dependencies 리스트를 참조해 패키지들을 설치합니다. )</span>
<center>
<img src="https://imgur.com/bneDlny.png" alt="Imgur" style="zoom:30%;" />
</center>

~~~bash
$ cd easy-api
$ npm install 
npm notice created a lockfile as package-lock.json. You should commit this file.
added 54 packages from 38 contributors and audited 55 packages in 1.654s
found 0 vulnerabilities
~~~

필수 패키지들이 모두 설치되었다면, 다음과 같이 프로젝트 폴더를 확인해봅시다.

<center>
<img src="https://imgur.com/7gyTS3U.png" alt="Imgur" style="zoom:50%;" />
</center>
<br>

<h4>(4) 서버 실행하기 </h4>

이제 기본적인 express 프로젝트의 생성이 끝났습니다. 그럼 우리의 서버를 한번 실행하고 확인해볼까요?

**npm start** 명령어를 이용해 서버를 실행하고 **http://localhost:3000** 으로 접속해봅시다. 그러면 다음과 같이 <u>express-generator 가 생성한 기본적인 프로젝트 인덱스 페이지</u> 를 보실 수 있을 겁니다.

~~~bash
$ npm start

> easy-api@0.0.0 start /Users/jaeheo/Desktop/express/easy-api
> node ./bin/www
~~~
<br>
<center>
<img src="https://imgur.com/27tTlR9.png" alt="Imgur" style="zoom:50%;" />
</center>

<br>

---

<h3>
   이번 포스트에서는 Node.js, Express 가 무엇인지 그리고 Express 프로젝트를 생성하고 실제 서버를 실행하는 방법까지 익혔습니다. 다음 포스트에서는 Express 프로젝트의 각 폴더, 파일들이 어떤 역할을 하는지 등을 알아보겠습니다.
</h3>