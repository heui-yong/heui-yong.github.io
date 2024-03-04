---
title:  "[Flutter] Dio + Retorfit + JsonSerializable API 통신"
search: false
categories: 
  - Flutter
last_modified_at: 2024-02-29T13:18:00-05:00
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
  오늘은 Dio, Retorfit 라이브러리에 대해 알아보려한다. 이전에 http를 이용한 통신에 대해 알아보았는데 이번에는 Dio와 Retorfit을 이용한 API통신에 대해 작성할 것이다.<br>
  그리고 JsonSerializable를 사용하여 자동 직렬화에 대해서도 알아보려한다.

<h2>Json 직렬화</h2>
  Json 직렬화 방법에는 크게 두가지가 있는데, 그 중 하나인 코드 생성을 사용한 자동 직렬화 방법을 사용해 볼 것이다.<br>
  먼저 이 방법을 사용하기위해서는 패키지를 아래와 같이 추가해주어야 한다.<br>
  ![flutter-retrofit-1](/assets/image/flutter_retrofit/flutter-retrofit-1.png)<br>
  패키지를 추가하였다면 모델 클래스를 작성해야한다. 자신이 만들 모델 클래스를 작성해준다. 나는 이름, 나이, 생년월일이 들어있는 humanInfo 리스트 모델을 아래와 같이 작성해 주었다.
  <script src="https://gist.github.com/heui-yong/df2c3aebdbd7c0e00afc8c3f073eb247.js"></script>
  내 코드 기준으로 <mark style='background-color: #fff5b1'>part 'rsp_human_info.g.dart'</mark>부분과 <mark style='background-color: #fff5b1'>_$RspHumanInfoFromJson</mark>, <mark style='background-color: #fff5b1'>_$HumanInfoFromJson</mark> 부분에서 에러가 발생하였을 것이다. 해당 부분을 잘못 작성한 것이 아니니 걱정하지 않아도 된다.<br>
  위 처럼 작성했다면 터미널을 열어 아래의 명령어를 입력해준다.
  > flutter pub run build_runner build

  명령어를 입력하고 나면 에러가 없어지고 아래의 "rsp_human_info.g.dart" 파일이 생성된 것을 확인할 수 있을것이다!
  <script src="https://gist.github.com/heui-yong/d36e3575cb095f512dea674187da50c5.js"></script>
  이렇게 코드 생성을 사용한 자동 직렬화 방법으로 Json 직렬화를 해보았다. 이후 내용에 이걸 이용하는 방법에 대해서도 설명할 것이다.<br>

<h2>Dio</h2>
  Dio는 Flutter에서 http요청을 처리하는 라이브러리이다. 네트워크 통신, 데이터 로딩, API호출 등 다양하게 활용이 가능하다.
  로깅, 인터셉트를 지원하는 부분에서 Android에서 사용해본 okHttp 라이브러리와 유사하다.

<h4>Dio 사용법</h4>
  Dio를 사용하기 위해서는 먼저 패키지를 아래와 같이 추가해주자.<br>
  ![flutter-retrofit-2](/assets/image/flutter_retrofit/flutter-retrofit-2.png)<br><br>
  추가해준 뒤 나는 Dio 클라이언트를 아래와 같이 생성해주어서 사용하였다.
  <script src="https://gist.github.com/heui-yong/003b536ab07c2081ec6fdc22c3fb02ef.js"></script>
  <mark style='background-color: #fff5b1'>interceptors</mark>의 경우 깃허브에 올린 Json파일을 가지고올 때 Map<String, dynamic>으로 들어와야할 값이 String으로 들어와 interceptors를 사용해 해당 값을 수정하였다.

<h2>Retorfit</h2>
  Retrofit은 REST API를 위한 HTTP 클라이언트를 생성하는 라이브러리이다. Retrofit은 간편하게 사용가능하고 다양한 http 요청, 옵션, 기능을 제공한다. 

<h4>Retrofit 사용법</h4>
  Retrofit역시 사용하기 위해서는 먼저 패키지를 아래와 같이 추가해주어야한다.<br>
  ![flutter-retrofit-3](/assets/image/flutter_retrofit/flutter-retrofit-3.png)<br>
  <mark style='background-color: #fff5b1'>retrofit_generator</mark>의 경우는 추가를 안해줘도 상관없지만 자동으로 코드를 생성해주기 위해 추가해주었다.<br><br>
  이제 서버와 통신하는데 필요한 API를 정의하는 부분에 대해 알아보자. 
  <script src="https://gist.github.com/heui-yong/1b34fd81531aa81a79ecf1ce9d5e41c3.js"></script>
  코드를 하나하나 살펴 보자.<br>

  <mark style='background-color: #fff5b1'>@RestApi</mark> 어노테이션은 API 인터페이스를 정의하는 데 사용된다. 위 코드에서는 baseUrl을 Dio에서 설정해주어 생략하였지만, 옵션으로 <mark style='background-color: #fff5b1'>baseUrl</mark>파라미터를 사용해 설정할 수 있다.<br>

  <mark style='background-color: #fff5b1'>@GET</mark> 어노테이션은 /human_info.json 엔드포인트에 대한 GET 요청을 정의한다.<br>

  
  <mark style='background-color: #fff5b1'>part 'api_retrofit_client.g.dart'</mark>의 경우는 코드 자동생성을 위해 추가해준 부분인데, 이 부분도 위의 직렬화와 동일하게 터미널에 아래의 명령어를 입력해주면 오류가 없어질 것이다. 
  > flutter pub run build_runner build

  입력 후 오류가 없어지면서 아래처럼 api_retrofit_client.g.dart 클래스가 생성될 것이다.
  <script src="https://gist.github.com/heui-yong/df7a60bd6f1292cb79efb67b6eac2aff.js"></script>

  이제 받아온 값을 사용하는 방법에 대해 알아보자. <br>
  먼저 해당 값을 사용하기 위해 Provider를 만들어 주었다. Provider생성 방법은 이전에 포스팅했으니 넘어가도록 하고 바로 코드를 확인해보자. 
  <script src="https://gist.github.com/heui-yong/c953bf87d313a402bd172204c009938c.js"></script>
  <mark style='background-color: #fff5b1'>apiClient</mark>는 ApiRestClient의 인스턴스이다. API 호출을 위한 클라이언트 역할을 한다.<br>
  <mark style='background-color: #fff5b1'>apiDioClient()</mark>를 통해 위에서 생성한 Dio 클라이언트를 호출해 ApiRestClient인스턴스를 생성하고 저장한다.<br>
  <mark style='background-color: #fff5b1'>fetchHumanInfo</mark>메소드를 통해 <mark style='background-color: #fff5b1'>apiClient.getHumanInfo()</mark>를 호출하여 정보를 가지고오고 <mark style='background-color: #fff5b1'>humanInfoList</mark>를 업데이트하고, 변경을 알린다.

<h2>끝으로..</h2>
  오늘은 Dio + Retorfit + JsonSerializable API 통신을 알아보았다. 실무에서는 http보다 Retorfit 사용을 더 많이 하기때문에 필수적으로 알고 있어야 하는 부분이라 포스팅 겸 학습을 진행해보았다. 아직 개념이 완벽하게 정리가 된것이 아니라 조금 더 다듬을 필요가 있을 것 같다. 실무에선 지금의 코드처럼 바로 받아서 쓰기보단 param을 따로 만들어서 사용하지만 아직은 그 부분까진 학습하지 못해서 이렇게 까지만 정리해보았다. 추후 더 알게되면 업데이트 하도록 하겠다!<br>
  끄읕...!