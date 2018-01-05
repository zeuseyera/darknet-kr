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
<a name="그냥-실행"></a>
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
<a name="욜로"></a>
<p align="center"><img width="30%" src="images/yologo_1.png" /></p>  

## 2. 욜로: 실시간 개체 검출(YOLO: Real-Time Object Detection)
욜로는(YOLO, 너는 오직 한번만 본다) 최첨단 기술이다, 실시간 개체 검출 시스템. 타이탄 X에서 40-90 FPS로 이미지를 처리한다 그리고 VOC 2007에 대해서 78.6%의 mAP를 가진다 그리고 COCO에 대해서 48.1%의 mAP 평가편차(test-dev)를 가진다.
```
욜로 v2 동영상: https://www.youtube.com/watch?v=VOC3huqHrss
```
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

### 1) 이것은 어떻게 동작하는가.
이전 검출 시스템은 검출을 수행하기 위해 분류기 또는 유도기를 용도에 맞게 변경한다. 그것은 위치와 눈금을 여러개로 이미지에 적용한다. 이미지영역의 점수가 높으면 검출로 간주한다.
 
우리는 완전히 다른 접근방식을 사용한다. 우리는 전체이미지에 단일 신경망을 적용한다. 이 망은 이미지를 여러 영역으로 나눈다 그리고 경계상자와 각 영역에 대한 확률을 예측한다. 이러한 경계상자는 예측된 확률로 가중된 것이다.  
<p align="center"><img width="100%" src="images/model2.png" /></p>  

