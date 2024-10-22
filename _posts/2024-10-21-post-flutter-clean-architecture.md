---
title: "[Flutter] 클린 아키텍처 쉽게 이해하기"
search: false
categories:
  - Android
last_modified_at: 2024-10-21T08:20:00-05:00
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

플러터를 처음 배우고 나서 프로젝트가 커지다 보면 어디에 어떤 코드를 넣어야 할지 혼란스러울 때가 많습니다. 이때 '클린 아키텍처(Clean Architecture)'가 코드의 구조를 명확하게 하여 유지보수를 쉽게 만드는 데 큰 도움을 줍니다. 오늘은 초심자를 위한 Flutter의 클린 아키텍처에 대해 이야기해 보려고 합니다. 최대한 쉽게 설명하니 함께 살펴봐요! 😊

## 클린 아키텍처란?

클린 아키텍처는 소프트웨어의 유지보수를 쉽게 하기 위해 아키텍처를 명확히 구분하여 구조화하는 방법론입니다. 이 아키텍처는 코드의 의존성을 한쪽 방향으로만 흐르게 하여 모듈의 재사용성과 테스트 가능성을 높입니다. 흔히 사용되는 레이어로는 **Presentation Layer**, **Domain Layer**, 그리고 **Data Layer**가 있습니다.

### 클린 아키텍처의 레이어 구성

클린 아키텍처는 크게 세 가지 레이어로 구성됩니다.

1. **Presentation Layer**: UI와 사용자의 상호작용을 처리하는 레이어입니다. 여기서는 `Widget`과 상태 관리(State Management)가 주로 사용됩니다. 예를 들어 Riverpod, Provider, Bloc 같은 상태 관리 패턴이 포함됩니다.

2. **Domain Layer**: 비즈니스 로직이 담긴 레이어로, 애플리케이션의 핵심적인 규칙과 연산을 처리합니다. `UseCase` 클래스가 이 레이어의 주요 요소입니다. 이 레이어는 다른 레이어에 의존하지 않도록 설계하는 것이 중요합니다.

3. **Data Layer**: 외부에서 데이터를 가져오거나 저장하는 레이어입니다. API 호출이나 로컬 데이터베이스와의 상호작용이 이 레이어에서 이루어집니다. 이 레이어는 `Repository`를 통해 데이터를 관리하며, `Data Source`로부터 데이터를 가져옵니다.

### 레이어 간 의존성 흐름

![clean_architecture_1](/assets/image/flutter_clean_architecture/clean_architecture_1.webp)
위 그림에서 볼 수 있듯이, 클린 아키텍처의 핵심은 **의존성 규칙(Dependency Rule)**입니다. 의존성은 반드시 안쪽으로만 흐르며, 바깥쪽 레이어는 안쪽 레이어를 참조할 수 없습니다. 이 구조 덕분에 UI 레이어는 비즈니스 로직을 직접 다루지 않고, Domain 레이어를 통해 접근합니다.

## 각 레이어 구현 예시

이제 각 레이어가 어떻게 실제로 구현되는지 간단한 예제를 통해 살펴보겠습니다.

### 1. Presentation Layer

```dart
try {
  final imageInfo = await ref.read(imageInfoNotifierProvider.notifier).getImageInfo(prompt);
  setState(() {
    _imageInfoState = AsyncValue.data(imageInfo);
  });
} catch (e, stackTrace) {
  setState(() {
    _imageInfoState = AsyncValue.error(e, stackTrace);
  });
}
```

위 코드는 사용자가 볼 수 있는 UI와 상태 관리 로직을 보여줍니다. 사용자가 텍스트 필드에 프롬프트를 입력하고 버튼을 누르면 `ImageInfoNotifier`를 통해 데이터를 가져오고 UI에 표시됩니다. 이 예시는 Riverpod을 사용하여 상태를 관리하고, 데이터를 비동기로 처리하는 방식을 보여줍니다.

### 2. Domain Layer

#### Model

