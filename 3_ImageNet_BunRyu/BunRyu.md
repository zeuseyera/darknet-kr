
:kr: 다크넷(darknet): C로 작성한 신경망 공개소스 

출처: https://pjreddie.com/darknet

| [다크넷](../README.md) | [설치](../1_SeolChi/SeolChi.md) | [욜로](../2_YOLO/yolo.md) | [이미지넷분류](../3_ImageNet_BunRyu/BunRyu.md) | [악몽](../4_AkMong/AkMong.md) | [재사용신경망](../5_RNN/rnn.md) | [다크고](../6_DarkGo/DarkGo.md) | [꼬맹이망](../7_GgoMaengIi/GgoMaengIi.md) | [분류기수련](../8_SuRyeon/SuRyeon.md) |  
| --- | --- | --- | --- | --- | --- | --- | --- | --- |  

<a name="이미지넷-분류"></a>
## 3. 이미지넷 분류(ImageNet Classification)
다크넷을 사용하여 1000-분류 이미지넷 도전에 대한 이미지를 분류할 수 있다. 다크넷을 아직 설치하지 않았다면, 먼저 다크넷을 설치해야 한다.

### 1) 미리수련된 모형으로 분류(Classifying With Pre-Trained Models)
다음의 명령을 다크넷을 설치하기 위한 명령이다, 분류 가중값 파일을 내려받기한다, 그리고 이미지 분류기를 실행한다:
```bash
git clone https://github.com/pjreddie/darknet.git
cd darknet
make
wget https://pjreddie.com/media/files/extraction.weights
./darknet classifier predict cfg/imagenet1k.data cfg/extraction.cfg extraction.weights data/dog.jpg
```

이 본보기는 추출모형을 사용한다, 아래에서 더 많은것을 읽을 수 있다. 이 명령을 실행한 후에 다음의 출력을 볼수 있다:
```bash
0: Convolutional Layer: 224 x 224 x 3 image, 64 filters -> 112 x 112 x 64 image
1: Maxpool Layer: 112 x 112 x 64 image, 2 size, 2 stride
...
23: Convolutional Layer: 7 x 7 x 512 image, 1024 filters -> 7 x 7 x 1024 image
24: Convolutional Layer: 7 x 7 x 1024 image, 1000 filters -> 7 x 7 x 1000 image
25: Avgpool Layer: 7 x 7 x 1000 image
26: Softmax Layer: 1000 inputs
27: Cost Layer: 1000 inputs
Loading weights from extraction.weights...Done!
298 224
data/dog.jpg: Predicted in 3.756339 seconds.
malamute: 0.194782
Eskimo dog: 0.155007
Siberian husky: 0.143937
dogsled: 0.020943
miniature schnauzer: 0.020566
```

다크넷은 설정파일과 가중값을 탑재할 때 정보를 표시한다, 그런다음 이미지를 분류한다 그리고 이미지에 대한 상위-10개의 분류를 인쇄한다. 켈프는 잡종 개다 하지만 말라뮤트(알래스카 썰매개)성질이 많다 그래서 잘 성공할 수 있다!

또한 다른 이미지로 시도할 수 있다, 대머리독수리 이미지 같은:
```bash
./darknet classifier predict cfg/imagenet1k.data cfg/extraction.cfg extraction.weights data/eagle.jpg
```

생산된 것:
```bash
...
data/eagle.jpg: Predicted in 4.036698 seconds.
bald eagle: 0.797689
kite: 0.185116
vulture: 0.006402
prairie chicken: 0.001041
hen: 0.000888
```

아주 좋다!

이미지 파일을 지정하지 않으면 실행중에 이미지에 대해 묻는다. 이렇게하면 전체 모형을 다시탑재를 하지 않고 연속해서 여러개를 분류할 수 있다. 다음 명령을 사용한다:
```bash
./darknet classifier predict cfg/imagenet1k.data cfg/extraction.cfg extraction.weights
```

그러면 다음과 같은 보여줌을 얻는다:
```bash
....
27: Softmax Layer: 1000 inputs
28: Cost Layer: 1000 inputs
Loading weights from extraction.weights...Done!
Enter Image Path:
```

이미지 분류가 지루해지면 언제나 프로그램을 종료하기 위해 Ctrl-C를 사용할 수 있다.

### 2) 이미지넷 검증(Validating On ImageNet)