우리의 모델은 분류기기반 시스템에 비해 몇가지 장점을 가진다. 평가시 이미지전체 를 확인한다 그래서 이것의 예측은 이미지에서 전체맥락으로 된 정보이다. 이것은 또한 하나의 이미지에 수천개가 필요한 [R-CNN](https://github.com/rbgirshick/rcnn) 과 달리 하나의 망으로 평가하여 예측한다. 이것은 극도로 빠르게 한다, R-CNN보다 1000배 더 빠르다 그리고 [Fast R-CNN](https://github.com/rbgirshick/fast-rcnn) 보다 100배 빠르다.  전체 시스템에 대한 자세한 내용은 우리의 [논문](https://arxiv.org/abs/1612.08242) 을 봐라.

### 2) 버전 2에서 새로운것은 무엇인가?
YOLOv2는 수련과 성능향상을 개선하귀 위하여 몇가지 묘책을 사용한다. 개체인식기-특징추출기(Overfeat: Object Recognizer, Feature Extractor) 와 한장면여러상자검출(SSD: Single Shot MultiBox Detector) 처럼 우리는 전부-나선 모델을 사용한다, 하지만 우리는 여전히 전체 이미지를 수련한다, 어려운음성(hard negative)이 아닌. Fast R-CNN 처럼 우리는 너비와 높이를 철저히 예측하는 대신 테두리상자에서 걸순(뛰어난순서)을 조정한다. 하지만, 우리는 여전히 x 와 y 좌표를 직접적으로 예측한다. 전체 내용은 우리 [논문](https://arxiv.org/abs/1612.08242)에 있다.!

### 3) 이미수련된 모델을 사용하여 검출
이 게시물은 이미수련된 모델을 사용한 욜로시스템으로 개체를 검출하는 방법을 안내한다. 만약 아직 다크넷이 설치되지 않았다면, 먼저 설치해야 한다. 아니면 전부 읽는 대신에 그냥 [실행해라](#그냥-실행):
```bash
git clone https://github.com/pjreddie/darknet
cd darknet
make
```

쉽다!

당신은 cfg/ 하위디렉토리에 욜로에 대한 설정파일을 이미 가지고 있다. 당신은 이미수련된 가중값파일을 여기에 내려받아야 한다(258 MB). 아니면 그냥 실행해라:
```bash
wget https://pjreddie.com/media/files/yolo.weights
```

그런다음 검출기를 실행하라!
```bash
./darknet detect cfg/yolo.cfg yolo.weights data/dog.jpg
```

당신은 이것과 비슷한 몇개의 출력을 볼 것이다.
```bash
layer     filters    size              input                output
    0 conv     32  3 x 3 / 1   416 x 416 x   3   ->   416 x 416 x  32
    1 max          2 x 2 / 2   416 x 416 x  32   ->   208 x 208 x  32
    .......
   29 conv    425  1 x 1 / 1    13 x  13 x1024   ->    13 x  13 x 425
   30 detection
Loading weights from yolo.weights...Done!
data/dog.jpg: Predicted in 0.016287 seconds.
car: 54%
bicycle: 51%
dog: 56%
```
<p align="center"><img width="100%" src="images/Screen_Shot_2016-11-17_at_11_14_54_AM.png" /></p>  

다크넷은 출력한다 검출된 개체, 신뢰도, 그리고 찾는데 걸린 시간. 우리는 **OpenCV** 로 컴파일하지 않았다 그래서 검출을 직접 표시할 수 없다. 대신에, 예측을 **predictions.png** 로 저장한다. 당신은 검출된 개체를 보기 위하여 그 파일을 열 수 있다. 우리는 CPU에서 다크넷을 사용하기 때문에 이미지당 6-12초 걸린다. 만약 GPU 버전을 사용한다면 훨씬 더 빠를 것이다.

나는 당신이 시도하는 경우에 필요하다는 생각이 들어 몇 가지 예시 이미지를 포함했다. **data/eagle.jpg**, **data/dog.jpg**, **data/person.jpg**, or **data/horses.jpg** 를 시도해라!

**검출(detect)** 명령은 명령의 일반 버전을 더 줄인것에 대한 줄임말이다. 이것은 다음 명령과 동일하다:
```bash
./darknet detector test cfg/coco.data cfg/yolo.cfg yolo.weights data/dog.jpg
```

하나의 이미지에서 검출을 실행하려는 경우 이것을 알 필요는 없다 하지만 웹캠에서 실행되는 것과 같은 다른 것을 하고 싶다면 아는것이 유용하다([나중에](https://pjreddie.com/darknet/yolo/#demo) 보게 될 것이다).

### 4) 다중 이미지(Multiple Images)
명령줄에 이미지를 제공하는 대신에, 한번에 여러개의 이미지를 시도해 볼 수 있다. 대신에 설정과 가중값 탑재가 완료되면 당신은 프롬프트를 볼 수 있다:
```bash
./darknet detect cfg/yolo.cfg yolo.weights
layer     filters    size              input                output
    0 conv     32  3 x 3 / 1   416 x 416 x   3   ->   416 x 416 x  32
    1 max          2 x 2 / 2   416 x 416 x  32   ->   208 x 208 x  32
    .......
   29 conv    425  1 x 1 / 1    13 x  13 x1024   ->    13 x  13 x 425
   30 detection
Loading weights from yolo.weights ...Done!
Enter Image Path:
```

data/horses.jpg 처럼 가지고 있는 이미지 경로를 입력하여 이미지에 대한 상자를 예측한다.
<p align="center"><img width="100%" src="images/Screen_Shot_2016-11-17_at_12_26_06_PM.png" /></p>  

일단 완료되면 다른 이미지를 시도하기 위하여 다른 경로를 물어볼 것이다. 끝나면 Ctrl-C 를 사용하여 프로그램을 종료한다.

### 5) 검출 기준값 변경(Changing The Detection Threshold)
By default, YOLO only displays objects detected with a confidence of .25 or higher. You can change this by passing the -thresh <val> flag to the yolo command. For example, to display all detection you can set the threshold to 0:
```bash
./darknet detect cfg/yolo.cfg yolo.weights data/dog.jpg -thresh 0
```

Which produces:
<p align="center"><img width="100%" src="images/Screen_Shot_2016-11-17_at_12_03_22_PM.png" /></p>  

So that's obviously not super useful but you can set it to different values to control what gets thresholded by the model.

### 6) 꼬맹이 욜로(Tiny YOLO)
Tiny YOLO is based off of the Darknet reference network and is much faster but less accurate than the normal YOLO model. To use the version trained on VOC:
```bash
wget https://pjreddie.com/media/files/tiny-yolo-voc.weights
./darknet detector test cfg/voc.data cfg/tiny-yolo-voc.cfg tiny-yolo-voc.weights data/dog.jpg
```

Which, ok, it's not perfect, but boy it sure is fast. On GPU it runs at >200 FPS.
<p align="center"><img width="100%" src="images/Screen_Shot_2016-11-26_at_11_22_46_PM.png" /></p>  

### 7) 웹캠으로 실시간 검출(Real-Time Detection on a Webcam)
Running YOLO on test data isn't very interesting if you can't see the result. Instead of running it on a bunch of images let's run it on the input from a webcam!

To run this demo you will need to compile Darknet with CUDA and OpenCV. Then run the command:
```bash
./darknet detector demo cfg/coco.data cfg/yolo.cfg yolo.weights
```

YOLO will display the current FPS and predicted classes as well as the image with bounding boxes drawn on top of it.

You will need a webcam connected to the computer that OpenCV can connect to or it won't work. If you have multiple webcams connected and want to select which one to use you can pass the flag -c <num> to pick (OpenCV uses webcam 0 by default).

You can also run it on a video file if OpenCV can read the video:
```bash
./darknet detector demo cfg/coco.data cfg/yolo.cfg yolo.weights <video file>
```

That's how we made the YouTube video above.

### 8) VOC로 욜로 수련(Training YOLO on VOC)
You can train YOLO from scratch if you want to play with different training regimes, hyper-parameters, or datasets. Here's how to get it working on the Pascal VOC dataset.

#### 8-1) Get The Pascal VOC Data
To train YOLO you will need all of the VOC data from 2007 to 2012. You can find links to the data here. To get all the data, make a directory to store it all and from that directory run:
```bash
wget https://pjreddie.com/media/files/VOCtrainval_11-May-2012.tar
wget https://pjreddie.com/media/files/VOCtrainval_06-Nov-2007.tar
wget https://pjreddie.com/media/files/VOCtest_06-Nov-2007.tar
tar xf VOCtrainval_11-May-2012.tar
tar xf VOCtrainval_06-Nov-2007.tar
tar xf VOCtest_06-Nov-2007.tar
```

There will now be a VOCdevkit/ subdirectory with all the VOC training data in it. 

#### 8-2) Generate Labels for VOC
Now we need to generate the label files that Darknet uses. Darknet wants a .txt file for each image with a line for each ground truth object in the image that looks like:
```bash
<object-class> <x> <y> <width> <height>
```

Where x, y, width, and height are relative to the image's width and height. To generate these file we will run the voc_label.py script in Darknet's scripts/ directory. Let's just download it again because we are lazy.
```bash
wget https://pjreddie.com/media/files/voc_label.py
python voc_label.py
```

After a few minutes, this script will generate all of the requisite files. Mostly it generates a lot of label files in VOCdevkit/VOC2007/labels/ and VOCdevkit/VOC2012/labels/. In your directory you should see:
```bash
ls
2007_test.txt   VOCdevkit
2007_train.txt  voc_label.py
2007_val.txt    VOCtest_06-Nov-2007.tar
2012_train.txt  VOCtrainval_06-Nov-2007.tar
2012_val.txt    VOCtrainval_11-May-2012.tar
```

The text files like 2007_train.txt list the image files for that year and image set. Darknet needs one text file with all of the images you want to train on. In this example, let's train with everything except the 2007 test set so that we can test our model. Run:
```bash
cat 2007_train.txt 2007_val.txt 2012_*.txt > train.txt
```

Now we have all the 2007 trainval and the 2012 trainval set in one big list. That's all we have to do for data setup!

#### 8-3) Modify Cfg for Pascal Data
Now go to your Darknet directory. We have to change the cfg/voc.data config file to point to your data:
```bash
  1 classes= 20
  2 train  = <path-to-voc>/train.txt
  3 valid  = <path-to-voc>2007_test.txt
  4 names = data/voc.names
  5 backup = backup
```

You should replace <path-to-voc> with the directory where you put the VOC data.

#### 8-4) Download Pretrained Convolutional Weights
For training we use convolutional weights that are pre-trained on Imagenet. We use weights from the Extraction model. You can just download the weights for the convolutional layers here (76 MB).
```bash
wget https://pjreddie.com/media/files/darknet19_448.conv.23
```

If you want to generate the pre-trained weights yourself, download the pretrained Darknet19 448x448 model and run the following command:
```bash
./darknet partial cfg/darknet19_448.cfg darknet19_448.weights darknet19_448.conv.23 23
```

But if you just download the weights file it's way easier.

#### 8-5) Train The Model
Now we can train! Run the command:
```bash
./darknet detector train cfg/voc.data cfg/yolo-voc.cfg darknet19_448.conv.23
```

### 9) Training YOLO on COCO
You can train YOLO from scratch if you want to play with different training regimes, hyper-parameters, or datasets. Here's how to get it working on the COCO dataset.

#### 9-1) Get The COCO Data
To train YOLO you will need all of the COCO data and labels. The script scripts/get_coco_dataset.sh will do this for you. Figure out where you want to put the COCO data and download it, for example:
```bash
cp scripts/get_coco_dataset.sh data
cd data
bash get_coco_dataset.sh
```

Now you should have all the data and the labels generated for Darknet.

#### 9-2) Modify cfg for COCO
Now go to your Darknet directory. We have to change the cfg/coco.data config file to point to your data:
```bash
  1 classes= 80
  2 train  = <path-to-coco>/trainvalno5k.txt
  3 valid  = <path-to-coco>/5k.txt
  4 names = data/coco.names
  5 backup = backup
```

You should replace <path-to-coco> with the directory where you put the COCO data.

You should also modify your model cfg for training instead of testing. cfg/yolo.cfg should look like this:
```bash
[net]
# Testing
# batch=1
# subdivisions=1
# Training
batch=64
subdivisions=8
....
```

####9-3) Train The Model
Now we can train! Run the command:
```bash
./darknet detector train cfg/coco.data cfg/yolo.cfg darknet19_448.conv.23
```

If you want to use multiple gpus run:
```bash
./darknet detector train cfg/coco.data cfg/yolo.cfg darknet19_448.conv.23 -gpus 0,1,2,3
```

If you want to stop and restart training from a checkpoint:
```bash
./darknet detector train cfg/coco.data cfg/yolo.cfg backup/yolo.backup -gpus 0,1,2,3
```

### 10) What Happened to the Old YOLO Site?

If you are using YOLO version 1 you can still find the site here: https://pjreddie.com/darknet/yolov1/

### 11) Cite

If you use YOLOv2 in your work please cite our paper!
```bash
@article{redmon2016yolo9000,
  title={YOLO9000: Better, Faster, Stronger},
  author={Redmon, Joseph and Farhadi, Ali},
  journal={arXiv preprint arXiv:1612.08242},
  year={2016}
}
```

---



