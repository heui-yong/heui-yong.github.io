---
title:  "[Flutter] Custom Bottom Sheet 만들기!"
search: false
categories: 
  - Flutter
last_modified_at: 2024-01-24T10:40:00-05:00
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
  오늘은 회사에서 스터디 용으로 만들고 있는 fitness App을 구현하는 중 찾게된 DraggableScrollableSheet를 사용해 Custom Bottom Sheet를 만들어 볼 것이다. 그렇게 어려운 부분은 없으니 따라만 하면 누구든 쉽게 만들 수 있을 것이다.

<h2>구성</h2>
  오늘 만들어 볼 앱은 아래처럼 동작하는 앱이다.<br>
 ![flutter-scroll_sheet_full](/assets/image/flutter_scroll_sheet/scrollsheet_full.gif){: style="width: 40%; height:40%; margin-right: 20px;"}<br>

 해당 앱을 다 만들고나면 위의 사진과는 다르게 나오는데, 이는 학습을 완료 후 스터디 앱에 적용한 뒤 화면을 녹화해서 그렇다. 물론 마지막에 블로그 작성용으로 만든 앱 영상도 첨부할 것 이다.

<h2>프로젝트 생성</h2>
  먼저 프로젝트를 만든 후 scroll_sheet.dart파일을 생성하고 아래 코드를 넣어주자.
  <script src="https://gist.github.com/heui-yong/e5fabbf3862fd3bd149e68395f836ca6.js"></script> <br>
  위 코드를 넣으면 아래의 이미지처럼 하늘색 배경의 앱이 실행될 것이다.<br>
   ![flutter-scroll_sheet_1](/assets/image/flutter_scroll_sheet/scroll_sheet_1.png){: style="width: 30%; height:30%; margin-right: 20px;"}

<h2>Bottom Sheet 영역</h2>
  이제 Bottom Sheet 영역을 만들어 볼 것이다. <br>
  먼저 위에서 작성한 코드의 Stack안에 아래의 코드를 넣어보자. 
  <script src="https://gist.github.com/heui-yong/d50783016a6c6b5330fcf22b81d834bb.js"></script>
  코드를 넣어보면 아래처럼 분홍색 영역이 생긴걸 볼 수 있다. <br>
   ![flutter-scroll_sheet_2](/assets/image/flutter_scroll_sheet/scroll_sheet_2.png){: style="width: 40%; height:40%; margin-right: 20px;"}
  
  아직은 1개 밖에 없기 때문에 위치가 이상해 보인다. 아래 Container를 3개 정도 색을 바꿔서 추가해보자.
  <script src="https://gist.github.com/heui-yong/c96ab4da76f6bb58ad6a1c08123012ce.js"></script> 

  추가하면 아래처럼 우리가 원하는 기능을 얼추 하는 느낌이 들게 변경되었다!
  ![flutter-scroll_sheet_3](/assets/image/flutter_scroll_sheet/scroll_sheet_3.gif){: style="width: 40%; height:40%; margin-right: 20px;"}


<h2>Bottom Sheet 디자인</h2>
  우리는 Bottom Sheet의 상단이 둥근 디자인을 원한다. 그러기 위해서는 DraggableScrollableSheet안에 있는 return Container 부분을 수정해야한다.<br>
  Container를 아래 코드처럼 ClipRRect 위젯으로 감싸준 뒤 Radius를 설정해주면 끝이다!
  <script src="https://gist.github.com/heui-yong/83480ba58ad5da33a314d4c77d6f53b1.js"></script>
    ![flutter-scroll_sheet_4](/assets/image/flutter_scroll_sheet/scroll_sheet_4.png){: style="width: 40%; height:40%; margin-right: 20px;"}

<h2>끝으로..</h2>
  오늘은 DraggableScrollableSheet를 사용해 Bottom Sheet를 만들어 보았다. 스터디할때는 관련 내용을 찾지 못했는데 집에서 유튜브를 보는 도중 알고리즘을 탔는지 딱 내가 찾던 기능을 하는 영상이 노출되어 학습을 진행하였다.
  끄읕..!



