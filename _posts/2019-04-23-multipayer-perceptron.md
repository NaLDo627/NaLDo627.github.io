---
layout: post
title:  "다층 퍼셉트론 실습"
subtitle:  "인공지능"
date:   2019-04-23 00:46:00 +0900
author:     "날도"
header-img: "img/post-bg-2015.jpg"
mathjax: true
catalog: true
tags: 
    - 인공지능
    - C/C++
    - MFC
    - 머신러닝
    - 딥러닝
    - 과제
    - 실패
---

인공지능 실습 과제로 다층 퍼셉트론 구현에 대해 하게 되었다.

## 퍼셉트론(Perceptron) 이란?

![(신경망 이미지)](/img/in-post/post-multipayer-perceptron/1.jpg)

퍼셉트론이란 인공 신경망 모형의 하나로, 1957년 Rosenblatt가 단순한 패턴을 인식하기 위해 제안한 모델이다. <br>
퍼셉트론은 다수의 Input을 받은 후 하나의 Output을 출력한다. 이는 뉴런이 전기신호를 내보내 정보를 전달하는 것과 비슷해 보인다. 실제 신경계에서 뉴런의 수상돌기나 축색돌기처럼 신호를 전달하는 역할을 퍼셉트론에서는 weight가 그 역할을 한다. 각 Input값과 weight값의 계산값의 총합을 그 신경망의 Activation함수에 입력하였을 때 임계값을 넘긴다면 1, 아니라면 0 혹은 -1을 출력한다.<br>
퍼셉트론에게 학습을 시키기 위해 지도값을 준 후 학습시키는 **교사학습** 을 시행하게 되는데, 이 학습 과정에서 weight값이 수정된다. 즉 학습이라는 것은 **weight값을 조정하는 것** 을 말한다.

## 다층 퍼셉트론(Multipayer Peceptron)이란?

![(선형분류)](/img/in-post/post-multipayer-perceptron/2.png)

퍼셉트론은 선형 분류이다. 선형 분류란 위 그림과 같이 강아지와 고양이의 구분을 선 하나로 그어 분류하는 것이다. 퍼셉트론 알고리즘은 학습을 통해 두 패턴을 분류하는 선, 즉 가중치를 조정하는 작업을 말한다.

![(XOR)](/img/in-post/post-multipayer-perceptron/3.gif)

여기서 선형 분류의 한계점이 나타난다. 위와 같은 XOR 문제에서 선 하나로 패턴을 분류할 수가 없다는 것이다. 실제로 이와 같은 문제점 때문에 1970년대 안팎에서 인공지능의 침체기가 일어났다.<br><br>
그러나 인공지능의 침체기 중에서도, 묵묵히 인공신경망의 힘을 믿고 꾸준히 연구하는 사람들이 있었다. McClelland, David 그리고 Geoffrey가  집필한 "병렬 분할 처리"라는 책을 통해 **다층 퍼셉트론** 의 개념이 나오게 되었다. 기존의 퍼셉트론이 선 하나로 해결할 수 없는 문제가 있다면, 중간에 은닉층을 더 추가함으로써, 아래와 같이 선을 추가로 긋는 효과를 얻음으로 XOR 문제를 해결할 수가 있게 된 것이다. 

![(XOR해결)](/img/in-post/post-multipayer-perceptron/4.gif)

또한, 다층 퍼셉트론의 활성화 함수(Activate Function)는 시그모이드(Sigmoid)함수를 사용한다.
<center>

$sigmoid(x) = \frac{1}{1+e^{-x}}$

</center>

## 역전파와 학습
본래 퍼셉트론은, 전방향 전파 과정에서 가중치 조정, 즉 학습하였다. 그러나 다층 퍼셉트론은 은닉층이 추가되면서 이 방법이 매우 어려워 졌는데, McClelland, David 그리고 Geoffrey가 Backpropagation, 즉 역전파 알고리즘을 제안하여 해결하였다.<br>

![(역전파)](/img/in-post/post-multipayer-perceptron/15.png)

먼저 초기화 된 가중치를 가지고 학습시킬 패턴을 입력층에 입력한다. 입력된 값은 은닉층에 노드에 대해 각각의 가중치와 곱한 후, 활성화 함수에 의해 Output이 결정된다. 이렇게 결정된 Output을 Input으로, 이번엔 출력층에 방금 전과 같이 각각의 가중치와 곱하여 출력층의 Output을 결정한다. 여기까지가 순전파이다.<br>
역전파 과정은 먼저 출력층에서 학습시길 값과의 오차($\delta$)를 계산 후, 은닉층의 오차값을 계산한다. 구해진 오차값으로, ETA값(Learning rate)값과 output값을 통해 Weight값을 업데이트한다.

