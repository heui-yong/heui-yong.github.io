---
title:  "[Flutter] 첫 플러터 앱 만들어보기!"
search: false
categories: 
  - Flutter
last_modified_at: 2024-01-21T10:40:00-05:00
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
  회사에서 진행하던 프로젝트가 바빠서 블로그 작성을 최근 하지못하였다. <br>
  하지만 이번 프로젝트가 끝난 후 시간이 생기게 되어 다시 블로그를 작성할 수 있게되었다! <br>
  오늘은 아래 플러터 공식 홈페이지에 있는 codelab을 따라서 만들어 볼 것이다. <br>
  이번에는 codelab을 따라하는 것이다보니 따로 코드는 올리지 않을 것이다.<br>
  [codelab 주소 클릭!](https://codelabs.developers.google.com/codelabs/flutter-codelab-first?hl=ko#0)
  

<h2>구성</h2>
  오늘 만들어 볼 앱은 아래와 같은 앱이다.<br>
 ![flutter-name-create_full](/assets/image/flutter_name_create/name_create_full.gif)<br>

 이 앱은 사용자에게 이름을 추천해주는 앱이다. 마음에 드는 이름은 좋아요 버튼을 통해 저장할 수 있다.<br>
 또한 마음에 들지 않은 이름은 해당 이름을 선택하면 좋아요가 취소가되며, favorites페이지에서도 삭제된다. 이제 처음부터 천천히 이 앱을 만들어 보자!

<h2>버튼 생성</h2>
  먼저 프로젝트를 생성한 뒤 코드랩에 있는 코드를 적용 후 실행 시 아래의 이미치럼 나올 것이다.<br>
 ![name_create_1](/assets/image/flutter_name_create/name_create_1.png){: style="width: 60%; margin-right: 20px;"} <br>
 여기서 codelab에 있는 코드로 main.dart에 Next 버튼을 추가해보자.<br>
 코드를 추가 후 실행시켜 확인해보면 아래 이미지처럼 버튼 생성에 성공한 것을 확인할 수 있다!
 ![name_create_2](/assets/image/flutter_name_create/name_create_2.png){: style="width: 60%; margin-right: 20px;"} <br>

<h2>추천 이름 영역 디자인</h2>
  이번에는 이름을 추천해주는 영역 디자인을 해볼것이다. <br>
 디자인을 위해서 Card를 사용해 볼 것이고 위젯들을 가운데 정렬 시켜볼 것이다. <br>
 또한 텍스트에 스타일을 적용도 해볼 수 있고 위젯의 color 값을 주는 방법도 알아볼 것이다.<br>
 코드랩을 잘 따라했다면 아래의 이미지와 같이 화면구성이 이루어질 것이다.<br>
![name_create_3](/assets/image/flutter_name_create/name_create_3.png){: style="width: 60%; margin-right: 20px;"} <br>

<h2>좋아요 버튼 추가</h2>
  지금까지 만든 앱은 Next를 클릭하면 다음 단어가 나와서 마음에 드는 단어를 따로 내가 기억해야하는 번거로움이 있다.<br>
 그래서 이번에는 좋아요 기능을 추가해서 내가 마음에 드는 단어는 좋아요 버튼을 통해 해당 단어를 저장하는 기능을 구현해볼 것이다. 먼저 저장하는 기능을 구현하기 전 좋아요 버튼을 먼저 구현해보자.<br>
 좋아요 버튼을 구현 시 아래의 이미지 처럼 나오게 된다.<br>
 ![name_create_4](/assets/image/flutter_name_create/name_create_4.png){: style="width: 60%; margin-right: 20px;"} <br>
 지금은 좋아요 버튼을 누를 시 리스트에는 해당 단어가 저장되지만 사용자에게는 노출되지 않고 있다.<br>
 새로운 페이지을 생성해 해당 페이지에서 좋아요한 단어의 리스트를 노출되게 만들어 볼 것이다.<br>

<h2>탐색 레일 추가</h2>
  좋아요한 단어의 리스트를 노출되는 페이지를 생성하기 전 해당 페이지로 이동할 수 있게 만들어주는 탐색 레일을 구현해 볼 것이다. 탐색 레일을 추가하게되면 단어를 추천해주는 페이지의 Home과 좋아요로 저장한 단어가 노출되는 Favorites화면으로 구성된다. <br>
  코드랩을 따라 구현 시 아래의 이미지처럼 Favorites 탭이 추가된 것을 확인 할 수 있다.<br>
  ![name_create_5](/assets/image/flutter_name_create/name_create_5.png){: style="width: 60%; margin-right: 20px;"} <br>

<h2>새 페이지 추가</h2>
  이전에 페이지를 따로 생성하지 않아 Placeholder 위젯을 사용하였는데, 이번에는 페이지를 생성해서 해당 페이지를 추가해 볼 것이다.<br>
  이번에는 코드랩에서 힌트만 얻고 직접 페이지를 구현해보는 것도 학습에 많은 도움이 될 것이다!<br>
  구현을 완료하였다면 아래 이미지처럼 내가 좋아요한 단어들이 보이는 페이지가 추가되었을 것이다.<br>
  ![name_create_6](/assets/image/flutter_name_create/name_create_6.png){: style="width: 60%; margin-right: 20px;"} <br>

<h2>끝으로..</h2>
  오늘은 플러터공식 홈페이지에 있는 플러터 첫번째 앱을 만들수있게 도와주는 코드랩을 따라 학습을 진행해보았다. 처음 시작할때 보여준 화면과 끝날때의 화면의 구성이 다른 것을 확인할 수 있을 것인데,
  고급버전의 코드까지 추가하면 첫 시작 시 보여준 화면과 동일한 구성이 될 것이다. 아직은 플러터에 대한 이해가 부족해 따라하는 것에도 시간이 많이 걸렸지만 차차 익숙해지면 나아질 것이라 생각한다..
  끄읕..!