사방에 뿌려진 검증집합 번호를 볼 수 있다. 아마도 스스로 이중으로 확인하고 싶을 것이다 이러한 모형이 실제로 얼마나 잘 작동하는지. 이것을 해보자!

먼저 검증 이미지를 내려받기할 필요가 있다, 그리고 cls-loc 주석을. 여기에서 그것들을 얻을 수 있다 하지만 계정을 만들어야 한다! 일단 모든것을 내려받기한다 ILSVRC2012_bbox_val_v3.tgz와 ILSVRC2012_img_val.tar이 있는 디렉토리가 있어야한다. 먼저 이것들의 압축을 푼다:
```bash
tar -xzf ILSVRC2012_bbox_val_v3.tgz
mkdir -p imgs && tar xf ILSVRC2012_img_val.tar -C imgs
```

```bash
ILSVRC : 이미지넷 대규모 시각인식 도전(ImageNet Large Scale Visual Recognition Challenge)
```

이제 이미지와 주석을 가지고 있다 하지만 이미지에 딱지를 붙일 필요가 있다 그렇게 해서 다크넷이 예측한 것을 평가할 수 있다. 이 배쉬스크립트(bash script)를 사용한다. 이것은 이미 scripts/ 하위디렉토리에 있다. 그렇지만 그냥 이것을 다시 가져올 수 있다 그리고 이것을 실행한다:
```bash
wget https://pjreddie.com/media/files/imagenet_label.sh
bash imagenet_label.sh
```

이것은 두가지를 생성한다: 이름이 변경된 이미지에 대한 연결기호가 포함된 labelled/ 라고 하는 디렉토리와 딱지가 붙은 이미지의 경로 목록이 포함된 inet.val.list 라고 하는 파일. 다크넷의 하위디렉토리인 data/ 이 파일을 이동할 필요가 있다:
```bash
mv inet.val.list <path-to>/darknet/data
```

이제 마침내 모형을 검증할 준비가 되었다! 먼저 다크넷을 다시 만든다. 그 다음에 검증 경로를 실행한다 이렇게:
```bash
./darknet classifier valid cfg/imagenet1k.data cfg/extraction.cfg extraction.weights
```

알림: 만약 OpenCV로 다크넷을 컴파일하지 않으면 이미지넷 이미지 전부를 탑재할 수 없다 그중 일부는 stb_image.h로 지원되지 않는 별난 형식이기 때문이다.

만약 쿠다로 컴파일하지 않아도 여전히 이미지넷을 검증할 수 있다 하지만 이것은 정말정말로 오랜 시간이 걸릴 것이다. 권장하지 않는다.

### 3) 미리수련된 모형(Pre-Trained Models)

Here are a variety of pre-trained models for ImageNet classification. Accuracy is measured as single-crop validation accuracy on ImageNet. GPU timing is measured on a Titan X, CPU timing on an Intel i7-4790K (4 GHz).
여기에 이미지넷 분류를 위해 미리수련된 다양한 모형이 있다. 정밀도는 이미지넷에서 단일집단(single-crop) 검증 정밀도로 측정된 것이다. GPU 시간은 Titan X로 측정됨, CPU 시간은 인텔 Intel i7-4790K(4 GHz)로.

