---
title:  "[Flutter] 플러터 시작하기!"
search: false
categories: 
  - Flutter
last_modified_at: 2023-03-24T17:00:00-05:00
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
  지금까지 포스팅이 없었던 이유는 어떤 내용을 포스팅할까 고민을 하다 마땅히 생각나는 내용이 없어
쓰지않고 있었다. 그러던 중 갑자기 회사에서 들은 플러터 세미나가 생각나서 이참에 플러터를 혼자 
공부해볼까하고 마음을 먹게 되어 다시 블로그 포스팅을 시작해보려 한다! 플러터에 대해서는 하나도
알지 못하니 처음부터 배워나가는 포스팅이라 험란한 길로 예상이 된다.. 

  <h2>플러터란?</h2>
  - 구글에서 17년도에 출시한 크로스 플랫폼 GUI SDK이다
  - 크로스 플랫폼은 AOS, iOS 플랫폼에서 하나의 코드베이스로 만들 수 있는 플랫폼이다. 
  - 구글에서 개발하고 구글에서 많은 지원을 해주고 있어 앞으로 플러터의 활용도가 높아질 가능성이 있다.
  
  <h3>Dart</h3>
  플러터는 다트(Dart)라는 프로그래밍언어를 사용한다. 다트는 베이스가 다른 프로그래밍 언어와 유사하여 자바 또는 C나 여기서 파생된 언어를 사용해봤다면 다트의 문법과 비슷한 점을 많이 찾을 수 있다. JIT(Just-In-Time), AOT(Ahead-Of-Time) 컴파일러가 모두 포함 되어 있다.

  <h2>플러터 시작</h2>
  플러터에 대해 간략하게 알아보았으니 이제 플러터를 사용해서 프로젝트를 하나 생성해보자. <br>
  먼저 나는 맥을 사용하기때문에 brew를 통해서 설치할 것이다. <br>
  자신이 사용하는 터미널을 열어 아래의 커맨드를 입력해 플러터를 설치해준다. <br>
  
  ```
  brew install flutter
  ```

  ![brew_flutter_install](/assets/image/Flutter_start/brew_flutter_install.png)

  설치가 완료 되면 아래의 커맨드를 입력해 필요한 항목들을 확인한다. 
  ```
  flutter doctor
  ```

  ![flutter_doctor](/assets/image/Flutter_start/flutter_doctor.png)

  위와 같이 두가지의 문제가 있는데, 먼저 첫번째 부분은 Android Studio를 실행한 후 <br>
  Preferences > Apperanance & Behavior > System Settings > Android SDK에 들어간다. <br>
  탭의 SDK Tools를 클릭하고 Android SDK Command-line Tools(latest)를 체크하여 apply를 누르고 설치하면 해결된다. <br>
  두번째 부분은 터미널을 열고 아래의 커맨드를 입력해주면 해결된다. <br>

  ```
  flutter doctor --android-licenses
  ```

  이제 다시 flutter doctor를 통해 확인하면 아래와 같이 필요한 항목이 충족된것을 알 수 있다!

  ![flutter_doctor__end](/assets/image/Flutter_start/flutter_doctor_end.png)

  이제 플러터를 사용해서 프로젝트를 생성해보자! <br>
  나는 지금까지 aos개발을 했어서 Android Studio로 프로젝트를 만들 것이다. <br>
  먼저 Android Studio를 실행해서 아래처럼 프로젝트를 생성해준다. 
  
  ![flutter_project_create](/assets/image/Flutter_start/flutter_project_create.png)

  그리고 좌측 탭의 Flutter에 들어가서 내가 설치한 Flutter의 경로를 설정해준다. <br>

  ![flutter_create_step1](/assets/image/Flutter_start/flutter_create_step1.png)

  마지막으로 프로젝트명과 사용할 언어를 선택해주면 프로젝트 생성이 완료된다! <br>
  나는 Kotlin과 Swift를 선택하였다. <br>

  ![flutter_create_step2](/assets/image/Flutter_start/flutter_create_step2.png)

  <h2>끝으로..</h2>
  오늘은 플러터를 설치하는 방법과 셋팅, 프로잭트 생성을 알아보았다. <br>
  설치부터 생성까지 전부 막혔던것 같다.. 앞으로 잘 배워나갈진 모르겠지만 열심히 알아보려고 노력할 예정이다! <br>
  끄읕...! 
