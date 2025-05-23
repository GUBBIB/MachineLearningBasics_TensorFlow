# 코드 설명

## 합성곱 - CNN(Convolutional Neural Network) 데이터 흐름
![Image](https://github.com/user-attachments/assets/4e65a7cb-3ec2-4e54-b0ed-2bcea858bb30)

## 텐서(Tensor)란?
<img width="899" alt="Image" src="https://github.com/user-attachments/assets/328e29c7-41cb-43b6-a63a-1f19f21dfe4a" />

- **텐서(Tensor)** 는 쉽게 말해서 ``다차원 배열`` 이다.
- **텐서(Tensor)** 는 ``벡터(Vector)``와 ``행렬(Matrix)``을 **일반화** 한 것이며, ``3차원`` 이상으로 확장할 수 있다.

## keras
### keras란?
**keras**는 ``Python`` 으로 구현된 **쉽고 간결한 딥러닝 라이브러리**이다.

### keras를 사용하는 이유
1. 모듈화가 가능하다.
2. 간결하며 이해하기가 쉽다.
3. 새로운 클래스나 함수로 모듈을 쉽게 확장할 수 있다.

### keras 라이브러리의 모듈
이 챕터에서 사용하는 모듈은 ``datasets``, ``models``, ``layers`` 3가지이다.

- **dataset** : 딥러닝 모델을 학습시키기 위한 데이터셋을 제공하는 모듈로 ``CIFAR10``, ``MINIST`` 가 있다.<br>
  - 이 챕터에서는 ``datasets.cifar10.load_data()``를 통해서 ``CIFAR10`` 데이터셋을 로드한다.

**※ ``CIFAR10`` 데이터셋은 10개의 **클래스/객체** (자동차, 비행기, 고양이, 강아지 등)로 분류된 ``32x32`` 크기의 **컬러(RGB)** 이미지 데이터셋이다.**

- **models** : 딥러닝 모델을 ``구성`` 하고 ``학습`` 하는데 필요한 **고수준 API** 를 제공하는 모듈이다.<br>
  - ``Sequential()`` : **레이어**를 한줄의 **층의 형태**로 **순차적(직선적)으로 쌓는 모델**이다.
  - ``Model()`` : **다중입력** , **다중출력** 이 가능해서 **Sequential** 보다 ``유연한/복잡한`` 구조를 설계할 수 있다.
  - ``summary()`` : 모델의 **전체 구조**를 **요약**해서 출력해주며, 각 `레이어의 이름`, ``출력 형태``, ``학습해야 하는 파라미터 수`` 를 표의 형태로 보여준다.
  - [Compile()](https://github.com/GUBBIB/MachineLearningBasics_TensorFlow/blob/main/Doc/Models/Compile().md) : **모델**을 학습하기 전에, 학습에 필요한 ``방식/전략`` **(옵티마이저, 손실 함수, 평가 지표 등)** 을 설정하는 함수이다.
  - [Fit()](https://github.com/GUBBIB/MachineLearningBasics_TensorFlow/blob/main/Doc/Models/Fit().md): 모델에 데이터를 넣어서 합습시키는 함수이다.

- **layers** : 딥러닝 모델을 구성하는 다양한 ``기본적인 층``을 제공하는 모듈이다.
  - [Conv2D(합성곱 레이어)](https://github.com/GUBBIB/MachineLearningBasics_TensorFlow/blob/main/Doc/Layers/Conv2D(%ED%95%A9%EC%84%B1%EA%B3%B1%20%EB%A0%88%EC%9D%B4%EC%96%B4).md) : 2D 합성곱 레이어를 만든다.
    - 이미지에서 ``특징(feature)`` 을 추출하는 역할을 하며 ``필터(커널)`` 을 이용해 이미지에서 ``중요한 패턴``을 감지한다.<br>
    - 필터를 거쳐서 나온 값이 클수록 특징이 뚜렷하다는 의미이다.

  - [MaxPooling2D(최대 풀링 레이어)](https://github.com/GUBBIB/MachineLearningBasics_TensorFlow/blob/main/Doc/Layers/MaxPooling2D(%EC%B5%9C%EB%8C%80%20%ED%92%80%EB%A7%81%20%EB%A0%88%EC%9D%B4%EC%96%B4).md) : 주로 ``Conv2D 함수`` 뒤에 사용되며, 추출한 ``특징``을 **유지하면서** 크기는 **줄이는 함수**이다.

    - 크기를 줄이기 때문에 **계산량**도 줄고, **과적합** 도 막아준다.

  - [Flatten(평탄화 레이어)](https://github.com/GUBBIB/MachineLearningBasics_TensorFlow/blob/main/Doc/Layers/Flatten(%ED%8F%89%ED%83%84%ED%99%94%20%EB%A0%88%EC%9D%B4%EC%96%B4).md) : ``Conv2D``, ``MaxPooling2D`` 등을 통해 얻은 ``다차원(2D/3D 등) 특징 데이터``를 ``1차원 벡터``로 변환하는 레이어다.
    - ``Dense 레이어`` 가 **1차원 데이터** 만 입력받기 때문에, 그 전에 ``Flatten 레이어`` 를 사용해 데이터를 1차원으로 변환해야 한다.

  - [Dense(완전 연결 레이어)](https://github.com/GUBBIB/MachineLearningBasics_TensorFlow/blob/main/Doc/Layers/Dense(%EC%99%84%EC%A0%84%20%EC%97%B0%EA%B2%B0%20%EB%A0%88%EC%9D%B4%EC%96%B4).md) : ``Conv2D``, ``MaxPooling2D`` 로 추출한 특징들을 하나로 모아서, 최종적인 판단이나 예측을 내리는 함수이다.
    - 예를들어 ``CNN``에서 **고양이/강아지**를 구분하는 문제에서 ``Dense 레이어`` 가 **특징**들을 보고 **"이건 고양이다!"** 라고 ``결정``을 내리는 부분이다.

*****
## 데이터셋 다운로드 및 데이터 확인하기 
- **datasets.cifar10.load_data()로 load해온 데이터**

|항목|설명|데이터 수|형태(shape)|
|-|-|-|-|
|``train_images``|학습용 이미지|``50,000개``|``(50000, 32, 32, 3)``|
|``train_labels``|학습용 이미지의 라벨 (정답)|``50,000개``|``(50000, 1)``|
|``test_images``|테스트용 이미지|``10,000개``|``(10000, 32, 32, 3)``|
|``test_labels``|테스트용 이미지의 라벨|``10,000개``|``(10000, 1)``|

### images를 255로 나누는 이유
```python
train_images, test_images = train_images / 255.0, test_images / 255.0
```
- **images**는 ``1차원(흑백) 데이터`` 와 ``3차원(RGB) 데이터``가 있는데, 이 값이 ``0 ~ 255`` 로 너무커서 ``0 ~ 1`` 사이의 값으로 **``정규화``** 를 해줘야 하기 때문이다.
  - ``1차원(흑백) 데이터`` 이미지에서 각 픽셀의 값이 ``0 ~ 255`` 사이의 **숫자** 이며, 이는 **빛의 밝기** 를 수치화 한것이다. <br>
  **``※(0은 검정색, 255는 흰색)``**

  - ``3차원(RGB) 데이터`` 이미지에서는 각 픽셀의 값이 ``0 ~ 255`` 사이의 **숫자**이며, **RGB 데이터의 값**을 표현 하고 있다.<br>
  ``[x][y][0] = R(빨강)``, ``[x][y][1] = G(초록)``, ``[x][y][2] = B(파랑)``

### ``class_names``이 필요한 이유
```python
class_names = ['airplane', 'automobile', 'bird', 'cat', 'deer',
               'dog', 'frog', 'horse', 'ship', 'truck']
```
- ``###_labels``에는 ``###_images``에 해당하는 정답 값이 들어있지만 그 값이 ``0, 1, ..., 9`` 이런 식으로 **정수** 형태로 들어있다.
- 따라서 ``###_labels`` 값을 ``index``로 사용해서 클래스 이름이 들어있는 배열인 ``class_names``와 연결해 사용한다.

#### 예시
```python
# train_images[3]의 클래스 이름이 "Cat" 일 때
class_names[train_labels[3]]
출력 : "Cat"
```

※ ``class_names``에서 정의한 값의 순서는 **``CIFAR-10``의 공식 클래스 순서** 에 맞춰서 작성한다.

**``📦 CIFAR-10 클래스 순서 (공식)``**

| 숫자 라벨 | 클래스 이름   |
|-----------|---------------|
| 0         | airplane      |
| 1         | automobile    |
| 2         | bird          |
| 3         | cat           |
| 4         | deer          |
| 5         | dog           |
| 6         | frog          |
| 7         | horse         |
| 8         | ship          |
| 9         | truck         |

*****
## 합성곱 층 만들기
- 이 챕터에서 **합성곱 층** 은 ``Conv2D``, ``MaxPooling2D``, ``Flatten``, ``Dense`` 등을 사용해서 **Sequential 모델** 에 층을 쌓는 작업을 한다.
- 이는 이미지로부터 **특징**을 ``추출`` 하고, 최종적으로 **분류 작업** 을 할 수 있도록 **모델의 구조**를 ``정의`` 하는 곳이다.<br>
**※ 즉, 훈련 모델을 구성하는 단계이다.**

### 출력된 표의 의미

| Layer (type)              | Output Shape         | Param #  |
|---------------------------|----------------------|----------|
| conv2d_3 (Conv2D)         | (None, 30, 30, 32)   |      896 |
| max_pooling2d_2 (MaxPooling2D) | (None, 15, 15, 32)   |        0 |
| conv2d_4 (Conv2D)         | (None, 13, 13, 64)   |   18,496 |
| max_pooling2d_3 (MaxPooling2D) | (None, 6, 6, 64)     |        0 |
| conv2d_5 (Conv2D)         | (None, 4, 4, 64)     |   36,928 |
| flatten (Flatten)         | (None, 1024)         |        0 |
| dense (Dense)             | (None, 64)           |   65,600 |
| dense_1 (Dense)           | (None, 10)           |      650 |


### Param
#### Param 이란?
- 해당 층에서 **학습 과정 중에 조정되는 값(가중치 + 편향)의 총 개수** 를 의미한다.

#### Conv2D 레이어의 Param 계산
```python
# Conv2D 레이어의 Param 계산 식
(filter_height * filter_width * 입력 채널 수 + bias(편향)) * 출력 채널 수
```
```python
# 예시 코드
1 | model.add(layers.Conv2D(32, (3, 3), activation='relu'))
2 | model.add(layers.MaxPooling2D((2, 2)))
3 | model.add(layers.Conv2D(64, (3, 3), activation='relu'))
```
- 3번째 코드를 기준으로 **필터(커널)** 의 크기는 ``3x3``이고 입력 채널이 ``32개``, 출력 채널이 ``64개`` 이다.  각 **필터(커널)** 는 ``9개`` 의 값(가중치)을 가지고 있고 ``채널 x 필터크기`` 개 만큼 값을 가지므로 ``3 x 3 x 32 = 288개``가 있다.
- 하지만 ``Conv2D`` 의 매개변수 ``use_bias`` 의 기본값이 ``True`` 이기 때문에 ``편향``을 사용하게 되므로 **편향의 개수** ``1`` 을 더해줘야 한다. ``※ 289개``
- 마지막으로, ``출력 채널 개수`` 를 **곱해주면**  해당 층에서 **조정되는 가중치와 편향의 총 개수(Param 수)** 가 계산된다. ``※ (289 * 64 = 18,496개)``

#### Dense 레이어의 Param 계산
```python
# Dense 레이어의 Param 계산식
1 | (입력 채널 수 + bias(편향)) * 출력 채널 수
                    또는
2 | 입력 채널 수 * 출력 채널 수 + (편향(bias) * 출력 채널 수)
```
```python
# 예시 코드
1 | model.add(layers.Flatten())
2 | model.add(layers.Dense(64, activation='relu'))
```
- 2번째 코드를 기준으로 **입력으로 들어오는 값**은 ``Flatten 레이어`` 의 **Output Shape**인 ``(None, 1024)``이므로 1번 계산식은 ``(1024 + 1) * 64 = 65,600``, 2번 계산식은 ``1024 * 64 + (1 * 64) = 65,600``이다.
- 계산식이 2개가 있지만 표현 방식의 차이일 뿐, 1번 식을 전개한 식이 2번 식이다.

#### 주의
- ``MaxPooling2D 레이어``는 **이미지의 크기를 줄이는 레이어**이기 때문에 **Param**이 0이다.
- ``Flatten 레이어``는 일렬로 나열 하기만 하는 레이어이기 때문에 **Param**이 0이다.

#### Flatten 레이어의 Output Shape
- **특징** 만을 뽑은 **압축된** ``3차원 데이터 이미지(가로, 세로, 채널)`` 를 ``1차원 벡터`` 로 **변환**하기 위해 ``가로 * 세로 * 출력 채널 수`` 만큼 곱해서 값을 **일렬로 나열**한다.
- 따라서, ``4 x 4 x 64``값인 ``1024``가 ``Flatten``의 출력 모양이다.

*****
## 모델 컴파일과 훈련
### 코드
```python
model.compile(optimizer='adam',
              loss=tf.keras.losses.SparseCategoricalCrossentropy(from_logits=True),
              metrics=['accuracy'])

history = model.fit(train_images, train_labels, epochs=10, 
                    validation_data=(test_images, test_labels))
```

- ``실제 데이터``와 ``구성한 모델``을 가지고 **학습**을 시키는 단계이다.

- ``compile 함수``를 통해서 모델의 **학습방법**을 정하고, ``fit 함수``로 **학습 데이터**를 넣은 다음 학습한다.

### 출력 결과
```python
# 마지막 Epoch 학습 결과
Epoch 10/10
1563/1563 ━━━━━━━━━━━━━━━━━━━━ 5s 3ms/step - accuracy: 0.7729 - loss: 0.6437 - val_accuracy: 0.7071 - val_loss: 0.8691
```
- ``accuracy``: 정확도 **(정답 확률)**
    - ``77.29%``의 **정답률**로 모델이 훈련 데이터에 대해 예측했다.
- `loss`: 손실 값 **(모델 예측이 정답과 얼마나 다른지 나타냄)**
    - 손실 값이 **낮을수록** 예측이 더 정확하다는 뜻이다. 현재 손실 값은 0.6437.<br>
    ※ **손실 값**은 ``퍼센트(%)``가 아니며, **손실 함수**에 따라서 ``log(10) ≈ 2.3`` 정도의 값도 나올 수 있다.
- ``val_accuracy``: **검증 데이터(validation data)** 의 정확도
    - 모델이 **본 적 없는 데이터**에 대해 ``70.71%``의 **정확도**로 예측했다.
- ``val_loss``: **검증 데이터(validation data)**의 손실 값
    - **손실 값**이 훈련보다 더 크면 **과적합(overfitting)**을 의심해볼 수 있다.

! ``loss``는 모델이 **얼마나 틀렸는지**, ``accuracy``는 모델이 **얼마나 맞췄는지** ``비율``로 측정한 값이다.

*****
## 모델 평가
```python
# Epoch 10/10 학습 결과
accuracy: 0.7729 - loss: 0.6437 - val_accuracy: 0.7071 - val_loss: 0.8691

# 검증 데이터 정확도 및 손실값
313/313 - 0s - 1ms/step - accuracy: 0.7071 - loss: 0.8691
```
![모델 평가](https://github.com/user-attachments/assets/5adeed62-fd50-4835-a284-ff8748ac92de)
- **accuracy** :
  - 훈련 데이터 정확도는 ``Epoch``가 진행될수록 ``accuracy``가 점점 올라가고 있다. 이는 모델이 훈련 데이터에 대해서 학습이 잘 되고 있다는 뜻이다.
- **val_accuracy** :
  - 검증 데이터 정확도는 ``Epoch``가 진행될수록 ``val_accuracy``가 올라가지만 일정 ``Epoch``이후 부터는 약간의 변동(오르내림)이 발생한다.

  **※** **훈련 데이터 정확도**는 ``77.29%``, **검증 데이터 정확도**는 ``70.71%``로 약 ``7%``의 차이가 나지만 그 차이가 **심하지 않기때문에** 과적합이 발생했다고 보기에는 어렵지만, **과적합이 시작되는 단계**로 볼 수 있다.
*****
## 참고
- [1. 텐서 기초 살펴보기](https://codetorial.net/tensorflow/basics_of_tensor.html) - 텐서에 대해서
- [[Pytorch]텐서의 정의](https://meaningful96.github.io/pytorch/pytorch1/) - 텐서 설명 이미지
- [[Keras & Tensorfow] 개념](https://golikeriver97.tistory.com/41) - keras에 대해서
- [CNN: Step 3— Flattening](https://medium.com/@PK_KwanG/cnn-step-2-flattening-50ee0af42e3e) - CNN 데이터 흐름

<!-- 
```python
model = models.Sequential()
model.add(layers.Conv2D(32, (3, 3), activation='relu', input_shape=(32, 32, 3)))
model.add(layers.MaxPooling2D((2, 2)))
model.add(layers.Conv2D(64, (3, 3), activation='relu'))
model.add(layers.MaxPooling2D((2, 2)))
model.add(layers.Conv2D(64, (3, 3), activation='relu'))

model.summary()
C:\Windows\System32\myTensorflow\lib\site-packages\keras\src\layers\convolutional\base_conv.py:107: UserWarning: Do not pass an input_shape/input_dim argument to a layer. When using Sequential models, prefer using an Input(shape) object as the first layer in the model instead.
  super().__init__(activity_regularizer=activity_regularizer, **kwargs)
  ```

합성곱 층 만들기에서 ``model.add(layers.Conv2D(32, (3, 3), activation='relu', input_shape=(32, 32, 3)))`` 이런식으로 첫번째 레이어에 shape을 직접 지정하는 것보다 Import 객체를 사용하는 것이 권장된다고 해서 코드 수정 -->