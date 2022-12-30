---
title:  "[Github Blog] Jekll - minimal mistakes"
search: false
categories: 
  - github.io 생성
last_modified_at: 2022-12-30T17:33:00-05:00
---
```yaml
📌 Windows 10 사용
```
<!--
블럭 사용법
 ```yaml
```
!-->

<h2>00. Github블로그를 선택한 이유</h2>


  지금까지 미루고 미루던 개인 블로그를 작성하기로 마음 먹었다.
  처음에는 velog와 GitHub블로그 중에 고민을 하다가 GitHub블로그를 만들기로 했다!<br>
  GitHub블로그에는 여러가지 장단점이 있는데 대충 정리하면 아래와 같다.

  <h4>장점</h4>

  1. <mark>높은 자유도</mark><br>
      블로그에 포스팅 하는 게시물은 물론이고 블로그의 페이지 자체를 내가 원하는 대로 꾸밀 수 있다. 그리고 기능적인 부분도 내가 직접 추가할 수 있는 부분들이 있다는 것에 매력을 느꼈다.<br>
  2. <mark>다른 사람 신경을 안써도 된다.</mark><br>
      만들고나면 따로 구독자나 나의 블로그를 보는 사람들 걱정은 하지 않아도 된다. 그냥 내가 기억하고 싶은 부분이나 정리하는 용도로 쓰기가 좋다. ex) 개발일지, 일상
  3. <mark>광고로 수입 창출이 가능하다.</mark><br>
      근데 이부분은 내가 사용할 지는 잘 모르겠다..

  <h4>단점</h4>

  1. <mark>높은 진입장벽</mark><br>
      나도 블로그를 만들 때 이 부분이 너무 힘들었다. 블로그를 사용하기 위해서 따로 설치도 해야 하며, 세팅도 어려웠다. 그리고 오류를 검색해도 잘 나오지 않았고, 따로 마크다운을 몰라 5-6시간 정도 헤맨 것 같다.
  2. <mark>높은 자유도</mark><br>
      이 부분이 큰 장점이기도 하지만 큰 단점이기도 하다. 엄청난 자유도 덕분에 디자인을 잘 하지 못한다면 누군가가 만든 테마를 사용해야 하는데, 그 역시 누가 코드로 만든 것이기 때문에 내가 원하는 방향으로 변경하기 위해서는 어느 정도의 지식이 필요하다.

이러한 장단점들이 있어 고민을 하다가 높은 자유도와 정리하기 위해 만드는 블로그이기 때문에
Github블로그를 선택하게 되었다! 이제 Github블로그를 작성하기 위해 기본 세팅을 시작해보자!<br><br>

<h2>01. 기본 세팅</h2>
나는 윈도우에서 작업을 하기 때문에 Ruby와 Jekyll의 설치를 진행해야 한다. 