## 실습 개요
저번 [홉필드 네트워크 실습](https://naldo627.github.io/2019/04/06/hopfield-network/)때 사용하였던 패턴을 그대로 사용하였다. 당시 실습때에는 비슷한 패턴이 많아 연상이 잘 되지 않았었는데, 이번에는 과연 연상이 잘 될지 기대가 된다. <br>
학습시킬 패턴은 이전과 같이 다음과 같다.

![(패턴 이미지)](/img/in-post/post-multipayer-perceptron/5.png)


## 소스코드 
소스코드는 길이가 상당히 긴 관계로, github 링크를 따로 첨부하겠다.<br>
<https://github.com/NaLDo627/MultipayerPerceptronApp>

## 실습 과정
먼저 저번과 동일하게 아래와 같이 pattern.txt파일로 패턴을 학습시켰다.
```
# 순서대로 가, 내, 댜, 럐, 머, 베, 셔, 예, 조, 쵸, 쿠, 튜, 프, 히
00000000110 11111100110 11111100110 00001100110 00001100111 00001100111 00011100110 11111000110 11100000110 00000000110 00000000110
00000011011 11000011011 11000011011 11000011011 11000011111 11000011111 11000011011 11111011011 11111011011 00000011011 00000011011
00000011000 11111011000 11111011110 11000011110 11000011000 11000011000 11000011110 11111011110 11111011000 00000011000 00000011000
00000011011 11111011011 11111011111 00011011111 11111011011 11111011011 11000011111 11111011111 11111011011 00000011011 00000011011
00000000110 11111000110 11111000110 11011000110 11011011110 11011011110 11011000110 11111000110 11111000110 00000000110 00000000110
00000000101 11001100101 11001100101 11111100101 11111101101 11001101101 11001101101 11111100101 11111100101 00000000101 00000000101
00000000110 00100000110 01110011110 01110011110 11111000110 11111000110 11011011110 11011011110 10001000110 00000000110 00000000110
00000000101 00110000101 01111001101 11111101101 11001100101 11001100101 11111101101 01111001101 00110000101 00000000101 00000000101
00000000000 01111111110 01111111110 00011111000 00111011100 01111011110 11100000111 11001110011 00001110000 11111111111 11111111111
00001110000 01111111110 01111111110 00011111000 00111011100 01111011110 11100000111 11011011011 00011011000 11111111111 11111111111
00000000000 11111111111 11111111111 00000000111 00011111110 00000001110 01111111100 00000000000 11111111111 11111111111 00001110000
00000000000 11111111110 11111111110 11100000000 11111111110 11100000000 11111111110 00000000000 11111111111 11111111111 00011011000
00000000000 01111111110 01111111110 00011011000 00011011000 01111111110 01111111110 00000000000 11111111111 11111111111 00000000000
00110000110 11111110110 01111000110 11111100110 11001100110 11001100110 11111100110 01111000110 00110000110 00000000110 00000000110
```

실행화면은 다음과 같다.


![(실행화면)](/img/in-post/post-multipayer-perceptron/6.png)

최대 EPOCH수는 50000, ETA값과 초기 Weight값은 각각 0.1로 주었다.<br>
먼저, 학습이 제대로 되었는지를 확인하기 위해 **"가"** 글자 하나를 정확하게 입력하였다.

![(입력화면)](/img/in-post/post-multipayer-perceptron/7.png)

어... 패턴의 분류가 되지 않았다. 

![(입력화면2)](/img/in-post/post-multipayer-perceptron/8.png)

다른 패턴을 넣어도 마찬가지이다.. <br>

무엇이 문제일까 이틀을 계속 소스코드를 살펴보고 디버깅을 해보았지만, 알고리즘 문제는 찾을 수 없었다.. 혹시나 저번처럼 패턴 문제일까 싶어서 임시로 실습 PPT에 나온 ㄱ, ㄴ, ㄷ 세 패턴만 학습 시켰다.

![(실습ppt캡쳐)](/img/in-post/post-multipayer-perceptron/9.PNG)

```
# pattern2.txt
111001001
100100111
111100111
```

이렇게 간단한 패턴이라면 쉽게 분류가 되지 않을까?

![(실행화면-ㄱ)](/img/in-post/post-multipayer-perceptron/10.png)

어째서일까.. 간단한 패턴도 읽히지 못하다니..ㅠㅠ<br>
혹시나 싶어서 ㄴ을 넣어 보았다.

![(실행화면-ㄴ)](/img/in-post/post-multipayer-perceptron/11.png)

띠용? ㄴ은 잘 나온다. 어째서일까.. 혹시 ETA(Learning Rate) 값 문제는 아닐까 싶어서, ETA값을 1로 설정하였다.

![(실행화면-ㄱ)](/img/in-post/post-multipayer-perceptron/12.png)

이번엔 ㄱ이 연상되었다! 역시 ETA값의 문제였던 것인가?

![(실행화면-ㄴ)](/img/in-post/post-multipayer-perceptron/13.png)

![(실행화면-ㄷ)](/img/in-post/post-multipayer-perceptron/14.png)

하지만 이번엔 반대로 ㄴ과 ㄷ의 패턴 분류에 실패하였다.. ~~미칠 노릇이다.~~<br><br>
이 이후에도 ETA값과 초기 Weight값을 계속 조정하면서 실행시켜 보았지만, 결국 하나 이상의 패턴을 분류하는 것에는 실패하고 말았다. <br>
3일간 연속 디버깅 후 데드라인은 다가왔기에, 눈물을 머금고 이 실험은 **실패** 처리하기로 하였다..

## 평가

구현 중 어려움을 겪었던 부분은 하나는 학습을 디버깅하는 과정에서, 이게 정말 맞게 데이터가 흘러가는 것인지를 알기 힘들었다는 것이다. 분명히, EPOCH가 전진될수록, Weight값의 오차값은 줄어들었다. 그러나 위에서 본 것처럼 패턴 분류가 잘 되지 않는걸로 보아, 분명히 뭔가 잘못됬음을 알고 있음에도, 그 문제점을 찾을 수가 없었다. 계산 수식을 200번쯤 검토한 것 같지만, 수업ppt와 교재에 나와있는 식과 정확히 일치함을 확인할 뿐이었다. 그렇다면 문제는 200번의 수식 검토를 했음에도 내가 놓친 부분이 있거나, 아니면 애초에 수식 적용을 잘못한 것이 아닐까?<br>
실습에 사용된 수식은 수업시간에 배운 수식 그대로 사용하였다. 사실 수업시간에 배운 수식으로 코딩하는 것은 사실 어렵지 않았다. 나와있는 수식 그대로 코딩하였고, 수식이 맞으니 당연히 결과도 잘 나올것이라고 생각했다. 그 생각이 굉장히 오만한 생각이었다고 깨달은 것은 3일동안 디버깅을 하면서 원인을 찾지 못해 결국 실험을 실패로 결론지을 때였다. <br>
결국 근본적인 실험 실패 이유는, 아무래도 딥러닝(Deep Learning)에 대한 전반적인 지식이 부족한 상태에서, 다층 퍼셉트론을 구현했기 때문이라고 생각한다. 수학 문제를 풀려면 수식을 외워야 하는 것은 기본이다. 그러나 수학을 마스터하려면 수식을 이해해야한다. 난 그 수식을 외우지도 못했을 뿐더러 당연히 이해도 못했다. 보다 이 수식을 잘 이해하려면, 딥러닝 공부를 기초부터 다시 해야하는 수 밖에는 없는 것 같다..

## 실습 후기
당연히 PPT대로, 배운대로 학습 시키면 될 것이라고 생각한 내가 어리석었다는 생각까지 들었다. 이렇게나 연상이 어렵고 패턴 분류가 힘든 것일 줄이야... 인공 신경망 100년 역사가 괜히 있는게 아니구나 싶었다. 그걸 다 알고있다고 착각하고 C++로 처음부터 구현할 생각을 했다니.. 물론 공부 목적에서 직접구현을 한 것도 있지만 생각보다 너무 시간을 잡아먹어 비효율적이라는 생각마저 들었다.<br>
 무엇보다 가장 힘들었던 건, 딥러닝에 대해서 제대로 터득하지 못한 상태에서 구현하는 것이 어려웠다. 수업시간에 가르쳐 준것은 인공지능 전반의 지식으로, 머신러닝 수업은 사실 아니다. 대표 인공 신경망인 다층 퍼셉트론에 대해서 수업에서 배웠을 뿐, 구현 자체는 가이드라인만 받았을 뿐 직접 알아보고 해야했다. 직접 알아보는 과정에서, 수업시간엔 나오지 않은, 혹은 용어가 다른 개념들이 등장하면서 머릿속이 더 복잡해지기만 했다. 주변에 인공지능에 대해 잘 아는 사람이 없어 코드 리뷰를 받지 못하는 것도 실패의 원인이기도 하다. 무엇보다 가장 신경쓰이는 것은 아직까지도 제대로 된 원인을 찾지 못했다는 것이다.<br>
 인공 신경망 구현에 대해 직접 찾아보기도 하고 여기저기 물어보던 중, 파이썬에는 인공 신경망 구현을 보다 쉽고 깔끔하게 해주는 라이브러리가 많이 나와있다고 한다. 기존에 파이썬을 쓰지 않았던 이유가 인공신경망 라이브러리를 그대로 제공해 줄 것 같아서 공부가 될까 싶어서 쓰지 않았었는데, 그대로 제공해 주는 것이 아닌 단순히 지원 라이브러리라면, 다음 구현 기회가 있다면 파이썬 라이브러리를 활용하여 보다 효율적으로 인공지능 신경망을 구현해 볼 수 있을 것 같다.

 _주관적인 생각이 많이 들어간 포스트입니다. 지적은 언제나 환영입니다!_

> 출처 : <https://sacko.tistory.com/10>
> <http://blog.naver.com/PostView.nhn?blogId=samsjang&logNo=221033626685&parentCategoryNo=&categoryNo=87&viewDate=&isShowPopularPosts=true&from=search>