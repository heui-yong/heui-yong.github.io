---
title:  "[Flutter] http 통신"
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
  오늘은 http 패키지를 사용해서 API를 호출하는 방법에 대해 알아보자. 이전까지는 json파일을 직접 프로젝트안에 생성해서 해당 json파일에서 데이터를 가공해서 사용했지만 json파일을 github에 올리고 http 통신을 통해 데이터를 받은 뒤 데이터를 가공해서 사용해 볼 예정이다. 

<h2>사전 작업</h2>
  먼저 http 패키지를 사용하기 위해서는 <mark style='background-color: #fff5b1'>pubspec.yaml</mark>에 http 패키지를 추가해야한다. 아래 이미지 참고하자.<br>
  ![flutter-http_1](/assets/image/flutter_http/http_1.png){: style="width: 50%; height:50%; margin-right: 20px;"}<br>
  해당 패키지의 정보는 아래 링크를 통해 확인할 수 있다. 

  http : [https://pub.dev/packages/http](https://pub.dev/packages/http)

  만약 위 방법으로 패키지가 추가되지 않을 경우 터미널로도 추가가 가능하다. 아래의 명령어를 입력해 주자.
   ```
  flutter pub get
  ```

  패키지 추가를 완료하였다면 인터넷 권한을 추가해주어야한다. 

   - ios<br>
  <mark style='background-color: #fff5b1'>Info.plist</mark> 파일에 아래 코드를 추가한다.
  <script src="https://gist.github.com/heui-yong/adc7927863733f52ccc7404fb246bdd7.js"></script>

   - Mac Os<br>
    <mark style='background-color: #fff5b1'>*.entitlements</mark>파일에 아래 코드를 추가한다. 
    <script src="https://gist.github.com/heui-yong/efd0e297726e1726fa3da43554cfb225.js"></script>

   - Android<br>
    <mark style='background-color: #fff5b1'>AndroidManifest.xml</mark>파일에 아래 코드를 추가해준다.
    <script src="https://gist.github.com/heui-yong/0793fc991dd40b1d0fe69f799b18e86f.js"></script>

  이제 http 패키지를 사용하기 위한 사전 작업은 끝났다!

<h2>http로 API 결과 받아오기</h2>
 아래 코드를 사용해서 결과 값을 가지고 올 수 있다. 
<script src="https://gist.github.com/heui-yong/9f6cd0c69c8780228cbee7c9b324b2f8.js"></script>
먼저 baseUrl은 내가 github에 올린 json의 url이다. 그리고 fetchHomeInfo에서 전달되는 값을 비동기로 받기 위해서 fetchHomeInfo함수를 async로 만들어 주었다. 그리고 response 변수가 await를 통해 비동기 처리 요청 후 결과가 올 때까지 기다린다. 이후 결과가 오게되면 response.statusCode가 200일때 응답이 성공적으로 올 경우기때문에 조건을 걸어주었다. 응답받은 json을 list형식으로 변환해준다. 이후 추가한 리스트를 반환해준다. 

<h2>받아온 데이터 사용</h2>
  이제 위에서 받아온 데이터를 사용하는 방법을 알아보자. 아래 코드를 확인해보자.<br>
  <script src="https://gist.github.com/heui-yong/47401f60785a58965db5414f119ede03.js"></script>
  나는 model class를 생성해서 해당 클래스에서 데이터를 사용할 수 있게 만들어주었다.<br>
  <mark style='background-color: #fff5b1'>ApiService().fetchHomeInfo()</mark>를 통해 API 결과에서 받아온 데이터를 _homeInfoList에 저장해준다.<br>
  <mark style='background-color: #fff5b1'>homeInfoList</mark>는 homeInfo목록을 비동기로 가져오는 메소드로, <mark style='background-color: #fff5b1'>필요한 경우에만 캐시된 목록을 반환</mark>하게 만들어주었다.<br>
  <mark style='background-color: #fff5b1'>get으로 시작되는 메소드들</mark>은 각각에 해당하는 리스트를 반환하는 메소드이다. 이 메소드에서 사용한 <mark style='background-color: #fff5b1'>first.리스트명</mark>은 
  homeInfoList에서 첫번째 HomeInfo객체를 선택하고, 그 객체의 리스트명에 해당하는 리스트를 반환하게된다. <br>
  
  이후 해당값들을 보여주는 방법을 알아보자. 
  <script src="https://gist.github.com/heui-yong/192be17b9c8762ba39d32d9f9ab7383e.js"></script>
  userList에 이전에 만들어준 getNearList를 통해 리스트에 값을 넣어준다. 그리고 FutureBuilder를 만들어주고 <mark style='background-color: #fff5b1'>snapshot.hasData</mark>으로 값이 있을 때 보여줄 화면을 만든다.<br>
  return CircularProgressIndicator()은 리스트가 불러올 동안 보여주는 화면이다.

<h2>끝으로..</h2>
  오늘은 실무에서는 데이터를 항상 서버에서 받아오기에 필수적으로 알고있어야하는 http통신을 알아보았다. 아직 플러터를 학습한지 얼마안되어 이 방법이 맞는지는 잘 모르겠지만, 일단 정리해보기 위해 작성하였다. 추후 더 좋은 방법을 알게된다면 수정해서 올리도록하겠다. 
  끄읕..!


