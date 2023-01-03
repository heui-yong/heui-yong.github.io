---
title:  "[Github Blog] minimal mistakes - 댓글, 검색"
search: false
categories: 
  - GitHub Blog
last_modified_at: 2023-01-02T11:33:00-05:00
comments: true 
---
```yaml
📌 Windows 10 사용
```
<!--
블럭 사용법
 ```yaml
```
!-->

<!-- 
[Ruby install](https://rubyinstaller.org/downloads/) 하이퍼 링크
![rubyinstaller](/assets/image/Jekll-minimal_mistakes/rubyinstaller.PNG) 이미지
<mark style='background-color: #fff5b1'>...</mark><br> 형광팬처리
--> 

  Github 블로그는 따로 댓글 기능과 Goole에서 검색 노출을 설정해줘야한다.<br>
  오늘의 포스팅은 이 부분들을 구현하는 방법을 알아보도록 하자!<br>

<h1>댓글기능</h1>
 댓글 기능을 사용하기 위해서 Disqus와 Utterances가 있었는데 오늘 내가 사용하는 것은 Utterances이다. 댓글 기능을 구현하기 위해 구글에 검색해 본 결과 Disqus에는 광고가 붙는다는 사실을 알게 되어 Utterances로 선택하게 되었다<br>
<h3>01. Utterances</h3>
 <h4>설치</h4>
  Utterances을 사용하기 위해서는 먼저 Github App에서 <span style="color:#fd8900"> [Utterances](https://github.com/apps/utterances)</span>를 설치해야한다.
  ![rubyinstaller](/assets/image/Jekll-minimal_mistakes/Utterances-install-page.PNG)<br>

  설치 페이지에 접속하면 위와같은 화면이 나온다. <br>
  install버튼을 누르면 저장소를 선택하는 화면이 나오게 된다. <br>
   ![rubyinstaller](/assets/image/Jekll-minimal_mistakes/Utterances-install-page-repo.PNG) <br>

   댓글을 관리할 repo를 선택해준다. 나는 YongLog-comments를 새로 생성해주었다.<br><br>

   <h4>설정</h4>
   설치가 완료되면 설정페이지로 이동하게된다.<br>
   설정 페이지에서 repo를 설정해준다.<br>
   ![rubyinstaller](/assets/image/Jekll-minimal_mistakes/Utterances-install-page-repo-setting.PNG) <br>
   위와 같이 repo에 계정명/repo명을 입력한다.<br><br>

   그 후 블로그 포스트와 이슈 매핑 방법을 나타내는 설정이다.<br>
  ![rubyinstaller](/assets/image/Jekll-minimal_mistakes/Utterances-install-page-repo-mapping.PNG)<br>
  이슈의 제목으로 블로그 글의 경로를 설정했다.<br><br>

  ![rubyinstaller](/assets/image/Jekll-minimal_mistakes/Utterances-install-page-repo-label.PNG)<br>
  라벨과 테마를 설정하는 부분인데, 이 부분은 label에 Comment만 추가해주었다.<br><br>

  다 입력하면 아래와 같은 스크립트가 나오는데 해당 내용들을 _config.yml에 추가해준다.
   ![rubyinstaller](/assets/image/Jekll-minimal_mistakes/Utterances-install-page-repo-end.PNG)<br>
   
<h3>02. _config.yml</h3>
 여기서 수정해야할 부분은 아래와 같다.<br>

 1. repository : "YongLog-comments"
 2. provider : "utterances" 
 3. theme : "github-light"
 4. issue_term : "pathname"

 이렇게 수정을 하고 push를 진행하면 아래와 같이 정상적으로 댓글기능이 활성화 된것을 볼 수 있다!<br>
 ![rubyinstaller](/assets/image/Jekll-minimal_mistakes/Utterances-install-page-comment.PNG)<br>

<h1>검색 기능</h1>
블로그에 글을 포스팅했을 때 다른 사람들이 키워드를 검색할 경우 내 블로그가 노출되어야 한다. 그러기 위해서는 Google search console을 등록해서 검색 기능을 추가해 주어야 한다.<br>

  <h3>Google search console</h3>
  <span style="color:#fd8900">[Google search console](https://search.google.com/search-console/about)</span>은 google에서 검색을 할 경우 나의 블로그를 노출시키도록 등록하는 google서비스이다.<br>
  해당 기능을 이용하기 위해서는 구글 계정이 필요하다.<br><br>

  ![rubyinstaller](/assets/image/Jekll-minimal_mistakes/Google_search_console-start.PNG)<br>
  해당 링크에 진입 후 "시작하기"버튼을 눌려 등록을 진행한다.<br><br>

  ![rubyinstaller](/assets/image/Jekll-minimal_mistakes/Google_search_console-step1.PNG)<br>
  나는 도메인이 없고, Github에서 제공해 주는 url을 사용하기 때문에 URL 접두어를 사용한다.<br><br>

  ![rubyinstaller](/assets/image/Jekll-minimal_mistakes/Google_search_console-step2.PNG)<br>
  유효한 URL 인지 확인이 완료되면 소유권 확인을 위해 위와 같은 화면이 나온다.
- HTML 파일(권장)
- HTML 태그
- Google 애널리틱스
- Google 태그 관리자
- 도메일 이름 공급업체

이 중에 나는 HTML 파일로 진행하였다.<br>
먼저 위의 HTML파일을 다운받아준다.<br>

<h3>HTML 파일 세팅</h3>
  다운 받은 HTML파일을 _config.yml 파일과 동일한 위치에 넣는다.<br>

  ![rubyinstaller](/assets/image/Jekll-minimal_mistakes/Google_search_console-step3.PNG)<br><br>

<h3>sitemap.xml 생성</h3>
<script src="https://gist.github.com/heui-yong/e1be0a648c7e77a6a8ec4a60eb157d87.js"></script>
위에 보이는 sitemap.xml을 만든 후 아까 넣었던 HTML과 같은 위치에 넣어준다.<br>
<span style="color:#fd8900">[http://localhost:4000/sitemap.xml](http://localhost:4000/sitemap.xml)</span>를 통해 아래의 화면과 동일하게 나오는지 확인한다.

![rubyinstaller](/assets/image/Jekll-minimal_mistakes/Google_search_console-step4.PNG)<br><br>

<h3>robots.txt 생성</h3>
<script src="https://gist.github.com/heui-yong/926743e1b8a651e4195e21aa6be5a95e.js"></script>
robots.txt를 생성 후 위와 같은 위치에 넣어준다.



    




