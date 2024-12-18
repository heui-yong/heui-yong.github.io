---
title: "[Flutter] 비디오 메타데이터 처리 문제 "
search: false
categories:
    - Flutter
last_modified_at: 2024-12-17T08:20:00-05:00
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

오늘은 회사에서 플러터 프로젝트를 진행하다 처음 만났던 큰 문제인 동영상 메타데이터 처리에 대한 부분을 다뤄볼 것이다.

## 문제 정의

### 1. 현상

-   파일 정보와 직접적으로 보이는 영상의 해상도는 720x1280이지만, 메다데이터는 1280x720 이였음.
-   iOS에서는 동영상이 세로로 꽉 차게 정상적으로 표시됨.
-   Android에서는 동영상이 상하좌우 여백이 생기며 비율이 iOS와 상이하여, 수동 회전을 적용하면 동영상이 짤리고 비율이 맞지 않음.

### 2. 재현 조건

-   video_player 패키지를 사용하여 Android 기기에서 특정 동영상을 재생할 때 발생함.

### 3. 원인

-   동영상 메타데이터에 rotation=-90 (회전 정보)이 포함되어 있으나 Android에서는 이를 자동으로 적용하지 않음.
-   iOS에서는 회전 메타데이터를 자동으로 인식하고 반영.

### 4. 실행 화면

실제 사용한 동영상은 저작권 문제 때문에 흰색으로 대체하였습니다. 안드로이드의 수동 회전 화면의 경우는 동영상이 좌우로 잘려서 노출되는 상황입니다.

<div style="display: flex; justify-content: space-between; gap: 10px;">
  <div style="width: 30%; text-align: center;">
    <img src="/assets/image/flutter-video-metadata-rotation-processing-issues/ios.png" style="width: 100%; height: 500px; object-fit: cover;">
    <p>iOS 화면</p>
  </div>
  <div style="width: 30%; text-align: center;">
    <img src="/assets/image/flutter-video-metadata-rotation-processing-issues/aos.jpg" style="width: 100%; height: 500px; object-fit: cover;">
    <p>안드로이드 기본 화면</p>
  </div>
  <div style="width: 30%; text-align: center;">
    <img src="/assets/image/flutter-video-metadata-rotation-processing-issues/aos_manual_rotation.jpg" style="width: 100%; height: 500px; object-fit: cover;">
    <p>안드로이드 수동 회전 화면</p>
  </div>
</div>

## 문제 발생 배경

-   동영상 메타데이터

```
[STREAM]
…
width=1280
height=720
coded_width=1280
coded_height=720
…
displaymatrix=
00000000:            0       65536           0
00000001:       -65536           0           0
00000002:            0           0  1073741824

rotation=-90
…
```

-   원본 동영상은 **1280x720 (가로 비율)** 이지만, 메타데이터 상에서 -90도 회전이 적용되어 세로 방향으로 보여야 함.

-   iOS와 Android에서 메타데이터 회전 처리 방식이 다름.

## 시도한 해결 방법

### 1. Transform.rotate()를 통한 수동 회전 - 실패

```dart
  @override
  Widget build(BuildContext context) {
    double aspectRatio = _controller.value.aspectRatio;
    double rotationAngle = -90 * (math.pi / 180.0);

    if (aspectRatio > 1) {
      aspectRatio = 1 / aspectRatio;
    }

    return Scaffold(
      backgroundColor: Colors.black,
      body: Center(
        child: _controller.value.isInitialized
            ? Transform.rotate(
              angle: rotationAngle,
              child: AspectRatio(
                        aspectRatio: aspectRatio,
                        child: VideoPlayer(_controller),
                      ),
            )
            : CircularProgressIndicator(),
      ),
    );
  }
```

-   영상 비율은 맞게 출력 되나 영상 자체가 회전되어 출력 됨.
    <br>

### 2. 영상 해상도 자체 조절 - 성공

```
ffmpeg -i input.mp4 -vf scale=720:1280 -c:v libx264 -c:a copy output.mp4
```

-   ffmpeg 명령어를 사용해서 해상도를 강제로 1280x720에서 720x1280으로 변경
-   비율과 영상이 정상적으로 노출
-   정상적으로 노출되긴하지만 파일 자체를 수정하기때문에 보류

### 3. 비율을 강제로 적용할 수 있는 패키지 사용 - 성공

> 링크 : [better_player_plus](https://pub.dev/packages/better_player_plus)

```dart
_controller = BetterPlayerController(
  const BetterPlayerConfiguration(
    aspectRatio: 9 / 16,
    looping: true,
    autoPlay: true,
    controlsConfiguration: BetterPlayerControlsConfiguration(
      controlBarColor: Colors.transparent,
      showControls: false,
    ),
  ),
);
```

-   aspectRatio: 9 / 16 설정을 통해 세로 비율을 강제로 적용.
-   비율과 영상이 정상적으로 노출
-   동영상 화면 비율 문제를 코드만으로 해결하기때문에 해당 방법 선택

## 결론

문제의 핵심은 동영상 메타데이터에 포함된 회전 정보(-90도)를 Android에서는 자동으로 적용하지 않아 발생한 것이었다. iOS는 동영상 메타데이터를 기반으로 자동 회전을 처리하였지만, Android에서는 이를 고려하지 않아 동영상 재생 시 비율과 회전 문제(상하좌우 여백 및 잘림 현상)가 나타남.

이를 해결하기 위한 시도로 Transform.rotate()를 통한 수동 회전, 동영상 파일 자체의 해상도 재조정, 그리고 aspectRatio를 강제로 적용하는 패키지(`better_player_plus`) 활용 등을 적용해봄.

-   **Transform.rotate() 사용:** 영상은 회전되나 결과적으로 화면 비율이나 잘림 문제가 여전히 존재.
-   **ffmpeg로 해상도 변경:** 동영상 파일 자체를 수정하면 올바른 비율로 표시 가능하지만, 파일 조작에 의존하는 단점이 있음.
-   **better_player_plus 패키지 사용:** 코드 레벨에서 aspectRatio를 (9/16 등) 강제로 지정하여, 추가적인 파일 수정 없이 정상적인 세로 비율을 구현 가능.

최종적으로 별도의 파일 변환 과정 없이 단순히 플레이어 단에서 비율을 강제 적용하는 `better_player_plus` 패키지를 사용하는 방식을 채택함으로써 문제 해결.
