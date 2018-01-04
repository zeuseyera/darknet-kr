:kr: 다크넷(darknet): C로 작성한 신경망 공개소스  
출처:
- https://github.com/pjreddie/darknet
- https://pjreddie.com/darknet
---
---
# 다크넷(darknet): C로 작성한 신경망 공개소스
다크넷은 C와 쿠다로 작성한 공개소스 신경망 작업틀이다. 이것은 빠르고, 설치가 쉽다, 그리고 CPU 와 GPU 계산을 지원한다. 

## [1. 다크넷 설치(Installing Darknet)](#다크넷-설치)
다크넷은 설치와 실행이 쉽다. 이 게시는 이것을 통해 안내한다.

## [2. 욜로: 실시간 개체 검출(YOLO: Real-Time Object Detection)](#욜로)
욜로는(YOLO, 너는 오직 한번만 본다) 최첨단 기술이다, 실시간 개체 검출 시스템.

## [3. 이미지넷 분류(ImageNet Classification)](#이미지넷-분류)
알렉스넷과 VGG-16과 같은 인기있는 모델로 이미지를 분류한다.

## [4. 악몽(Nightmare)](#악몽)
유령, 악귀(ghouls), 그리고 기괴한 야생 오소리(badgermoles)를 만들어내는 마술에 다크넷의 숨겨진 마법을 사용한다. 하지만, 경고한다, 여기에 들어간 자들에게: 악몽의 땅에서 아무도 안전하지 않다.

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
  year = {2013--2016}}
```

## 11. 연락(Contact)
다크넷에 관한 질문이나 도움을 받으려면 [다크넷 메일목록](https://groups.google.com/forum/#!forum/darknet)에 연락하시오. 가능한 한 빨리 질문에 답변할 것이다.

---
---
<a name="다크넷-설치"></a>
## 1. 다크넷 설치
Darknet is easy to install with only two optional dependancies:
- OpenCV if you want a wider variety of supported image types.
- CUDA if you want GPU computation.Both are optional so lets start by just installing the base system. I've only tested this on Linux and Mac computers. If it doesn't work for you, email me or something?
### 1) Installing The Base System
First clone the Darknet git repository here. This can be accomplished by:
> ```bash
> git clone https://github.com/pjreddie/darknet.git
> cd darknet> Make
> ```
If this works you should see a whole bunch of compiling information fly by:
```bash
mkdir -p obj
gcc -I/usr/local/cuda/include/  -Wall -Wfatal-errors  -Ofast....
gcc -I/usr/local/cuda/include/  -Wall -Wfatal-errors  -Ofast....
gcc -I/usr/local/cuda/include/  -Wall -Wfatal-errors  -Ofast....
.....
gcc -I/usr/local/cuda/include/  -Wall -Wfatal-errors  -Ofast -lm....
```
If you have any errors, try to fix them? If everything seems to have compiled correctly, try running it!
```bash
./darknet
```
You should get the output:
```bash
usage: ./darknet <function>
```
Great! Now check out the cool things you can do with darknet here.

### 2) Compiling With CUDA
Darknet on the CPU is fast but it's like 500 times faster on GPU! You'll have to have an Nvidia GPU and you'll have to install CUDA. I won't go into CUDA installation in detail because it is terrifying.  
Once you have CUDA installed, change the first line of the Makefile in the base directory to read:  
GPU=1  
Now you can make the project and CUDA will be enabled. By default it will run the network on the 0th graphics card in your system (if you installed CUDA correctly you can list your graphics cards using nvidia-smi). If you want to change what card Darknet uses you can give it the optional command line flag -i <index>, like:  
./darknet -i 1 imagenet test cfg/alexnet.cfg alexnet.weights  
If you compiled using CUDA but want to do CPU computation for whatever reason you can use -nogpu to use the CPU instead:  
./darknet -nogpu imagenet test cfg/alexnet.cfg alexnet.weights  
Enjoy your new, super fast neural networks!  
  
### 3) Compiling With OpenCV
By default, Darknet uses stb_image.h for image loading. If you want more support for weird formats (like CMYK jpegs, thanks Obama) you can use OpenCV instead! OpenCV also allows you to view images and detections without having to save them to disk.  

First install OpenCV. If you do this from source it will be long and complex so try to get a package manager to do it for you.  

Next, change the 2nd line of the Makefile to read:  

OPENCV=1  
You're done! To try it out, first re-make the project. Then use the imtest routine to test image loading and displaying:  

./darknet imtest data/eagle.jpg  

If you get a bunch of windows with eagles in them you've succeeded! They may look like:


