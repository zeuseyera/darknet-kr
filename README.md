:kr: 다크넷(darknet): C로 작성한 신경망 공개소스  

출처:  
- https://github.com/pjreddie/darknet
- https://pjreddie.com/darknet

---
<p align="center"><img width="30%" src="images/darknet.png" /></p>  

---
# 다크넷(darknet): C로 작성한 신경망 공개소스
다크넷은 C와 쿠다로 작성한 공개소스 신경망 작업틀이다. 이것은 빠르고, 설치가 쉽다, 그리고 CPU 와 GPU 계산을 지원한다.  

---

## [1. 다크넷 설치(Installing Darknet)](#다크넷-설치)
다크넷은 설치와 실행이 쉽다. 이 게시는 이것을 통해 안내한다.

## [2. 욜로: 실시간 개체 검출(YOLO: Real-Time Object Detection)](#욜로)
욜로는(YOLO, 너는 오직 한번만 본다) 최첨단 기술이다, 실시간 개체 검출 시스템.
<p align="right"><img width="10%" src="images/yologo_1.png" /></p>  

## [3. 이미지넷 분류(ImageNet Classification)](#이미지넷-분류)
알렉스넷과 VGG-16과 같은 인기있는 모델로 이미지를 분류한다.

## [4. 악몽(Nightmare)](#악몽)
유령, 악귀(ghouls), 그리고 기괴한 야생 오소리(badgermoles)를 만들어내는 마술에 다크넷의 숨겨진 마법을 사용한다. 하지만, 경고한다, 여기에 들어간 자들에게: 악몽의 땅에서 아무도 안전하지 않다.
<p align="right"><img width="10%" src="images/nightmare-01.png" /></p>  

## [5. 다크넷으로 작성한 재사용신경망(RNNs in Darknet)](#재사용-신경망)
재사용신경망은 순차(time-series)자료와 자연어처리(NLP: Natural Language Processing)에 대한 유행의 전부이다. 다크넷에서 어떻게 사용하는지 배워라!

## [6. 다크고: 다크넷으로 작성한 바둑(DarkGo: Go in Darknet)](#다크고)
다크넷으로 수련된 정책망을 사용하여 바둑놀이를 한다.

## [7. 꼬맹이 다크넷(Tiny Darknet)](#꼬맹이-다크넷)
이미지 분류를 꼬맹이(아주작게)로 만들었다.

## [8. CIFAR-10 으로 분류기를 수련한다(Train a Classifier on CIFAR-10)](#CIFAR-10-분류기)
다크넷에서 분류자를 어떻게 수련하는지 기초부터 배운다.

## [9. 장비 안내: GPU 로 신경망](#장비-안내)
Hardware Guide: Neural Networks on GPUs (Updated 2016-1-30)
많은 사람들이 나에게 물었다 시각응용프로그램을 위한 신경망 수련을 위하여 권장하는 장비가 무엇인지. 이것은 내생각의 일부이다.

## 10. 인용(Cite)
다크넷을 연구에 사용한다면 이것을 인용하시오:
```
@misc{darknet13,
  author =   {Joseph Redmon},
  title =    {Darknet: Open Source Neural Networks in C},
  howpublished = {\url{http://pjreddie.com/darknet/}},
  year = {2013--2016}
}
```

