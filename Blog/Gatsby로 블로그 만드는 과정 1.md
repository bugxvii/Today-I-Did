tags: #blog #gatsby #jekyll

---

[Gatsby Github](https://github.com/gatsbyjs/gatsby-starter-default)

### 1. `gatsby-cli` 설치:
```shell
$ npm install -g gatsby-cli
```

### 2. 프로젝트 생성
```shell
$ gatsby new my-default-starter https://github.com/gatsbyjs/gatsby-starter-default
```

error: 
```shell
~/Documents/github  gatsby new gatsby-starter-blog https://github.com/gatsbyjs/gatsby-starter-blog

info Creating new site from git: https://github.com/gatsbyjs/gatsby-starter-blog.git

Cloning into 'gatsby-starter-blog'...

 ERROR 

Command failed with exit code 128: git clone https://github.com/gatsbyjs/gatsby-starter-blog.git
gatsby-starter-blog --recursive --depth=1


  Error: Command failed with exit code 128: git clone https://github.com/gatsbyjs/gatsby-starter-blog.git 
  gatsby-starter-blog --recursive --depth=1
  
  - error.js:56 makeError
    [lib]/[gatsby-cli]/[execa]/lib/error.js:56:11
  
  - index.js:114 handlePromise
    [lib]/[gatsby-cli]/[execa]/index.js:114:26
  
  - task_queues.js:93 processTicksAndRejections
    internal/process/task_queues.js:93:5
  
  - init-starter.js:197 clone
    [lib]/[gatsby-cli]/lib/init-starter.js:197:3
  
  - init-starter.js:343 initStarter
    [lib]/[gatsby-cli]/lib/init-starter.js:343:5
  
  - create-cli.js:485 
    [lib]/[gatsby-cli]/lib/create-cli.js:485:9
```
	
맥의 문제인지 내 맥 문제인지 모르겠으나,, 일단 포기.

그냥 바닥부터 시작.

```shell
$ cd blog/
$ npm init
$ npm install gatsby react react-dom
```

이것도 실패.

안됨.

fuck it.

---

Jekyll로 우회.

[Jekyll](https://jekyllrb.com/docs/)

## prerequisites
아래 링크로 가서 따라하자.
[MacOS에 Jekyll 설치하기](https://jekyllrb.com/docs/installation/macos/)

## 프로젝트 생성
```shell
$ jekyll my_blog
$ cd my_blog
$ bundle exec jekyll my_blog
```

포트 4000(localhost:4000)번에 해당 프로젝트가 실행된다.