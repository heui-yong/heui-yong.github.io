---
title:  "[Android] Keras MNIST Android에 적용 - 1"
search: false
categories: 
  - Android
last_modified_at: 2024-04-28T08:20:00-05:00
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

오늘은 오랜만에 안드로이드에 대한 포스팅을 하려한다.<br> 
요즘 회사에서 딥러닝 학습을 진행중인데, 학습할때 사용한 손글씨 숫자를 어떤 숫자인지 인식하는 모델을 텐서플로 라이트를 사용해서 안드로이드에 적용하는 방법을 알아보자!<br><br>

먼저 텐서플로우와 관련 파이썬 라이브러리는 설치가 되어있다는 가정하에 진행하니 라이브러리 설치는 다른 블로그의 포스팅을 참고부탁드립니다!<br>

<h1>Keras 손글씨 모델 학습하기</h1>
이미 많은 학습된 모델이 많지만, 이번 포스팅의 목표는 내가 학습 시킨 모델을 안드로이드에 적용시키는 방법을 알아보는 것이기때문에 먼저 직접 모델을 학습시켜볼 것이다. 데이터 셋의 경우는 MNIST 데이터셋을 사용할 것이다. 

<h3>MNIST 데이터셋</h3>

```python
from tensorflow.keras.datasets import mnist
import numpy as np

(x_train,y_train),(x_test,y_test) = mnist.load_data()
```

위 코드를 사용해서 데이터를 불러올 수 있다.<br>
위를 통해 불러온 데이터가 어떤 데이터인지 간단하게 시각화해보면 아래와 같다.<br>

```python
import matplotlib.pyplot as plt
import random
for i in range(1,4,1):
    for j in range(1,4,1):
        plt.subplot(i,4,j)
        plt.imshow(x_train[random.randint(0,60000)],cmap="gray")
    plt.show()
```
![tensorflow-MNIST-1](/assets/image/tensorflow-MNIST/tensorflow-MNIST-1.png){: style="width: 30%; height:30%;"}

<h3>입력 데이터 정규화</h3>
현재 만들려고하는 모델의 입력 데이터는 28, 28 size의 이미지이고, 각 픽셀의 값은 0~255이다. 이 데이터를 0, 1의 범위로 정규화할 것이다. 코드는 아래와 같다. 

```python
from tensorflow.keras.utils import to_categorical

x_train = x_train.reshape(-1,28,28,1)/255.
x_test = x_test.reshape(-1,28,28,1)/255.
y_train = to_categorical(y_train)
y_test = to_categorical(y_test)
```
x_train과 x_test는 Conv2D레이어에 넣기 위해서 (28, 28)에서 (28, 28, 1)로 모양을 변졍을해주었다.

<h3>model 구성</h3>
레이어들을 순차석으로 쌓을 수 있게 해주는 keras의 Sequential모델을 사용한다.<br>
Dense,Flatten,BatchNormalization,Conv2D 레이어를 사용한다. 

```python
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense,Flatten,BatchNormalization,Conv2D

model = Sequential()
model.add(Conv2D(32,(2,2),activation="relu",input_shape=(28,28,1)))
model.add(BatchNormalization())
model.add(Conv2D(64,(2,2),activation="relu"))
model.add(BatchNormalization())
model.add(Conv2D(128,(2,2),2,activation="relu"))
model.add(BatchNormalization())
model.add(Conv2D(32,(2,2),activation="relu"))
model.add(BatchNormalization())
model.add(Conv2D(64,(2,2),activation="relu"))
model.add(BatchNormalization())
model.add(Conv2D(128,(2,2),2,activation="relu"))
model.add(BatchNormalization())
model.add(Flatten())
model.add(Dense(128,activation="relu"))
model.add(Dense(10,activation="softmax"))
```

<h3>model 학습</h3>

```python
model.compile(loss = "categorical_crossentropy",optimizer = "adam",metrics=["acc"])
history = model.fit(x_train,y_train,validation_data=(x_test,y_test),epochs=30,batch_size=256)
```

분류작업을 진행하는 모델이기때문에 categorical_crossentropy로 지정해주고 옵티마이저의 경우는 많이 사용하는 adam을 사용해주었다. 아래를 통해 결과를 확인하자.
```python
loss = history.history["loss"]
acc = history.history["acc"]
val_loss = history.history["val_loss"]
val_acc = history.history["val_acc"]
plt.subplot(1,2,1)
plt.plot(range(len(loss)),loss,label = "Train Loss")
plt.plot(range(len(val_loss)),val_loss,label = "Validation Loss")
plt.grid()
plt.legend()
plt.subplot(1,2,2)
plt.plot(range(len(acc)),acc,label = "Train Accuracy")
plt.plot(range(len(val_acc)),val_acc,label = "Validation Accuracy")
plt.grid()
plt.legend()
plt.show()
```

![tensorflow-MNIST-2](/assets/image/tensorflow-MNIST/tensorflow-MNIST-2.png){: style="width: 50%; height:30%;"}

<h3>결과 확인</h3>

```python
index =random.randint(0,9999)
plt.imshow(x_test[index],cmap="gray")
predict = model.predict(x_test[index].reshape(1,28,28,1))
print("Actual : {}\tPredict : {}".format(np.argmax(y_test[index]),np.argmax(predict)),)
```
![tensorflow-MNIST-3](/assets/image/tensorflow-MNIST/tensorflow-MNIST-3.png){: style="width: 50%; height:30%;"}

결과를 확인하니 잘 예측하는걸 볼 수 있다. 이제 모델을 저장해보자.

<h3>model 저장</h3>

```python
model.save("tensor_model.h5")
new_model = tf.keras.models.load_model("tensor_model.h5")
convert = tf.lite.TFLiteConverter.from_keras_model(new_model)
tflite_model = convert.convert()
with open('tensor_model.tflite', 'wb') as f:
    f.write(tflite_model)
```

위 코드로 학습 시킨 모델을 tensor_model.tflite로 저장하였다.<br>
지금까지 안드로이드에 적용할 모델의 생성하는 부분에대해 알아보았다. 다음 포스팅은 생성한 모델을 텐서플로 라이트를 사용해서 안드로이드에 적용하는 방법에 대해 알아볼 것이다.<br>
끄읕..! 