Model        | Top-1        | Top-5        | Ops          | GPU          | CPU          | Cfg          | Weights  
------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------  
AlexNet      | 57.0         | 80.3         | 2.27 Bn      | 1.5 ms       | 0.3 s        | [cfg](https://github.com/pjreddie/darknet/blob/master/cfg/alexnet.cfg)          | [285 MB](https://pjreddie.com/media/files/alexnet.weights)  
Darknet Reference | 61.1 | 83.0 |  0.81 Bn |  1.5 ms | 0.16 s | [cfg](https://github.com/pjreddie/darknet/blob/master/cfg/darknet.cfg) | [28 MB](https://pjreddie.com/media/files/darknet.weights)  
VGG-16            | 70.5 | 90.0 | 30.94 Bn | 10.7 ms | 4.9 s  | [cfg](https://github.com/pjreddie/darknet/blob/master/cfg/vgg-16.cfg) | [528 MB](https://pjreddie.com/media/files/vgg-16.weights)  
Extraction        | 72.5 | 90.8 |  8.52 Bn |  6.4 ms | 0.95 s | [cfg](https://github.com/pjreddie/darknet/blob/master/cfg/extraction.cfg) | [90 MB](https://pjreddie.com/media/files/extraction.weights)  
Darknet19         | 72.9 | 91.2 |  5.58 Bn |  6.0 ms | 0.66 s | [cfg](https://github.com/pjreddie/darknet/blob/master/cfg/darknet19.cfg) | [80 MB](https://pjreddie.com/media/files/darknet19.weights)  
Darknet19 448x448 | 76.4 | 93.5 | 22.33 Bn | 11.0 ms | 2.8 s  | [cfg](https://github.com/pjreddie/darknet/blob/master/cfg/darknet19_448.cfg) | [80 MB](https://pjreddie.com/media/files/darknet19_448.weights)  
Resnet 50         | 75.8 | 92.9 | 10 Bn    |  7.0 ms | ?? s   | [cfg](https://github.com/pjreddie/darknet/blob/master/cfg/resnet50.cfg) | [87 MB](https://pjreddie.com/media/files/resnet50.weights)  
Resnet 152        | 77.6 | 93.8 | 29.4 Bn  | ?? ms   | ?? s   | [cfg](https://github.com/pjreddie/darknet/blob/master/cfg/resnet152.cfg) | [220 MB](https://pjreddie.com/media/files/resnet152.weights)  
Densenet 201      | 77.0 | 93.7 | 10.9 Bn  | ?? ms   | ?? s   | [cfg](https://github.com/pjreddie/darknet/blob/master/cfg/densenet201.cfg) | [66 MB](https://pjreddie.com/media/files/densenet201.weights)  

#### 3-1) 알렉스넷(AlexNet)
이 모형은 혁명의 시작이다! [원본](http://www.cs.toronto.edu/~fritz/absps/imagenet.pdf) 모형은 GPU 분할 작업으로 굉장히 좋았다 그래서 이것은 많은 [후속 작업](http://arxiv.org/abs/1404.5997)의 모형이다.
- Top-1 정확도: 57.0%
- Top-5 정확도: 80.3%
- 순방향 시간: 1.5 ms/img
- CPU 순방향 시간: 0.3 s/img
- [설정(cfg) 파일](https://github.com/pjreddie/darknet/blob/master/cfg/alexnet.cfg)
- [가중값(weight) 파일 (285 MB)](http://pjreddie.com/media/files/alexnet.weights)

#### 3-2) Darknet Reference Model
이 모형은 작게 설계되었다 하지만 강력하다. 이것은 알렉스넷과 같은 top-1과 top-5와 동일 성능을 달성했다 하지만 참여는 1/10로. 이것은 끝에 큰 완전연결층 없이 대부분 나선층을 사용한다. 이것은 CPU 상에서 알렉스넷 보다 약 2배 빠르다 이것은 많은 시각 응용프로그램에 더욱 적합하다.
- Top-1 정확도: 61.1%
- Top-5 정확도: 83.0%
- 순방향 시간: 1.5 ms/img
- CPU 순방향 시간: 0.16 s/img
- [설정(cfg) 파일](https://github.com/pjreddie/darknet/blob/master/cfg/darknet.cfg)
- [가중값(weight) 파일 (28 MB)](http://pjreddie.com/media/files/darknet.weights)

#### 3-3) VGG-16
ILSVRC-2014 대회를 위하여 옥스포드의 [시각기하학무리(The Visual Geometry Group)](http://www.robots.ox.ac.uk/~vgg/research/very_deep/)가 VGG-16 모형을 개발했다. 이것은 매우 정확하고 분류와 검출을 위하여 널리 사용된다. 나는 [카페(Caffe)](http://caffe.berkeleyvision.org/)의 미리수련된 [모형](https://gist.github.com/ksimonyan/211839e770f7b538e2d8#file-readme-md)으로 이판을 개조했다. 이것은 다크넷-지정 이미지 전처리로 조정하기 위하여 추가적으로 6세대 수련했다(평균빼기 대신에 다크넷은 -1과 1 사이로 이미지를 조정한다).
- Top-1 정확도: 70.5%
- Top-5 정확도: 90.0%
- 순방향 시간: 10.7 ms/img
- CPU 순방향 시간: 4.9 s/img
- [설정(cfg) 파일](https://github.com/pjreddie/darknet/blob/master/cfg/vgg-16.cfg)
- [가중값(weight) 파일 (528 MB)](http://pjreddie.com/media/files/vgg-16.weights)

#### 3-4) Extraction
나는 [구글넷(GoogleNet) 모형](http://arxiv.org/abs/1409.4842)의 파생물로 이 모형을 개발했다. 이것은 "마수(인셉션, inception)" 구성물(module)을 사용하지 않는다, 오직 1x1 과 3x3 나선층이다.
- Top-1 정확도: 72.5%
- Top-5 정확도: 90.8%
- 순방향 시간: 6.4 ms/img
- CPU 순방향 시간: 0.95 s/img
- [설정(cfg) 파일](https://github.com/pjreddie/darknet/blob/master/cfg/extraction.cfg)
- [가중값(weight) 파일 (90 MB)](http://pjreddie.com/media/files/extraction.weights)

#### 3-5) Darknet19
나는 추출망을 더 빠르고 정밀하게 수정했다. 이 망은 다크넷 기준망 그리고 추출망, 망안의 망, 시작(인셉션), 그리고 뭉치고르기(Batch Normalization) 처럼 수많은 출판물의 아이디어를 하나로 합친 것이다.
- Top-1 정확도: 72.9%
- Top-5 정확도: 91.2%
- 순방향 시간: 6.0 ms/img
- CPU 순방향 시간: 0.66 s/img
- [설정(cfg) 파일](https://github.com/pjreddie/darknet/blob/master/cfg/darknet19.cfg)
- [가중값(weight) 파일 (80 MB)](http://pjreddie.com/media/files/darknet19.weights)

#### 3-6) Darknet19 448x448
나는 입력 이미지 크기가 큰 것으로 10세대 이상 Darknet19를 수련하였다, **448x448**. 이 모형은 상당히 좋은 수행을 한다 하지만 전체이미지가 크기 때문에 느리다.
- Top-1 정확도: 76.4%
- Top-5 정확도: 93.5%
- 순방향 시간: 11.0 ms/img
- CPU 순방향 시간: 2.8 s/img
- [설정(cfg) 파일](https://github.com/pjreddie/darknet/blob/master/cfg/darknet19_448.cfg)
- [가중값(weight) 파일 (80 MB)](http://pjreddie.com/media/files/darknet19_448.weights)

#### 3-7) Resnet 50
어떤 이유인지 사람들은 이 망을 좋아한다 비록 너무너무 느리지만. 도대체 무엇인가. [논문](https://arxiv.org/abs/1512.03385)
- Top-1 정확도: 75.8%
- Top-5 정확도: 92.9%
- 순방향 시간: ?? ms/img
- CPU 순방향 시간: ?? s/img
- [설정(cfg) 파일](https://github.com/pjreddie/darknet/blob/master/cfg/resnet50.cfg)
- [가중값(weight) 파일 (87 MB)](https://pjreddie.com/media/files/resnet50.weights)

#### 3-8) Resnet 152
어떤 이유인지 사람들은 이 망을 좋아한다 비록 너무너무 느리지만. 도대체 무엇인가. [논문](https://arxiv.org/abs/1512.03385)
- Top-1 정확도: 77.6%
- Top-5 정확도: 93.8%
- 순방향 시간: ?? ms/img
- CPU 순방향 시간: ?? s/img
- [설정(cfg) 파일](https://github.com/pjreddie/darknet/blob/master/cfg/resnet152.cfg)
- [가중값(weight) 파일 (220 MB)](https://pjreddie.com/media/files/resnet152.weights)

#### 3-9) Densenet 201
나는 덴스넷(DenseNets)을 좋아한다! 이것은 너무 깊다 그리고 아주 미친듯이 너무 잘 작동한다. 레스넷(Resnet) 처럼, 너무너무 많은층 때문에 여전히 느리다 하지만 적어도 이것은 정말로 잘 작동한다! [논문](https://arxiv.org/abs/1608.06993)
- Top-1 정확도: 77.0%
- Top-5 정확도: 93.7%
- 순방향 시간: ?? ms/img
- CPU 순방향 시간: ?? s/img
- [설정(cfg) 파일](https://github.com/pjreddie/darknet/blob/master/cfg/densenet201.cfg)
- [가중값(weight) 파일 (67 MB)](https://pjreddie.com/media/files/densenet201.weights)

---