```dart
@JsonSerializable()
class RspImageInfo{
    final List<ImageInfo> imageInfo;
    RspImageInfo({required this.imageInfo});

    factory RspImageInfo.fromJson(Map<String, dynamic> json) => _$RspImageInfoFromJson(json);
    Map<String, dynamic> toJson() => _$RspImageInfoToJson(this);
}

@JsonSerializable()
class ImageInfo{
    final String imageUrl;
    final String date;
    final String prompt;

    ImageInfo({required this.imageUrl, required this.date, required this.prompt});

    factory ImageInfo.fromJson(Map<String, dynamic> json) => _$ImageInfoFromJson(json);
    Map<String, dynamic> toJson() => _$ImageInfoToJson(this);
}
```

#### UseCase

```dart
class GetImageInfoUseCase {
  final ImageInfoRepository repository;

  GetImageInfoUseCase(this.repository);

  Future<RspImageInfo> execute(String prompt) {
    return repository.getImageInfo(prompt);
  }
}
```

Domain 레이어에서는 비즈니스 로직을 정의합니다. 위 예시는 `UseCase` 클래스인 `GetImageInfoUseCase`로, 데이터 레이어에서 정보를 가져오도록 합니다.

### 3. Data Layer

#### DataSource

```dart
abstract class ImageInfoRemoteDataSource {
  Future<RspImageInfo> getImageInfo(String prompt);
}

class ImageInfoRemoteDataSourceImpl implements ImageInfoRemoteDataSource{
  final Dio httpClient;

  const ImageInfoRemoteDataSourceImpl({required this.httpClient});

  @override
  Future<RspImageInfo> getImageInfo(String prompt) async {
    try {
      final response = await httpClient.post(
        imageCreate,
        data: {
          "prompt": prompt,
        },
      );
      return RspImageInfo.fromJson(response.data);
    } catch(e) {
      Logman.instance.error(e.toString());
      throw Exception('Failed to load video info');
    }
  }
}

final imageInfoRemoteDataSourceProvider = Provider.autoDispose<ImageInfoRemoteDataSource>(
    (ref) {
      final dio = ref.watch(dioProvider);
      return ImageInfoRemoteDataSourceImpl(httpClient: dio);
    }
);
```

#### Repository

```dart
abstract class ImageInfoRepository {
  const ImageInfoRepository();

  Future<RspImageInfo> getImageInfo(String prompt);
}

class ImageInfoRepositoryImpl extends ImageInfoRepository {
  final ImageInfoRemoteDataSource imageInfoRemoteDataSource;

  const ImageInfoRepositoryImpl({
    required this.imageInfoRemoteDataSource
  });

  @override
  Future<RspImageInfo> getImageInfo(String prompt) async {
    try {
      final res = await imageInfoRemoteDataSource.getImageInfo(prompt);
      return res;
    } catch(e) {
      Logman.instance.error(e);
      throw Exception('Failed to load image information from repository. Error: $e');
    }
  }
}
```

Data 레이어에서는 외부 데이터 소스를 이용해 정보를 가져오거나 저장합니다. 위 코드에서는 `Dio` 패키지를 이용해 API를 호출하고, 받은 데이터를 `RspImageInfo` 객체로 변환합니다.

## 마무리

오늘은 플러터의 클린 아키텍처에 대해 간단히 살펴봤습니다. 초심자에게는 생소할 수 있는 개념일 수 있지만, 클린 아키텍처를 적용하면 프로젝트가 커져도 코드의 유지보수가 훨씬 쉬워집니다. 이번 기회를 통해 클린 아키텍처의 개념을 이해하고, 실제 프로젝트에 적용해 보세요. 처음에는 어려울 수 있지만, 작은 프로젝트부터 적용하다 보면 점차 익숙해질 것입니다. 🛠️

추후 더 좋은 방법이나 개선사항이 있다면 계속 업데이트할 예정이니, 댓글로 의견 많이 남겨 주세요! 😊 끄읕..! 🚀
