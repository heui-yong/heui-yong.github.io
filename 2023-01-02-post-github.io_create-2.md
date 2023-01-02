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

<h2>01. Utterances</h2>
 댓글 기능을 사용하기 위해서 Disqus와 Utterances가 있었는데 오늘 내가 사용하는 것은 Utterances이다. 댓글 기능을 구현하기 위해 구글에 검색해 본 결과 Disqus에는 광고가 붙는다는 사실을 알게 되어 Utterances로 선택하게 되었다<br>

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
   ![rubyinstaller](/assets/image/Jekll-minimal_mistakes/Utterances-install-page-repo-end.PNG)<br><br>

   <h4>_layout/post.html</h4>

   
   
   
   
   



  


