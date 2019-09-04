---
title: Github page & Hexo 를 이용한 블로그 생성
date: 2019-09-04 21:10:18
tags: hexo
---

드디어 첫 블로그를 만들었다.😊
이 블로그를 통해 개인 프로젝트나 개발공부에 관련된 글을 써나가려고 한다.

첫 포스트는 [Hexo](https://hexo.io/)라는 프레임워크를 소개하고 [Github page](https://pages.github.com/)를 통해 간단하게 hosting 하는
방법에 대해 이야기하려고 한다. Gatsby, Hugo 등 여러 정적 웹사이트 생성기들을 찾아보다가
사용성이 가장 심플하고 속편한? [Hexo](https://hexo.io/)에 정착했다!
Gatsby는 react 기반이라 어렵진 않았지만 아예 새로 웹사이트를 개발하는게 낫겠다 싶을 정도로 복잡하고
손볼것이 많았고 Hugo는 왜인지 theme가 잘 적용되지 않았다..
(아마도 우분투 root path에 이상이 생겨 무언가 꼬인듯하다😰)

그러던 와중 발견한 [Hexo](https://hexo.io/)로 10분만에 뚝딱 이 블로그를 만들어버렸다.
불필요한 패키지설치 없이 간결하고 몇안되는 명령어로 포스팅 생성, markdown 기반으로 아주아주 간단하게 작성 가능하다는 점이 맘에든다.👍

---

## Hexo를 사용한 블로그 생성

Hexo는 Node.js로 되어있으며 작성시 **HTML, Markdown, AsciiDoc** 등을 이용해서 사용가능한 블로그 프레임워크이다.

### **장점**

1. 명령어로 간편하게 포스트 생성이 가능하다.
2. 사용성이 아주아주 쉽다.
3. 빌드 속도가 빠르다.
4. 한글 문서를 지원한다.

Gatsby에 비해 theme가 많지 않다는 점이 조금 아쉽지만(20190904 기준 270items)
커스터마이징 또한 어렵지 않아서 문제될 것이 없다.

---

_이제 블로그를 만들어보자!_
👇

### 요구사항

- Node.js (최소 6.9이상)
- Git

위 두가지는 사전에 설치가 되있어야 하며, 설치되어있다면 생략하고 넘어가자
Hexo 설치

```bash
$ npm install -g hexo-cli
```

### 블로그 생성

```bash
$ hexo init blog
$ cd blog
$ npm install
```

`> hexo init [생성할 폴더 이름]` 으로 벌써 블로그가 만들어졌다.

```bash
$ hexo server
```

위 명령어를 통해 로컬에서 생성된 블로그를 확인해본 뒤 **테마를 적용**해보자.
_([localhost:4000](localhost:4000))_

### 테마적용

themes 폴더에 있는 기본테마를 사용해도 괜찮지만
Hexo 사이트에 있는 다양한 테마 중 하나를 적용해보길 추천한다.

<span style="color: #EE7785">Hexo theme</span> : [https://hexo.io/themes](https://hexo.io/themes)

적용 방법은,

1. `root` 디렉토리에서:

```bash
$ git clone https://github.com/probberechts/hexo-theme-cactus.git themes/cactus
```

2. config.yml 파일 수정:

```bash
theme: cactus
```

간단한 수정으로 테마는 이미 적용되었다.
추가로 커스터마이징을 원한다면 `config.yml` 파일을 수정하거나
해당 테마의 `document`를 참고하자.

### 포스트 작성

커스터마이징까지 끝냈다면 포스트를 작성해보자
아주 간단하다.

```bash
$ hexo new post post_name
```

<u>**blog > source > \_posts > post_name.md**</u>
위 경로에 해당 이름의 md 파일이 생성된 것을 확인할 수 있다.
마크다운 문법을 이용해서 포스트를 작성해주면 된다.

### 빌드하기

블로그 운영을 위해 배포를 해보자.

```bash
$ hexo generate
or
$ hexo g
```

배포를 완료하면 `public` 폴더가 생성되는데 요 폴더만 있으면 호스팅을 할 수 있다.

- Github page
- Netlify
- Heroku
- ...

여러 서비스 중 [Github page](https://pages.github.com/)를 통해 호스팅을 진행했다.
github여서 접근성이 쉽고 간단하기 때문이다.

### Github page를 이용해서 호스팅하기

1. 배포할 github `repository`를 만든다.
   일반 프로젝트의 저장소를 만들때와 방법이 조금 다르다.
   저장소 이름을 입력할 때 `username.github.io`로 만들어야 한다.

2. deploy 설정하기
   해당 저장소로 public 파일을 push하기 위해 `_config.yml`파일을 수정해야 한다.

```bash
...
url: https://username.github.io/ #만들어진 깃험 페이지 주소
...

deploy:
   type: git
   repo: 생성한 저장소 깃헙주소
```

위처럼 설정을 변경해준뒤 다음과 같이 배포를 진행한다.

```bash
$ hexo generate
$ hexo deploy

or

$ hexo g -d #위의 명령어 두 줄을 줄여서 빌드와 배포를 한 번에 할 수 있다.
```

`username.github.io` 로 접속해서 빌드한 결과물을 확인할 수 있다.

> ! 여기서 주의할 점은,
> 배포한 결과물 즉, `public` 폴더만이 repository에 올라간다는 것이다.
> 그렇기 때문에 내가 작성한 포스트, 설정, 테마 등등의 파일을 따로 백업해두어야 한다.
> 해서, github page 를 이용해 만든 저장소가 아닌 코드 자체를 관리하기 위한 저장소를 따로 만들어 관리하고있다.
> 관리방법이 좀 까다롭다.. 다음 포스트에 정리해 놓았다. [Hexo 코드 백업하기](http://localhost:4000/2019/09/04/Hexo-code-manage/)

### 폴더구조

```bash
- root
   ├ source #설정파일
   │ └ _posts #포스트 md파일
   │ └ something #페이지
   ├ themes #테마

```

### 이슈

글은 길어보이지만 따라하면 채 10분이 걸리지 않는다. 아마도..
다만 배포를 진행하면서 약간의 이슈가 발생했었는데 변경이 적용이 안되고 아래의 에러가 발생했다.🤔

```bash
$ ERROR Deployer not found: git
```

이 문제는 `hexo-deployer-git` 플러그인을 설치해서 해결할 수 있었다.

```bash
$ npm i hexo-deployer-git --save
```

위의 문제 외의 배포가 잘 적용되지 않는 경우가 있는데
이럴때는 `clean` 를 진행해주고 재배포하면 해결된다.

```bash
$ hexo clean
$ hexo g -d
```

🙌