<h4>Ruby 설치</h4>
[Ruby install](https://rubyinstaller.org/downloads/)
해당 링크에 들어가서 아래에 체크해놓은 파일을 설치한다.<br>
<!-- <img src="assets/image/Jekll-minimal_mistakes/rubyinstaller.png" title="rubyinstaller"> -->
![rubyinstaller](/assets/image/Jekll-minimal_mistakes/rubyinstaller.PNG)

<h4>Jekll 설치</h4>
Ruby 설치가 끝나면 Jekll을 설치해야한다.<br> 
Jekll을 설치하기 위해서는 방금 설치한 Start Command Prompt with Ruby를 실행한다.<br>
![start_Ruby](/assets/image/Jekll-minimal_mistakes/start_Ruby.png)<br><br>
Ruby를 실행 후 CMD창에 아래와 같은 명령어를 입력해준다.

```
gem install jekyll
```
입력한 후 ruby -v와 jekll -v를 통해 잘 설치가 되었는지 확인이 가능하다. 잘 설치가 되었다면 기본 세팅이 끝이 났다!<br><br>

<h2>02. minimal mistakes</h2>
Github블로그에는 여러가지 테마가 존재하는데 나는 내가 쉽게 꾸밀 수 있고 마음대로 변경 가능한 minimal mistakes를 사용하기로 했다.<br><br>

<h4>minimal mistakes 설치</h4>
먼저 minimal mistakes를 사용하기 위해서는 [minimal mistakes github link](https://github.com/mmistakes/minimal-mistakes)에 들어간다.<br>
![minimal_mistakes_github_link](/assets/image/Jekll-minimal_mistakes/minimal_mistakes_github_link.PNG)<br><br>
위의 이미지에 체크한 부분을 눌려 테마를 다운로드한다. 테마를 다운로드한 후 압축을 풀면 아래와 같은 파일들을 확인할 수 있다.<br>
![minimal_mistakes_file](/assets/image/Jekll-minimal_mistakes/minimal_mistakes_file.PNG)<br><br>
아래의 파일 목록은 필요 없으므로 삭제해 주도록 하자.
- .github 
- test
- .editorconfig
- .gitattributes
- .travis.yml
- CHANGELOG.md
- README.md
- screenshot.png
- screenshot-layouts.png

삭제를 진행한 후 docs 내부의 _pages폴더를 최상위로 이동준다. 이동 시켜주고 나면 아래와 같은 구조를 가지게 된다.<br>

![minimal_mistakes_file_end](/assets/image/Jekll-minimal_mistakes/minimal_mistakes_file_end.PNG)<br><br>

이제 minimal mistakes테마를 설치 하는 과정이 끝났다. 이제 블로그를 사용하기 위한 베이스 작업은 끝났다! 이제 github블로그를 만들기 위해 Github에 Repository를 만들어 보자.<br><br>

<h2>03. Github Repository</h2>
이 부분은 간단하게 지금까지 Repo를 만들던 형식 그대로 Repo의 이름만 <mark>자신의githubid</mark>.github.io 로 만들면 끝이다. 아래를 참고해서 만들어보자.
![github_create_repo](/assets/image/Jekll-minimal_mistakes/github_create_repo.PNG)<br><br>
나는 이미 Repo를 생성했기 때문에 오류가 나지만 처음 생성하면 오류가 나지 않는다.<br>
Repo를 생성했으면 위에 설치한 minimal mistakes 테마를 push 하면 된다.<br><br>

<h2>04. 로컬서버</h2>
이제 마지막이지만 내가 하면서 헤맸던 부분이다. <br>
포스팅을 할 때 Github에 바로 push 한 뒤 github.io 링크로 확인하는 방법도 있지만 push된 이후 적용이 되기까지 약간의 시간이 필요하고 내가 원하는 방향으로 나오지 않았을 때 수정을 하면서 계속해서 commit을 진행해야 할 수 있기 때문에 로컬 서버로 먼저 확인 후 Github에 push 하는 것이 좋다.<br><br>

![localseverfile](/assets/image/Jekll-minimal_mistakes/localseverfile.PNG)<br><br>
위가 현재 나의 repo폴더이다. 해당 위치에서 CMD창을 켜서 아래의 명령어를 입력해준다.<br>
```
gem install bundler
bundle exec jekyll serve
```
명령어를 입력해주면 jekyll-cache 과 Gemfile.lock 파일이 생성된다.<br>
아래와 같이 나온다면 서버가 정상적으로 열린 것이다!<br>
![cmdend](/assets/image/Jekll-minimal_mistakes/cmdend.PNG)<br>


만약 아래와 같은 오류가 발생한다면<br>
![cmderror](/assets/image/Jekll-minimal_mistakes/cmderror.PNG)<br>

최상위 폴더에 있는 _pages 폴더에 파일들을 전부 삭제 후 다시 명령어를 입력하면 정상적으로 동작할 것이다.<br><br>

서버가 정상적으로 열렸다면, [http://localhost:4000/](http://localhost:4000/)으로 바로 확인이 가능하다!
![end](/assets/image/Jekll-minimal_mistakes/end.PNG)

나는 블로그를 이미 만든 후 포스팅을 했기때문에 나와는 다르게 나올것이다.<br><br>

<h2>05. 끝으로..</h2>
블로그를 만들면서 로컬서버 부분에서 엄청 헤맸다.. 5-6시간 정도 맨땅에 해딩하는 느낌으로 진행했다. 그래도 해결하고 나니 엄청 기분이 좋아졌다! 이제 블로그도 만들었으니 내가 만든 프로젝트, 공부한 부분, 일상같은 부분을 열심히 올려보려고 한다. 앞으로 열심히 포스팅하도록 노력해보겠다!<br><br>

끝!
