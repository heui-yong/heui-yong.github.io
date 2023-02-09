---
title:  "[Android-Kotlin] 좌표에 대해서"
search: false
categories: 
  - Android
last_modified_at: 2023-02-09T20:42:00-05:00
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
<script src="https://gist.github.com/heui-yong/9dfa0a6c6d9959f1fc736d374379e124.js"></script> 코드블럭
--> 
  드디어 검색기능이 활성화가 되어 다시 블로그 포스팅을 시작해보려고한다. <br>
  오늘 포스팅할 주제는 좌표에 대해서 포스팅을 하려한다.<br>

  <h2>Left, Right, Top, Bottom</h2>
  Android개발을 하다보면 View를 다룰 때 위의 4가지를 자주 접하게 된다.<br>
  먼저 아래의 그래프를 먼저 보자<br>

  ![location](/assets/image/location/location.png)<br>
  
  - Left : 생성된 View의 시작인 x좌표
  - Top : 생성된 View의 시작인 y좌표
  - Right : 생성된 View의 종료인 x좌표
  - Bottom : 생성된 View의 종료인 y좌표
  <br>

  결론적으로 시적점의 좌표 : (Left, Top), 종료점의 좌표 : (Right, Bottom)이 된다.<br><br>
  

  <h2>절대좌표와 상대좌표</h2>
  안드로이드에는 절대좌표와 상대좌표가 있다.<br>
  절대좌표는 <mark style='background-color: #fff5b1'>디바이스에서 좌측의 최상단이 
  (0,0)</mark>으로 시작하는 좌표값이다.<br>
  상대좌표는 <mark style='background-color: #fff5b1'>현재 View의 좌측 상단이 (0,0)
  </mark>으로 시작하는 좌표값이다.<br>

  <h4>절대좌표</h4>
  절대좌표를 구하는 방법으로는 getLocationOnScreen()이 있다.<br>
  <script src="https://gist.github.com/heui-yong/3a2a5396b2618c221a9cb637e0350471.js"></script>
  위의 코드를 보면 Window의 Left, Top을 넘겨줘서 디바이스의 좌측 최상단으로부터 시작점을 보내준다는 것을 알 수 있다.<br>

  <h4>상대좌표</h4>
  상대좌표를 구하는 방법으로는 getLeft(), getTop(), getRight(), getBottom()을 이용해서 구할 수 있다.<br><br>

  <h2>끝으로..</h2>
  오늘은 회사에서 좌표계의 개념이 정확하게 잡히지 않고 작업을 하다 하루종일 고생해서 작성하게 되었다. 처음에는 헷깔리지만 계속해서 하다보면 금방 갈피를 잡을 수 있을것이다.




