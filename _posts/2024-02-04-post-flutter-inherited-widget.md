---
title:  "[Flutter] Inherited Widget"
search: false
categories: 
  - Flutter
last_modified_at: 2024-02-05T13:18:00-05:00
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
  오늘은 Inherited Widget에 대해서 알아보자. 만약 내가 페이지를 구성할 때 하단에서 사용할 데이터를 전달할 때 트리의 top에서 bottom까지 데이터를 전달하게 되는데, 이때 위젯의 개수가 많아질수록 불필요한 데이터 전달이 많아지게 된다. 이때 Inherited Widget을 최상단에 선언 후 데이터를 저장하게되면 자식 위젯들은 이 데이터에 불필요한 데이터 전달 없이 데이터로 바로 접근이 가능하다. 아래 이미지를 참고하자!<br>
  ![flutter-inherited-widget-1](/assets/image/flutter_inherited_widget/inherited-widget-1.png){: style="width: 60%; height:40%; margin-right: 20px;"}<br>

<h2>구성</h2>
  Inherited Widget에 대해서 알아보기 위해 간단한 앱을 만들어보았다. 체크박스가 있는 리스트뷰와 체크한 아이템의 개수를 보여주는 화면으로 구성되어있다. 

  ![flutter-inherited-widget-2](/assets/image/flutter_inherited_widget/inherited-widget-2.png){: style="width: 30%; height:30%; margin-right: 20px;"}

  화면 구성 코드이다.<br>
  <script src="https://gist.github.com/heui-yong/aab178afaf90ed0fafef83ff811021cc.js"></script>
  CheckBoxBgWidget()에는 체크박스 리스트화면이 구성되어있고, TotalCountWidget()에는 체크한 아이템의 개수를 보여주는 화면이다. 이 부분은 해당 포스팅에는 관련은 없으니 따로 추가해놓진 않았지만 내 깃허브에 들어가면 전체 코드를 확인할 수 있다. <br>
  [[해당 깃허프 프로젝트 주소 클릭!]](https://github.com/heui-yong/Flutter/tree/main/inherited_check_box)
  

<h2>Inherited Widget</h2>
  이제 Inherited Widget을 사용하는 방법에 대해 알아보자. 우선 밑 코드는 내가 작성한 코드이다.
  <script src="https://gist.github.com/heui-yong/d5b0ab09ba1898f207818f504d173e67.js"></script>
  AppState 클래스에서는 checkList를 가지고있다. 이때 생성자는 빈 Set<String>을 할당한다.
  <mark style='background-color: #fff5b1'>copyWith</mark> 메소드를 통해 상태를 변경한 새 인스턴스를 생성할 수 있다. <br>
  AppStateScope 클래스는 InheritedWidget을 상속받는 클래스이다. 여기서 <mark style='background-color: #fff5b1'>of</mark> 메소드를 통해 인스턴스의 data를 가지고 올 수 있다. <mark style='background-color: #fff5b1'>updateShouldNotify</mark> 메소드는 데이터가 변경되었을 때 위젯이 업데이트 되어야 하는지 결정하는 메소드이다. 



<h2>사용 방법</h2>
  먼저 Inherited Widget을 사용하기 위해 아래처럼 StatefulWidget 위젯을 생성하였다.
  <script src="https://gist.github.com/heui-yong/3a3fb95580981cebfe4dc13dfd5be262.js"></script>

  addToList를 통해 선택한 체크박스의 id를 checkList에 넣어주고 <mark style='background-color: #fff5b1'>copyWith</mark> 메소드를 통해 상태를 변경한 새 인스턴스를 생성한다. removeToList는 체크 박스 해제 시 checkList에 해당 id를 삭제해주고 나머지는 동일하다. 이렇게 StatefulWidget을 생성한 뒤 최상단을 아래 코드처럼 생성한 위젯으로 감싸면 사용이 가능하다.<script src="https://gist.github.com/heui-yong/354dbc9ad213b9aa0c2a09872f1ba4b5.js"></script>

  접근을 할 경우는 위에서 말한 것 처럼 of메소드를 사용해서 접근한다. 
  <script src="https://gist.github.com/heui-yong/47a7f00b4b11b78f38d9fc980758102e.js"></script>
  

<h2>끝으로..</h2>
  오늘은 Inherited Widget에 대해서 알아보았다. 코드가 길어 복잡해 보일 수 있지만 차근차근 따라하면 어렵지 않게 Inherited Widget을 사용할 수 있을 것이다. 나는 Inherited Widget을 학습할 때 공식홈페이지의 codelab을 보고 공부하였다. 시간이 괜찮다면 공식 홈페이지의 codelab에서 Inherited Widget에 대해 자세하게 알아보는것도 추천한다!<br>
  끄읕..!


