
:kr: 다크넷(darknet): C로 작성한 신경망 공개소스 

출처: https://pjreddie.com/darknet

| [다크넷](../README.md) | [설치](../1_SeolChi/SeolChi.md) | [욜로](../2_YOLO/yolo.md) | [이미지넷분류](../3_ImageNet_BunRyu/BunRyu.md) | [악몽](../4_AkMong/AkMong.md) | [재사용신경망](../5_RNN/rnn.md) | [다크고](../6_DarkGo/DarkGo.md) | [꼬맹이망](../7_GgoMaengIi/GgoMaengIi.md) | [분류기수련](../8_SuRyeon/SuRyeon.md) |  
| --- | --- | --- | --- | --- | --- | --- | --- | --- |  

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

이제 과제를 **만들 수 있다** 그리고 쿠다는 활성화 된다. 기본적으로 시스템에서 0번째 그래픽카드로 망이 실행한다(쿠다를 올바르게 설치했다면 **nvidia-smi(Nvidia-System Management Interface)** 를 사용하여 그래픽카드를 나열할 수 있다). 다크넷이 사용하는 카드를 바꾸고 싶다면 선택적 명령줄에 **-i <고유번호>** 표시정보를 줄 수 있다, 다음처럼:  
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
