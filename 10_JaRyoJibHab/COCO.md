:kr: 상황 공통개체 자료

출처: http://cocodataset.org/#download

| 도구 						| 이미지							| 뜻풀이 |  
| ---						| ---								| --- |  
| [COCO API](Annotations)	| [2014 벼림 이미지(83K/13GB)](http://images.cocodataset.org/zips/train2014.zip)			| [2014 벼림/검증 뜻풀이(241MB)](http://images.cocodataset.org/annotations/annotations_trainval2014.zip)				|  
|							| [2014 검증 이미지(41K/6GB)](http://images.cocodataset.org/zips/val2014.zip)				| [2014 평가이미지 정보(1MB)](http://images.cocodataset.org/annotations/image_info_test2014.zip)						|  
|							| [2014 평가 이미지(41K/6GB)](http://images.cocodataset.org/zips/test2014.zip)				| [2015 평가이미지 정보(2MB)](http://images.cocodataset.org/annotations/image_info_test2015.zip)						|  
|							| [2015 평가 이미지(81K/12GB)](http://images.cocodataset.org/zips/test2015.zip)				| [2017 벼림/검증 뜻풀이(241MB)](http://images.cocodataset.org/annotations/annotations_trainval2017.zip)				|  
|							| [2017 벼림 이미지(118K/18GB)](http://images.cocodataset.org/zips/train2017.zip)			| [2017 소박이 벼림/검증 뜻풀이(1.1GB)](http://images.cocodataset.org/annotations/stuff_annotations_trainval2017.zip)	|  
|							| [2017 검증 이미지(5K/1GB)](http://images.cocodataset.org/zips/val2017.zip)				| [2017 다봄 벼림/검증 뜻풀이(821MB)](http://images.cocodataset.org/annotations/panoptic_annotations_trainval2017.zip)	|  
|							| [2017 평가 이미지(41K/6GB)](http://images.cocodataset.org/zips/test2017.zip)				| [2017 평가이미지 정보(1MB)](http://images.cocodataset.org/annotations/image_info_test2017.zip)						|  
|							| [2017 꼬리표없는 이미지(123K/19GB)](http://images.cocodataset.org/zips/unlabeled2017.zip)	| [2017 꼬리표없는 이미지 정보(4MB)](http://images.cocodataset.org/annotations/image_info_unlabeled2017.zip)			|  

## 1. 개요

 나눠진 어떤 자료집합을 내려받아야 하나? 각 연도의 이미지는 다른작업이 조합되었다. 구체적으로:  

|  |  |  
| ---	| --- |  
| 2014 벼림/검증		| [검출 2015](http://cocodataset.org/#detection-2015), [자막 2015](http://cocodataset.org/#captions-2015), [검출 2016](http://cocodataset.org/#detection-2016), [중요뜻 2016](http://cocodataset.org/#keypoints-2016)	|  
| 2014 평가				| [자막 2015](http://cocodataset.org/#captions-2015)	|  
| 2015 평가				| [검출 2015](http://cocodataset.org/#detection-2015), [검출 2016](http://cocodataset.org/#detection-2016), [중요뜻 2016](http://cocodataset.org/#keypoints-2016)	|  
| 2017 벼림/검증/평가	| [검출 2017](http://cocodataset.org/#detection-2017), [중요뜻 2017](http://cocodataset.org/#keypoints-2017), [소박이 2017](http://cocodataset.org/#stuff-2017),	|  
|						| [검출 2018](http://cocodataset.org/#detection-2018), [중요뜻 2018](http://cocodataset.org/#keypoints-2018), [소박이 2018](http://cocodataset.org/#stuff-2018), [다봄 2018](http://cocodataset.org/#panoptic-2018)	|   
| 2017 꼬리표없음		| 모든 경쟁에 대한 선택적 자료	|  

```
  만약 2017 또는 2018 작업으로 제출하는 경우 2017 이미지만 내려받아야 한다. 이전 분할은 무시할 수 있다.
  알림: 연도 분할은 이미지를 분할하여 배포된 연도를 나타낸다, 뜻풀이가 배포된 연도가 아니다.
```

 이미지를 효율적으로 내려받으려면, 큰 zip 파일 내려받기를 방지하기 위해 gsutil rsync 사용을 권고한다. 내려받은 COCO 자료를 설치하기 위하여 [COCO API 나를봐(Readme)](https://github.com/cocodataset/cocoapi)의 지침을 따른다(이미지와 뜻풀이는 "coco/images/" 와 "coco/annotations/" 안에 있어야 한다). 이 자료집합을 내려받으면, 당신은 우리의 [사용조건](http://cocodataset.org/#termsofuse)에 동의한 것이다.

```
우리의 자료는 구글 클라우드 플랫폼(GCP)에서 관리한다. gsutil은 이 자료를 효율적으로 접근하기위한 도구를 제공한다.
gsutil을 사용하기위한 자신의 GCP 계정이 필요하지 않다. 자료를 내려받기위한 지침은 다음과 같다:

  (1) 다음을 통해 gsutil을 설치한다: curl https://sdk.cloud.google.com | bash
  (2) 자신의 디렉토리를 만든다:      mkdir val2017
  (3) 다음을 통해 동기르 맞춘다:     gsutil -m rsync gs://images.cocodataset.org/val2017 val2017

rsync를 통해 내려받기 할수 있는 분할은 다음과 같다:
  train2014, val2014, test2014, test2015, train2017, val2017, test2017, unlabeled2017.

'val2017'을 내려받기 원하는 분할로 간단히 대체한다 그리고 (2)~(3) 단계를 반복한다.
끝으로, 다음을 통해 모든 뜻풀이 zip 파일을 내려받을수 있다:

  (4) 뜻풀이 가져오기: gsutil -m rsync gs://images.cocodataset.org/annotations [localdir]

내려받기는 다중쓰레드이며, 게다가 내려받기의 다른 선택사항도 제어할 수 있다.
([gsutil rsync](https://cloud.google.com/storage/docs/gsutil/commands/rsync)를 보라)
gsutil 설치 도움은 우리에게 연락하지 마라.
(우리는 당신이 gcloud init를 실행할 필요가 없다는것만 알린다)
```

 2018 갱신: 검출과 중요뜻 자료는 변경안됨. 2018에서 새로운 것, 모든 2017 이미지에 대해 완전한 소박이(stuff)와 다봄(panoptic) 뜻풀이가 가능하다. *알림: 만약 2018.06.17 이전에 소박(stuff)이 뜻풀이(annotations)를 내려받았다면, 다시 내려받아라.*

 2017 갱신: 2017에서 주된 변경은 벼림/검증을 83K/41K 분할 대신에, 공통집단(community)의 반응을 기반으로 분할한 것은 이제 벼림/검증에 대해 118K/5K 이다. 완전히 동일한 이미지가 사용된다, 그리고 검출/중요뜻 에 대한 새로운 뜻풀이가 없이 제공된다. 하지만 2017에서 새로운것은 벼림이미지 40K 와 검증이미지 5K 의 소박이 뜻풀이다. 또한, 평가를 위해, 2017 안에 평가집합은 두개의 분할만 가진다(개발 / 도전, dev / challenge), 이전 연도에 사용된 4개의 분할(개발 / 표준 / 예약 / 도전, dev / standard / reserve / challenge) 대신에. 끝으로, 2017에서 새로운것은 COCO에서 120K의 꼬리표없는 이미지를 배포한 것이다 COCO는 꼬리표있는 이미지와 동일한 분류 분포를 따른다; 이것은 COCO에서 부분-지도(半-指導, semi-supervised)학습에 대해 유용할 것이다.

## 2. 상황공통개체 응용프로그램연동(COCO API)

 COCO API는 COCO에서 탑재, 분석, 그리고 뜻풀이 시각화를 거든다. API는 다중 뜻풀이 형식을 지원한다([자료형식](http://cocodataset.org/#format-data) 페이지를 보라). 추가적인 상세설명을 보기위해: 매트랩(Matlab), 파이썬(Python), 그리고 루아(Lua)코드 각각에 대해 [CocoApi.m](https://github.com/cocodataset/cocoapi/blob/master/MatlabAPI/CocoApi.m), [coco.py](https://github.com/cocodataset/cocoapi/blob/master/PythonAPI/pycocotools/coco.py), 그리고 [CocoApi.lua](https://github.com/cocodataset/cocoapi/blob/master/LuaAPI/CocoApi.lua), 그리고 또한 [파이썬 API 실증](https://github.com/cocodataset/cocoapi/blob/master/PythonAPI/pycocoDemo.ipynb).

```
API 전체에서 "ann"=annotation, "cat"=category, 그리고 "img"=image.

  getAnnIds    주어진 필터조건을 만족하는 뜻풀이 고유번호를 가져온다.
  getCatIds    주어진 필터조건을 만족하는 범주의 고유번호를 가져온다.
  getImgIds    주어진 필터조건을 만족하는 이미지 고유번호를 가져온다.
  loadAnns     지정한 고유번호로 뜻풀이를 탑재한다.
  loadCats     지정한 고유번호로 범주를 탑재한다.
  loadImgs     지정한 고유번호로 이미지를 탑재한다.
  loadRes      알고리즘 결과를 탑재하고 이것에 접근하기위한 API를 생성한다.
  showAnns     지정한 뜻풀이를 표시한다.
```

## 3. 가리개 응용프로그램잇대기(MASK API)

 COCO는 모든 개체근본(object instance)에 대한 분리가리개를 제공한다. 이것은 두가지 도전을 불러일으킨다: 가리개를 작게 저장하고 가리개 계산을 효율적으로 수행을 위한. 우리는 맞춤 실행길이부호(Run Length Encoding, RLE)제도를 사용하여 두가지 도전을 해결한다. 실행길이부호(RLE) 표현의 크기는 가리개 경계화소의 수에 비례한다 그리고 영역, 결합, 또는 교차같은 연산은 실행길이부호(RLE)에서 직접 효율적으로 계산할 수 있다. 구체적으로, 상당히 단순한 모양을 가정한다, 실행길이부호(RLE) 표현은 O(√n) 이고 여기에서 n은 개체에서 화소의 수이다, 그리고 공통계산은 마찬가지로 O(√n) 이다. 풀린가리개(배열로 저장된)로 동일한 연산을 순수하게 계산하면 O(n)이 될 것이다.

 가리개 API는 실행길이부호(RLE) 형식으로 저장된 가리개를 조작하기위한 잇대기를 제공한다. API는 아래에 정의되어 있다, 추가적인 상세설명을 보기위해: [MaskApi.m](https://github.com/cocodataset/cocoapi/blob/master/MatlabAPI/MaskApi.m), [mask.py](https://github.com/cocodataset/cocoapi/blob/master/PythonAPI/pycocotools/mask.py), 또는 [MaskApi.lua](https://github.com/cocodataset/cocoapi/blob/master/LuaAPI/MaskApi.lua). 끝으로, 우리는 참가리개바탕 대다수는 다각형으로 저장된다는 것을 알린다(이것은 상당히 작다), 이러한 다각형은 필요한 경우 실행길이부호(RLE)로 변환된다.

```
encode    실행길이부호(RLE)를 사용하여 이진가리개 부호한다.
decode    실행길이부호(RLE)를 통해 이진가리개 부호를 푼다.
merge     가리개부호의 결합 또는 교차를 계산한다
iou       가리개사이의 교차 겹침 결합을 계산한다.
area      가리개부호의 영역을 계산한다.
toBbox    가리개부호를 둘러싼 경계상자를 가져온다.
frBbox    경계상자를 가리개부호로 변환한다.
frPoly    다각형을 가리개부호로 변환한다.
```

---
