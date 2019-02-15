
:kr: 다크넷(darknet): C로 작성한 신경망 공개소스 

출처: https://pjreddie.com/darknet

| [다크넷](../README.md) | [설치](../1_SeolChi/SeolChi.md) | [욜로](../2_YOLO/yolo.md) | [이미지넷분류](../3_ImageNet_BunRyu/BunRyu.md) | [악몽](../4_AkMong/AkMong.md) | [재사용신경망](../5_RNN/rnn.md) | [다크고](../6_DarkGo/DarkGo.md) | [꼬맹이망](../7_GgoMaengIi/GgoMaengIi.md) | [분류기벼림](../8_SuRyeon/SuRyeon.md) | [사용방법](../SaYongBeob_Yolo-v3.md) |  
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |  

<a name="CIFAR-10-분류기"></a>
## 8. CIFAR-10 으로 분류기를 벼림(Train a Classifier on CIFAR-10)

 이 게시는 다크넷을 처음부터 분류기를 벼림하는 방법을 가르칠 것이다. 우리는 [CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html) 자료집합을 가지고 놀것이다, 10 분류의 작은 이미지 자료집합. 시작하자!

### 1) 다크넷 설치

 만약 아직 설치하지 않은 경우, 다음을 하라:

```
git clone https://github.com/pjreddie/darknet
cd darknet
make
```

 만약 모든 작업을 했다면, 훌륭하다! 만약 뭔가 잘못됐다면... 음... 그것을 고쳐라?

### 2) 자료 가져오기

 우리는 CIFAR 자료의 내 복제본을 사용할 것이다 왜냐하면 우리는 이미지형식의 사진을 원하기 때문이다. 원본 자료집합은 바이너리형식으로 되어있다 하지만 내가 원하는 이 지침은 당신이 작업하길 원하는 모든 자료집합을 일반화하는 것이다, 그래서 우리는 대신이 이미지인 이것으로 할 것이다.

 `data/` 폴더에 자료를 밀어넣자. 그것을 하기위해 실행:

```
cd data
wget https://pjreddie.com/media/files/cifar.tgz
tar xzf cifar.tgz
```

 이제 우리가 가진것이 무엇인지 보자:

```
ls cifar
```

 우리의 자료뢰 두개의 디렉토리를 나열한다, `train`(벼림) 과 `test`(평가), 그리고 딱지가 있는 파일, `labels.txt`. 당신은 `labels.txt`를 볼수 있다 만약 당신이 원한다면 그리고 우리가 벼림할 분류종륙가 무엇인지 봐라:

```
cat cifar/labels.txt
```

 우리는 또한 우리의 파일경로를 생성할 필요가 있다. 이러한 파일은 벼림과 검증(또는 이 경우에는 평가) 자료의 모든 경로를 가질것이다. 그것을 하기 위해, 우리는 `cd(디렉토리변경)`로 `cifar`디렉토리 안으로 이동, `find`로 모든 이미지를 찾는다, 그리고 파일로 그것들을 기록한다, 그런다음 우리의 **다크넷** 기본디렉토리로 돌아간다.

```
cd cifar
find `pwd`/train -name \*.png > train.list
find `pwd`/test -name \*.png > test.list
cd ../..
```

### 3) 자료집합 구성파일 만들기

```
메타데이타(metadata): 더높은, 초월한 자료
```

 우리는 다크넷에 CIFAR-10에 관한 약간의 메타데이타를 줘야한다. 자신이 좋아하는 편집기를 사용하여, `cfg/` 디렉토리에서 `cfg/cifar.data`라는 새로운 파일을 열어라. 그 안에는 다음과 같은 것이 있어야 한다:

```
classes=10
train  = data/cifar/train.list
valid  = data/cifar/test.list
labels = data/cifar/labels.txt
backup = backup/
top=2
```

  * `classes = 10` : 자료집합이 가진 10개의 다른 분류
  * `train   = ...`: 벼림파일 목록을 찾는 위치
  * `valid   = ...`: 검증파일 목록을 찾는 위치
  * `labels  = ...`: 분류가능 목록을 찾는 위치
  * `backup  = ...`: 벼림하는 동안 예비(backup)가중값을 저장하는 위치
  * `top     = 2`  : 평가시에 상위 n(top-n)개의 정확도 계산(상위 1개에 추가로)


