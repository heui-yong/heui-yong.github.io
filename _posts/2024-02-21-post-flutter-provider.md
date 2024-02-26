---
title:  "[Flutter] Provider 사용"
search: false
categories: 
  - Flutter
last_modified_at: 2024-02-21T13:18:00-05:00
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
<script src="https://gist.github.com/heui-yong/9f6cd0c69c8780228cbee7c9b324b2f8.js"></script> 소스코드
--> 

![flutter-logo](/assets/image/Flutter_start/flutter-logo.png) 
  오늘은 Provider를 사용해서 상태관리를 해보는 방법에 대해 알아볼 예정이다. 학습을 위해 예제 코드도 만들었지만 코드에 대한 설명은 깊게는 하지 않을 예정이다. 

<h2>Provider</h2>
  Provider는 앱 내 상태 관리 및 데이터 공유에 사용되는 패키지이다. 이전에 포스팅한 InheritedWidget을 기반으로 구현되어있으며 아래와 같은 장점이 있다. <br>

  - 사용자 편의성 : <mark style='background-color: #fff5b1'>ChangeNotifier</mark>를 기반으로 데이터 공급자를 구현하며, <mark style='background-color: #fff5b1'>Consumer</mark> 위젯을 통해 데이터에 액세스하고 업데이트를 추적할 수 있다.
  - 추상화 수준: Provider는 데이터 공급자와 위젯 트리 간의 상호작용을 추상화하여 코드를 더 간결하고 유지 관리가 용이하다.
  - 지연 로딩

 >공식 문서<br>[Provider Library](https://pub.dev/documentation/provider/latest/provider/provider-library.html)

아래부터는 예제 코드를 통해서 설명을 해보겠다!<br>

<h2>사용 방법</h2>
  먼저 Provider 패키지를 사용하기 위해서는 <mark style='background-color: #fff5b1'>pubspec.yaml</mark>에 Provider 패키지를 추가해준다. 추가 방법은 아래 이미지를 참고하자.<br>
  ![flutter-](/assets/image/flutter_provider/flutter_provider_2.png) <br><br>
  패키지를 추가한 뒤 아래와 같이 모델클래스를 만들어 준다.
<script src="https://gist.github.com/heui-yong/fa578e29d3c5819b16b5732fcffea5d6.js"></script>

  여기서 <mark style='background-color: #fff5b1'>ChangeNotifier</mark>는 데이터 공급자의 기본을 형성하는 클래스이다. 해당 클래스에서는 아래와 같은 기능을 제공한다.<br>

  - 가변 상태 표현 : 데이터 공급자의 가변 상태를 추적
  - 데이터 변경 알림 : 데이터가 변경될 때 리스너에게 알림

  <mark style='background-color: #fff5b1'>notifyListeners()</mark>는 ChangeNotifier 클래스의 메소드이다. 이 메서드를 호출하면 데이터 공급자에 등록된 모든 리스너에게 데이터 변경 사항을 알린다. 리스너의 종류는 아래와 같다.<br>

  >- watch : 인스턴스의 변경에 따라 위젯을 자동으로 다시 빌드하지만 필요 없는 위젯까지 다시 빌드될 수 있음
  >- select : 인스턴스의 속성만 선택하여 리턴할 수 있어 불필요한 리빌드를 방지할 수 있음
  >- read : 인스턴스의 변경에 따라 위젯을 다시 빌드하지 않기때문에 데이터를 읽고 변경할 때 사용
  >- Consumer 
   - Provider 위젯의 하위 위젯에서 Provider가 관리하는 데이터에 접근하고 위젯을 빌드하는 데 사용
   - watch, select, read와 달리 리스너 기능을 내장하고 있어 데이터 변경에 따라 위젯을 자동으로 다시 빌드

  이제 위 리스너를 사용하는 방법을 알아보자. 내가 만든 예제 코드에는 watch, select, read 세개를 사용하였다. 
  <script src="https://gist.github.com/heui-yong/6f3f1fc6abc96a5dce1640c80c347c74.js"></script>

<h2>끝으로..</h2>
  오늘은 Provider에 대해서 알아보았다. 이전에 포스팅한 InheritedWidget보다 더욱 간단하게 코드를 짤 수 있어 앞으로는 Provider를 사용할 것 같다. Provider역시 학습을 위해 정리 용도로 포스팅하였기 때문에 부족한 부분이 있다면(작성하지 않은 Consumer, 멀티 Provider 등등 ..) 추후 수정해서 완벽한 글을 만들도록 노력해보겠다!<br>
  끄읕...!