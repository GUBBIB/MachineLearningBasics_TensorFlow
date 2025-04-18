# RandomRotation()
## 하는 일
- **데이터 증강을 위한 레이어**로 이미지를 **무작위**로 ``회전``시켜 학습 데이터를 다양하게 만든다.

## 형식
```python
tf.keras.layers.RandomRotation(
    factor,          
    fill_mode="reflect",  
    interpolation="bilinear",  
    fill_value=0.0,  
    seed=None,       
    name=None        
)
```
*****
- **factor** : 회전 범위를 설정하는 매개변수이다.
    - ``0.0 ~ 1.0`` 사이의 **실수**를 입력받는다.

*****
- **fill_mode** : 회전으로 인해 생기는 빈 영역을 어떻게 채울지 결정한다.
- 기본값은 ``reflect``이며, ``constant``, ``nearset``, ``wrap``이 있다.
    - **reflect** : 주변의 픽셀을 **거울처럼 반사**해서 채운다. ``[[1, 2, 3] -> [3, 2, 1]]``
    - **constant** : 빈 곳을 ``검정색`` 같이 **한 가지 색**으로만 채운다.
    - **nearset** : **가장 가까운 픽셀 값**을 복사해서 채운다.
    - **wrap** : 이미지의 **반대쪽의 픽셀**로 채운다.

*****
- **interpolation** : ``회전`` 중 **픽셀 사이 값을 어떻게 계산할지** 정한다.
    - **bilinear(기본값)** : 가장 **자연스럽고 부드럽게** 만든다.
    - **nearset** : **계산은 빠르지만** 이미지가 **뚝뚝 끊기게** 나온다.

*****
- **seed** : ``RandomFlip`` 레이어의 결과값은 무작위로 나오지만 **항상 같은 결과가 나오게** 할 수 있는 매개변수이다.<br>
    - 주로 디버깅을 할 때 사용한다.

*****
- **name** : **모델** 안에서 **레이어에 고유 이름을 지정**할 수 있게 해주는 매개변수이다.
    - 주로 **모델 구조를 파악**하거나 **디버깅을 할 때** 유용하다.