### 4) 망 구성파일을 만든다!

 우리는 벼림하기위한 망이 필요하다. 자신의 `cfg` 디렉토리에 `cfg/cifar_small.cfg`라는 또다른 파일을 만든다. 그 안에 이 망을 넣어라:

```
[net]
batch=128
subdivisions=1
height=28
width=28
channels=3
max_crop=32
min_crop=32

hue=.1
saturation=.75
exposure=.75

learning_rate=0.1
policy=poly
power=4
max_batches = 5000
momentum=0.9
decay=0.0005

[convolutional]
batch_normalize=1
filters=32
size=3
stride=1
pad=1
activation=leaky

[maxpool]
size=2
stride=2

[convolutional]
batch_normalize=1
filters=16
size=1
stride=1
pad=1
activation=leaky

[convolutional]
batch_normalize=1
filters=64
size=3
stride=1
pad=1
activation=leaky

[maxpool]
size=2
stride=2

[convolutional]
batch_normalize=1
filters=32
size=1
stride=1
pad=1
activation=leaky

[convolutional]
batch_normalize=1
filters=128
size=3
stride=1
pad=1
activation=leaky

[convolutional]
batch_normalize=1
filters=64
size=1
stride=1
pad=1
activation=leaky

[convolutional]
filters=10
size=1
stride=1
pad=1
activation=leaky

[avgpool]

[softmax]
```

 이것은 정말로 작은 망이다 그래서 이것은 아주잘 작동하지는 않을것이다 하지만 이 본보기에 대해서는 좋다. 망은 오직 4개의 나선(convolutional)층과 2개의 최대모음(maxpooling)층이다.

 마지막 나선층은 10개의 거르개(filters )가 있다 왜냐하면 10개의 분류(classes)를 가지기 때문이다. 이것은 `7 x 7 x 10` 이미지를 출력한다. 우리는 오직 총 10개의 예측을 원한다 그래서 우리는 각 채널에 대한 이미지 전체에 걸쳐 평균을 취하기 위해 하나의 평균모음층을 사용한다. 이것은 우리에게  10개의 예측을 제공할 것이다. 우리는 확률분포로 예측을 변환하기 위해 [소프트맥스](https://en.wikipedia.org/wiki/Softmax_function)를 사용한다. 이 층은 또한 크로스엔트로피 손실로 오차를 계산한다.


### 5) 모형 벼림

 이제 우리는 바로 벼림코드를 실행해야 한다!

```
./darknet classifier train cfg/cifar.data cfg/cifar_small.cfg
```

 그리고 진행을 봐라!

 당신은 단지 분류기(`classifier`)를 벼림(`train`)하기를 원한다고 다크넷에게 말하는 것이다 다음 자료(`cfg/cifar.data`)와 망 구성파일(`cfg/cifar_small.cfg`)을 사용하여. CPU로 벼림은 1시간 이상 걸릴수 있다, 작은 망임에도 불구하고. 만약 GPU를 가지고 있다면 [:kr:이러한 명령](../1_SeolChi/SeolChi.md#cuda)[(영문)](https://pjreddie.com/darknet/install/#cuda)에 따라 GPU벼림 사용하기를 해야한다.

#### 5-1) 벼림 재시작

 만약 벼림을 멈췄다면 당신은 이 방법에 따라 저장한 모형 확인지점 하나를 사용하여 항상 재시작할수 있다:

```
./darknet classifier train cfg/cifar.data cfg/cifar_small.cfg backup/cifar_small.backup
```

### 6) 모형 검증

 이제 우리는 우리의 모형이 얼마나 잘 작동하는지 살펴봐야 한다. 우리는 검증(`valid`) 명령을 사용하여 상위-1 과 상위-2 검증 정밀도를 계산할수 있다. 우리는 예비(backup)로 검증을 실행할수 있다, 최종 가중값 파일로, 아니면 모든 저장된 세대별 가중값 파일로:

```
./darknet classifier valid cfg/cifar.data cfg/cifar_small.cfg backup/cifar_small.backup
```

 당신은 자신의 정밀도를 말해주는 숫자가 말리는 다발을 볼수 있다.

---
