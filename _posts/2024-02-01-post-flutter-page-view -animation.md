---
title:  "[Flutter] PageView 에니메이션 사용해보기!"
search: false
categories: 
  - Flutter
last_modified_at: 2024-02-01T10:40:00-05:00
comments: true 
---
```yaml
📌 Mac M2 pro 사용
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

![flutter-logo](/assets/image/Flutter_start/flutter-logo.png) 
  오늘은 이전에 포스팅했던 PageView에서 애니메이션을 추가하는 방법을 포스팅할 것이다.<br>
  코드자체가 어렵지 않으니 금방 적용할 수 있을 것이다!

<h2>구성</h2>
  이번에 사용할 애니메이션은 아래처럼 선택한 페이지가 zoom처리 되고 나머지 페이지는 작아지는 애니메이션이다.
 ![page_view_animation-full](/assets/image/flutter_page_view_animation/page_view_animation_full.gif){: style="width: 30%; height:40%; margin-right: 20px;"}<br>
 TweenAnimationBuilder를 사용해서 해당 애니메이션을 구현해볼 것이다.
  

<h2>TweenAnimationBuilder</h2>
  TweenAnimationBuilder는 대상 값이 변경될 때마다 위젯의 속성을 대상 값으로 애니메이션화 하는 위젯빌더이다. 
  <mark style='background-color: #fff5b1'>tween.begin을 시작값으로 tween.end로 변할 때까지 적용된다.</mark> 아래 코드를 참고해보자! 
  <script src="https://gist.github.com/heui-yong/2b8dfdf14d96bdf172d4f6671eb1ae0f.js"></script>

<h2>적용</h2>
  먼저 PageView.builder안에 선택한 페이지를 변수 값에 저장해주는 코드와 컨트롤러를 추가해준다. 아래 코드를 사용하기 위해서는 StatefulWidget으로 사용해야한다!
  <script src="https://gist.github.com/heui-yong/44af5fa2bb829623f2f95ab2d6fec530.js"></script><br>
  위 코드에서 itemCount는 따로 생성한 리스트의 길이로 넣어주었다. itemBuilder의 경우는 scale값은 내가 선택한 페이지 인지 아닌지 판별해서 값을 넣어주고, GoalImageWidget은 내가 PageView에서 보여줄 화면을 따로 구성한 위젯이다.<br>
  이제 TweenAnimationBuilder를 작성하는 코드를 추가해보자!<br><br>
  <script src="https://gist.github.com/heui-yong/5fdbe4c4af1060a626f78357f95bb72d.js"></script>
  이전에 TweenAnimationBuilder의 생성자에 대해 설명했으니 이해하는데 어려움은 없을 것이다. 코드를 적용시켜보면 애니메이션이 적용된 PageView를 구현할 수 있다!

  

<h2>끝으로..</h2>
  오늘은 PageView에 애니메이션을 주는 방법에 대해 알아보았다. 딱히 어려운 코드는 아니지만 알고있으면 언젠간 쓸 일이 있을 것 같아 정리했다.<br>
  끄읕..!


