---
title:  "[Flutter] PageView 사용해보기!"
search: false
categories: 
  - Flutter
last_modified_at: 2024-01-30T10:40:00-05:00
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
  오늘은 회사도 스터디 용으로 만들고 있는 fitness App을 구현하면서 학습한 PagView에 대해 정리를 해볼 것이다. 기존 Android를 개발할때 사용한 ViewPager와 유사하였지만 사용하기는 Flutter의 PageView가 더 편하였다.

<h2>구성</h2>
  PageView는 아래처럼 여러가지의 화면을 한 화면에서 보여주게 만들어주는 기능이다.<br>
 ![page_view_full](/assets/image/flutter_page_view/page_view_full.gif){: style="width: 30%; height:40%; margin-right: 20px;"}<br>
  
 먼저 나는 아래의 이미지처럼 4가지의 화면을 PageView에서 보이게 만들 것이다. 
 ![page_view_1](/assets/image/flutter_page_view/page_view_1.png)<br>
 아래의 화면을 구성 후 PageView를 작성해 보겠다. 

<h2>PageView.Builder 생성자</h2>
  페이지에 들어갈 화면 구성을 완료하였다면 이제 구현한 페이지를 PageView안에 넣어야한다. 
 <script src="https://gist.github.com/heui-yong/e12c59926acc74e7240c51b1e404de0f.js"></script>
 나는 onBoardingList에 있는 값들에 따라 동적으로 화면구성을 하기 위해 <mark style='background-color: #fff5b1'>PageView.Builder</mark>를 사용하였다. OnBoardingWidget의 경우는 내가 위에서 따로 만든 화면이다. <br>
 위 코드에서 <mark style='background-color: #fff5b1'>controller</mark>는 나중에 버튼을 통해서 페이지 이동이 가능하도록 추가해주었고, <mark style='background-color: #fff5b1'>itemCount</mark>는 보여질 화면구성이 onBoardingList에 들어있는 값들이기 때문에 리스트의 길이로 설정하였다. 이렇게하면 스크롤을 통한 페이지 이동이 가능하게 되었다. 다음은 버튼을 통한 페이지 이동에 대해 작성해 보겠다.

<h2>버튼을 통한 이동</h2>
  이번에는 따로 버튼을 생성하여 해당 버튼 클릭 시 페이지 이동이 가능하도록 만들어 보자!<br>
 우선 버튼을 생성하기 전 위에서 추가해준 controller를 통해 선택한 page 번호를 아래 코드로 저장해준다.
 <script src="https://gist.github.com/heui-yong/6dcfe43f5bc605b7048320803af92bd4.js"></script>

 selectPage에 값을 넣어 준 뒤 버튼위젯의 onPressed에 아래 코드를 넣어주면 된다.
 <script src="https://gist.github.com/heui-yong/d5fa3abf4b894ae94aa88494768b767a.js"></script>
 <mark style='background-color: #fff5b1'>controller.jumpToPage</mark>으로 페이지 이동이 가능하고 화면 갱신을 위해 <mark style='background-color: #fff5b1'>setState</mark>를 사용해 주었다. 코드 적용 시 정상적으로 버튼으로도 이동이 가능하게 될 것이다!
  

<h2>끝으로..</h2>
  오늘은 PageView를 학습 후 포스팅 해보았다. 위 영상을 보면 프로그레스바도 버튼에 함께 있지만 해당 포스팅에서는 PageView에 대한 내용을 작성했기때문에 프로그레스바는 건너뛰었다. 언젠간 해당 내용도 다뤄서 포스팅하도록 하겠다.<br>
  끄읕..!


