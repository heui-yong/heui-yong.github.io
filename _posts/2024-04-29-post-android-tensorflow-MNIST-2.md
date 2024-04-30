---
title:  "[Android] Keras MNIST Android에 적용 - 2"
search: false
categories: 
  - Android
last_modified_at: 2024-04-29T08:20:00-05:00
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

![android-logo](/assets/image/Android/android_logo.png){: style="width: 90%; height:30%;"}

오늘은 지난 포스팅에 이어서 학습한 모델을 텐서플로우 라이트를 사용하여 안드로이드에 적용하는 방법에 대해 알아보자!<br> 
<!-- 코드의 기본적인 틀은 아래의 링크를 따라 만들었다.<br>
링크 -> [classifier app with TensorFlow Lite](https://developer.android.com/codelabs/digit-classifier-tflite#0)<br><br> -->

<h1>Android에 적용</h1>
먼저 안드로이드에서 손글씨를 그릴수 있는 뷰를 사용하기위해 AndroidDrawView 라이브러리를 사용한다. 

<h3>AndroidDrawView</h3>

> [AndroidDrawView](https://github.com/divyanshub024/AndroidDraw)

위 라이브러리를 사용하기위해 몇가지 적용을 해주어야한다. 

  <h6>build.gradle.kts(Module :app)</h6>

  ```kotlin
  dependencies {
      //AndroidDraw
      implementation("com.github.divyanshub024:AndroidDraw:v0.1")
  }
  ```

  <h6>settings.gradle.kts</h6>

  ```kotlin
  dependencyResolutionManagement {
      ..
      repositories {
          ..
          maven {
              setUrl("https://jitpack.io")
          }
      }
  }
  ```

  <h6>gradle.properties</h6>

  ```kotlin
  ..
  android.enableJetifier=true
  ```

위 코드들을 추가하고 gradle sync를 눌려 정상적으로 실행되는지 확인한다.
잘 실행이 된다면 아래의 형식처럼 레이아웃에서 사용할 수 있다!
```xml
<com.divyanshu.draw.widget.DrawView
  android:id="@+id/draw_view"
  android:layout_width="match_parent"
  android:layout_height="0dp"
  app:layout_constraintBottom_toTopOf="@+id/text_view"
  app:layout_constraintStart_toStartOf="parent"
  app:layout_constraintTop_toTopOf="parent" />
```

<h3>TensorFlow Lite</h3>
  텐서플로 라이트 라이브러리를 사용하기 위해서는 아래코드를 추가해주어야 한다. 

  <h6>build.gradle.kts(Module :app)</h6>

  ```kotlin
  dependencies {
    //tensorflow
    implementation("org.tensorflow:tensorflow-lite:2.5.0")
  }
  ```
  <h6>안드로이드에 모델 추가</h6>
  아래처럼 assets 폴더를 생성한 후 이전 포스팅에서 생성한 모델을 넣어주도록 하자. 

  ![tensorflow-MNIST-1](/assets/image/tensorflow-MNIST-2/tensorflow-MNIST-1.png){: style="width: 30%; height:30%;"}<br>

  이제 해당 모델을 사용하는 방법에 대해 알아보자. 먼저 해당 모델을 로드하는 코드는 아래와 같다.
  ```kotlin
    init {
        val am = context.assets
        val afd = am.openFd("tensor_model.tflite")
        val fis = FileInputStream(afd.fileDescriptor)

        val model = fis.channel.map(FileChannel.MapMode.READ_ONLY, afd.startOffset, afd.declaredLength)
        model.order(ByteOrder.nativeOrder())

        interpreter = Interpreter(model)

        initModelShape()
    }

    //입력 및 출력 텐서 형상 초기화
    private fun initModelShape() {
        val inputTensor = interpreter.getInputTensor(0)
        val inputShape = inputTensor.shape()

        //입력 텐서의 형상 [1,28,28,1]
        modelInputChannel = inputShape[0]
        modelInputWidth = inputShape[1]
        modelInputHeight = inputShape[2]

        val outputTensor = interpreter.getOutputTensor(0)
        val outputShape = outputTensor.shape()

        //출력 텐서의 형상 [1,10]
        modelOutputClasses = outputShape[1]
    }
  ```
  위 코드로 모델을 로드한 뒤 입력 및 출력 텐서의 모양을 초기화 시켜준다.<br>
  이제 이미지를 받아서 전처리 후 이미지가 어떤 숫자인지 분석하는 코드가 들어가야한다. 
  ```kotlin
  private fun resizeBitmap(bitmap: Bitmap): Bitmap = 
    Bitmap.createScaledBitmap(bitmap, modelInputWidth, modelInputHeight, false)

  private fun convertBitmapToGrayByteBuffer(bitmap: Bitmap) : ByteBuffer {
    val byteBuffer = ByteBuffer.allocateDirect(bitmap.byteCount)
    byteBuffer.order(ByteOrder.nativeOrder())

    //Bitmap의 모든 픽셀 값을 pixels 배열에 로드
    val pixels = IntArray(bitmap.width * bitmap.height)
    bitmap.getPixels(pixels, 0, bitmap.width, 0, 0, bitmap.width, bitmap.height)

    for (pixel in pixels) {
        //RGB 값을 추출
        val r = (pixel shr 16) and 0xFF
        val g = (pixel shr 8) and 0xFF
        val b = pixel and 0xFF

        //평균 픽셀 값 계산
        val avgPixelValue = (r + g + b) / 3.0f

        //평균 픽셀 값을 [0, 1] 범위로 정규화
        val normalizedPixelValue = avgPixelValue / 255.0f

        byteBuffer.putFloat(normalizedPixelValue)
    }

    return byteBuffer
  }
  ```
  이전 포스팅에서 만든 모델의 입력 크기가 28,28 size였기 때문에 이미지의 크기역시 동일한 사이즈로 만들어주고 학습된 이미지에 맞게 그레이스케일링한다. 그 후 동일하게 0과 1 범위로 정규화 시켜준다.<br>
  ```kotlin
  fun classify(bitmap: Bitmap) : Pair<Int, Float> {
    val buffer = convertBitmapToGrayByteBuffer(resizeBitmap(bitmap))
    val result = arrayOf(FloatArray(modelOutputClasses))

    interpreter.run(buffer, result)

    return argmax(result[0])
  }

  private fun argmax(array: FloatArray): Pair<Int, Float> =
    array.withIndex().maxByOrNull { it.value }?.let { it.index to it.value }
      ?: error("Array is empty")
  ```
  직접적으로 이미지를 입력받는 부분이다. classify를 통해 이미지를 입력받고 전처리 코드를 거친다. 그 후 argmax를 통해 예측한 숫자와 확률을 받아온다.<br>

  <h6>MainActivity</h6>
  <script src="https://gist.github.com/heui-yong/54bdf9d69cb30fdfe02be0892c568e68.js"></script>
  메인액티비티에서는 각 View의 동작코드를 작성한다.

<h3>결과</h3>

![tensorflow-MNIST-2](/assets/image/tensorflow-MNIST-2/tensorflow-MNIST-2.png){: style="width: 30%; height:30%;"}
![tensorflow-MNIST-3](/assets/image/tensorflow-MNIST-2/tensorflow-MNIST-3.png){: style="width: 30%; height:30%;"}
![tensorflow-MNIST-4](/assets/image/tensorflow-MNIST-2/tensorflow-MNIST-4.png){: style="width: 30%; height:30%;"}

<h3>전체 코드</h3>

> [전체 코드](https://github.com/heui-yong/Android/tree/main/tensorflow_MNIST)

<h3>참고</h3>
 
 > 
 [classifier app with TensorFlow Lite](https://developer.android.com/codelabs/digit-classifier-tflite#0)<br>
 [Kim JuYoung님 velog](https://velog.io/@wndudwkd003/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-Tensorflow-Lite-%EC%86%90%EA%B8%80%EC%94%A8-%EC%88%AB%EC%9E%90-%EC%9D%B8%EC%8B%9D%ED%95%98%EA%B8%B0)

<h3>마무리</h3>
이렇게 텐서플로 라이트를 사용해 내가 학습시킨 파이썬 모델을 안드로이드에 적용하는 방법을 알아보았다. 처음에는 안드로이드에서 직접 학습을 시켜서 적용해야하나 하는 생각도 있었지만 tensorflow와 pytorch에서 안드로이드를 지원하는 것을 알고, 적용해보기위해 공부하면서 블로그를 작성해보았다. 부족한 부분이 있다면 댓글로 알려주신다면 더 공부해보도록 하겠다!🙇‍♂️🙇‍♂️<br>
끄읕..!
