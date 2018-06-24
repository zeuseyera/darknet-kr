
:kr: 다크넷(darknet): C로 작성한 신경망 공개소스 

출처: https://pjreddie.com/darknet

| [다크넷](../README.md) | [설치](../1_SeolChi/SeolChi.md) | [욜로](../2_YOLO/yolo.md) | [이미지넷분류](../3_ImageNet_BunRyu/BunRyu.md) | [악몽](../4_AkMong/AkMong.md) | [재사용신경망](../5_RNN/rnn.md) | [다크고](../6_DarkGo/DarkGo.md) | [꼬맹이망](../7_GgoMaengIi/GgoMaengIi.md) | [분류기수련](../8_SuRyeon/SuRyeon.md) |  
| --- | --- | --- | --- | --- | --- | --- | --- | --- |  

<a name="꼬맹이-다크넷"></a>
## 7. 꼬맹이 다크넷(Tiny Darknet)

 나는 많은 사람들이 [스퀴즈넷(SqueezeNet)](https://arxiv.org/abs/1602.07360)에 대해 이야기하는 것을 들었다.

 스퀴즈넷(SqueezeNet)은 훌륭하다 하지만 이것은 단지 참여(parameter) 개수를 최적화한 것이다. 대부분 고품질 이지지가 10MB 또는 이상일 때 우리가 왜 신경써야 하나 만약 우리의 모형이 5MB 또는 50MB 라면? 만약 우리가 정말 빠른 작은 모형을 원한다면, [:kr:다크넷 기준망(Darknet reference network)](../3_ImageNet_BunRyu/BunRyu.md#기준망)[(영문)](https://pjreddie.com/darknet/imagenet/#reference)이 왜 안되는지 확인해보라? 이것은 28MB에 불과하다 하지만 더 중요한 것은, 이것은 단지 8억 부동소수점 연산을 한다. 원래 [알렉스넷(Alexnet)](https://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks.pdf)은 23억이다. 다크넷은 2.9배 빠르다 그리고 작고 4% 더 정확하다. 그러면 스퀴즈넷(SqueezeNet)은 어떤가? 물론 가중값은 4.8MB에 불과하다 하지만 순방향 전달은 여전히 22억 연산이다. 알렉스넷(Alexnet)은 분류에서 훌륭하게 첫번째로 통과했다 하지만 오늘날 우리의 망은 뒤로 물러섰다 이것의 나쁜점은 너무 느리다! 그러나 어찌됐는, 사람들은 스퀴즈넷(SqueezeNet)에 대단한 관심이 있다 그래서 당신이 정말로 작은망을 고집하면, 이것을 사용하라:

### 1) 꼬맹이 다크넷(Tiny Darknet)


| 모형                          | Top-1 | Top-5 | 연산(Ops) | 크기 |  
| ---                          | ---   | ---   | ---:     | ---:  |  
| 알렉스넷(AlexNet)             | 57.0  | 80.3  | 2.27 Bn | 238 MB |   
| 다크넷 기준(Darknet Reference) | 61.1  | 83.0 | 0.81 Bn | 28 MB |  
| 스퀴즈넷(SqueezeNet)          | 57.5  | 80.3  | 2.17 Bn | 4.8 MB |  
| 꼬맹이 다크넷(Tiny Darknet)    | 58.7  | 81.7  | 0.98 Bn | 4.0 MB |  

 여기에서 진정한 승자는 분명히 다크넷 기준망이다 하지만 만약 당신이 작은 모형을 원한다고 고집하면, 꼬맹이 다크넷을 사용하라. 아니면 당신 자신의것을 수련하라, 이것은 쉽게 할수 있다!

 여기에 다크넷에서 이것을 사용하는 방법이 있다(그리고 또한 다크넷을 설치하는 방법):

```
git clone https://github.com/pjreddie/darknet
cd darknet
make
wget https://pjreddie.com/media/files/tiny.weights
./darknet classify cfg/tiny.cfg tiny.weights data/dog.jpg
```

 희망스럽게 다음과 같은 것을 볼수 있다:

```
data/dog.jpg: Predicted in 0.160994 seconds.
malamute: 0.167168
Eskimo dog: 0.065828
dogsled: 0.063020
standard schnauzer: 0.051153
Siberian husky: 0.037506
```

 여기는 설정파일이 있다: [tiny.cfg](https://github.com/pjreddie/darknet/blob/master/cfg/tiny.cfg)

 모형은 단지 수많은 3x3 과 1x1 나선층이다:

```
layer     filters    size              input                output
    0 conv     16  3 x 3 / 1   224 x 224 x   3   ->   224 x 224 x  16
    1 max          2 x 2 / 2   224 x 224 x  16   ->   112 x 112 x  16
    2 conv     32  3 x 3 / 1   112 x 112 x  16   ->   112 x 112 x  32
    3 max          2 x 2 / 2   112 x 112 x  32   ->    56 x  56 x  32
    4 conv     16  1 x 1 / 1    56 x  56 x  32   ->    56 x  56 x  16
    5 conv    128  3 x 3 / 1    56 x  56 x  16   ->    56 x  56 x 128
    6 conv     16  1 x 1 / 1    56 x  56 x 128   ->    56 x  56 x  16
    7 conv    128  3 x 3 / 1    56 x  56 x  16   ->    56 x  56 x 128
    8 max          2 x 2 / 2    56 x  56 x 128   ->    28 x  28 x 128
    9 conv     32  1 x 1 / 1    28 x  28 x 128   ->    28 x  28 x  32
   10 conv    256  3 x 3 / 1    28 x  28 x  32   ->    28 x  28 x 256
   11 conv     32  1 x 1 / 1    28 x  28 x 256   ->    28 x  28 x  32
   12 conv    256  3 x 3 / 1    28 x  28 x  32   ->    28 x  28 x 256
   13 max          2 x 2 / 2    28 x  28 x 256   ->    14 x  14 x 256
   14 conv     64  1 x 1 / 1    14 x  14 x 256   ->    14 x  14 x  64
   15 conv    512  3 x 3 / 1    14 x  14 x  64   ->    14 x  14 x 512
   16 conv     64  1 x 1 / 1    14 x  14 x 512   ->    14 x  14 x  64
   17 conv    512  3 x 3 / 1    14 x  14 x  64   ->    14 x  14 x 512
   18 conv    128  1 x 1 / 1    14 x  14 x 512   ->    14 x  14 x 128
   19 conv   1000  1 x 1 / 1    14 x  14 x 128   ->    14 x  14 x1000
   20 avg                       14 x  14 x1000   ->  1000
   21 softmax                                        1000
   22 cost                                           1000
```

---