## 11. 연락(Contact)  
다크넷에 관한 질문이나 도움을 받으려면 [다크넷 메일목록](https://groups.google.com/forum/#!forum/darknet)에 연락하시오. 가능한 한 빨리 질문에 답변할 것이다.  

---
<a name="다크넷-설치"></a>
## 1. 다크넷 설치
다크넷은 선택적인 의존성이 2개뿐 이므로 설치가 쉽다:  
- **OpenCV**: 지원하는 이미지 유형이 다양하게 넓은것을 원한다면  
- **CUDA**: GPU 계산을 원한다면  
둘 다 선택사항이다 그러므로 기본시스템만 설치하고 그냥 시작하자. 나는 리눅스와 맥컴퓨터 에서만 이것을 평가했다. 이것이 작동하지 않으면, 나 또는 누구에게든 전자우편을 보내라?

### 1) 기본시스템 설치(Installing The Base System)
먼저 [여기](https://github.com/pjreddie/darknet)에 있는 다크넷 깃 저장소를 복제하라. 이것은 다음고 같이 해낼 수 있다:  

```bash
git clone https://github.com/pjreddie/darknet.git
cd darknet
Make
```

이 작업을 하면 반드시 컴파일 정보의 완전한 전체뭉치를 봐야한다 흐름에 따른:  
```bash
mkdir -p obj
gcc -I/usr/local/cuda/include/  -Wall -Wfatal-errors  -Ofast....
gcc -I/usr/local/cuda/include/  -Wall -Wfatal-errors  -Ofast....
gcc -I/usr/local/cuda/include/  -Wall -Wfatal-errors  -Ofast....
.....
gcc -I/usr/local/cuda/include/  -Wall -Wfatal-errors  -Ofast -lm....
```

어떤 오류가 있다면, 그것들을 수정하라? 모든것이 올바르게 컴파일 된 것처럼 보인다면, 실행하라!  
```bash
./darknet
```

반드시 출력 결과를 얻어야 한다:  
```bash
용법: ./darknet <기능>
```
훌륭하다! 이제 멋진 것들을 확인해 보라 [여기](https://pjreddie.com/darknet/)에 있는 다크넷으로 할 수 있다.

### 2) 쿠다로 컴파일(Compiling With CUDA)
다크넷은 CPU에서 빠르다 하지만 GPU에서는 500배 더 빠르다! **엔비디아(Nvidia) GPU** 가 있어야 한다 그리고 **쿠다(CUDA)** 를 설치해야 한다. 나는 자세하게 쿠다 설치를 다루지 않겠다 왜냐하면 이것은 끔찍한 것이다.  

일단 쿠다를 설치했다면, 기본 디렉토리로에서 **만들기파일(Makefile)** 의 첫행을 다음과 같이 변경하라 읽기위하여:  
```
GPU=1  
```

이제 과제를 **만들 수 있다** 그리고 쿠다는 활성화 된다. 기본적으로 시스템에서 0번째 그래픽카드로 망이 실행한다(쿠다를 올바르게 설치했다면 **nvidia-smi(Nvidia-System Management Interface)** 를 사용하여 그래픽카드를 나열할 수 있다). 다크넷이 사용하는 카드를 바꾸고 싶다면 선택적 명령줄에 **-i <고유번호>** 정보표시를 줄 수 있다, 다음처럼:  
```
./darknet -i 1 imagenet test cfg/alexnet.cfg alexnet.weights  
```

만약 쿠다를 사용하여 컴파일 했다 하지만 어떠한 이유로 든 CPU 계산을 원한다면 대신에 CPU를 사용하기 위하여 **-nogpu** 를 사용할 수 있다:  
```
./darknet -nogpu imagenet test cfg/alexnet.cfg alexnet.weights  
```

새로운, 초고속 신경망을 즐겨라!  
  
### 3) OpenCV로 컴파일(Compiling With OpenCV)
기본적으로, 다크넷은 이미지 탑재를위하여 **stb_image.h** 를 사용한다. 색다른 양식을 위하여 더 많은 지원을 원한다면(CMYK jpeg 처럼) 대신에 **OpenCV** 를 사용할 수 있다! OpenCV는 또한 디스크에 저장하지 않고 이미지를 보고 검출할 수 있다.  

먼저 OpenCV를 설치하라. 원본으로 이것을 한다면 길고 복잡할 것이다 그러므로 너를 위하여 패키지 관리자를 얻기 위하여 노력하라.  

그런다음, **만들기파일(Makefile)** 의 두번째행을 다음과 같이 변경하라 읽기위하여:  
```
OPENCV=1  
```

끝났다! 시도해 보기 위한, 먼저 과제를 다시 **만든다**. 그 다음에 평가를위한 **imtest** 순서를 사용하여 이미지를 탑재하고 표시한다:  
```
./darknet imtest data/eagle.jpg  
```

If you get a bunch of windows with eagles in them you've succeeded! They may look like:
독수리가 있는 창 뭉치를 가지고 있다면 성공한 것이다! 그것은 다음처럼 보일 것이다:
<p align="center"><img width="70%" src="images/Screen_Shot_2015-06-10_at_2_47_08_PM.png" /></p>

---
<p align="center"><img width="30%" src="images/yologo_1.png" /></p>  

## 2. 욜로: 실시간 개체 검출(YOLO: Real-Time Object Detection)
욜로는(YOLO, 너는 오직 한번만 본다) 최첨단 기술이다, 실시간 개체 검출 시스템. 타이탄 X에서 40-90 FPS로 이미지를 처리한다 그리고 VOC 2007에 대해서 78.6%의 mAP를 가진다 그리고 COCO에 대해서 48.1%의 mAP 평가편차(test-dev)를 가진다.

![욜로 v2](https://www.youtube.com/watch?v=VOC3huqHrss)
<p align="center"><img width="30%" src="https://www.youtube.com/watch?v=VOC3huqHrss" /></p>  

모형(Model)     | 수련(Train) | 평가 | mAP | FLOPS | FPS | Cfg | Weights |  
------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ | ------------ |  
Old YOLO       | VOC 2007+2012 | 2007 | 63.4 | 40.19 Bn | 45 | - | [link](https://pjreddie.com/darknet/yolov1/)  
SSD300         | VOC 2007+2012 | 2007 | 74.3 | - | 46 | - | [link](https://arxiv.org/abs/1512.02325)  
SSD500         | VOC 2007+2012 | 2007 | 76.8 | - | 19 | - | [link](https://arxiv.org/abs/1512.02325)  
YOLOv2         | VOC 2007+2012 | 2007 | 76.8 | 34.90 Bn | 67 | [cfg](https://github.com/pjreddie/darknet/blob/master/cfg/yolo-voc.cfg) | [weights](https://pjreddie.com/media/files/yolo-voc.weights)  
YOLOv2 544x544 | VOC 2007+2012 | 2007 | 78.6 | 59.68 Bn | 40 | [cfg](https://github.com/pjreddie/darknet/blob/master/cfg/yolo-voc.cfg) | [weights](https://pjreddie.com/media/files/yolo-voc.weights)  
Tiny YOLO      | VOC 2007+2012 | 2007 | 57.1 | 6.97 Bn | 207 | [cfg](https://github.com/pjreddie/darknet/blob/master/cfg/tiny-yolo-voc.cfg) | [weights](https://pjreddie.com/media/files/tiny-yolo-voc.weights)  
SSD300         | COCO trainval | test-dev | 41.2 | - | 46 | - | [link](https://arxiv.org/abs/1512.02325)  
SSD500         | COCO trainval | test-dev | 46.5 | - | 19 | - | [link](https://arxiv.org/abs/1512.02325)  
YOLOv2 608x608 | COCO trainval | test-dev | 48.1 | 62.94 Bn | 40 | [cfg](https://github.com/pjreddie/darknet/blob/master/cfg/yolo.cfg) | [weights](https://pjreddie.com/media/files/yolo.weights)  
Tiny YOLO      | COCO trainval | - | - | 7.07 Bn | 200 | [cfg](https://github.com/pjreddie/darknet/blob/master/cfg/tiny-yolo.cfg) | [weights](https://pjreddie.com/media/files/tiny-yolo.weights)
```
mAP : 평균정밀도 평균(Mean Average Precision)
Bn : 백만(Million)
cfg : 신경망 설정내용
Weights : 신경망 가중값
```

### 1) 이것은 어떻게 동작하는가.(How It Works)
이전 검출 시스템은 검출을 수행하기 위해 분류기 또는 유도기를 용도에 맞게 변경한다. 그것은 위치와 눈금을 여러개로 이미지에 적용한다. 이미지영역의 점수가 높으면 검출로 간주한다.
 
우리는 완전히 다른 접근방식을 사용한다. 우리는 전체이미지에 단일 신경망을 적용한다. 이 망은 이미지를 여러 영역으로 나눈다 그리고 경계상자와 각 영역에 대한 확률을 예측한다. 이러한 경계상자는 예측된 확률로 가중된 것이다.


