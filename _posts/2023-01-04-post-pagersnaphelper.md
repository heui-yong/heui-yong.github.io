---
title:  "[Android-Kotlin] SnapHelper"
search: false
categories: 
  - Android
last_modified_at: 2023-01-04T22:33:00-05:00
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
--> 
  SnapHelper는 RecyclerView를 ViewPager처럼 사용할 수 있게 도와주는 클래스이다. 

  <h2>사용 방법</h2>
  SnapHelper를 사용하기 위해서는 평소와 같이 RecyclerView를 생성하고 Adapter를 만들고 나서 어뎁터와 연결 후 아래의 코드만 추가해주면 끝난다.
  <script src="https://gist.github.com/heui-yong/9dfa0a6c6d9959f1fc736d374379e124.js"></script>

  <h2>적용</h2>
  <script src="https://gist.github.com/heui-yong/a62bab83626fd1904d0696c14fd51242.js"></script>
  위의 코드와 같이 snap.attachToRecyclerView(this)를 통해 SnapHelper기능을 추가하였다. 


  <h2>결과</h2>

  ![test1](/assets/image/snaphelper/test1.gif)<br>
  적용 전

  ![test1](/assets/image/snaphelper/test2.gif)<br>
  적용 후

  <h2>끝으로..</h2>
  오늘은 회사에서 알게된 SnapHelper를 간단하게 구현해보았다. 조만간 SnapHelper를 하면서 알게된 drag&drop도 한번 구현해 볼 예정이다.




