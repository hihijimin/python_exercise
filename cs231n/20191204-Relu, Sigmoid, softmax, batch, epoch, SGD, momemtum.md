![image](https://user-images.githubusercontent.com/56099627/96572081-611e3300-1307-11eb-9064-9becaad62a0a.png)

# Relu
  
# Sigmoid  
<img src="https://latex.codecogs.com/gif.latex?y=\frac{1}{1&plus;e^{-x}}" title="y=\frac{1}{1+e^{-x}}" />  
  
# softmax 함수 구현시 단점(문제점)  
  overflow 문제 생김 softmax 함수는 지수함수를 사용하는데 아주 큰 값을 내뱉어내기 때문  
  일반적으로 회기에는 항등함수를, 분류에는 softmax 함수를 사용함  
  n은 출력층의 뉴런수, k번째 출력, ak는 입력신호  
<img src="https://latex.codecogs.com/gif.latex?y_{k}=\frac{exp(a^{_{k}})}{\sum_{n}^{i=1}exp(a^{_{i}})}" title="y_{k}=\frac{exp(a^{_{k}})}{\sum_{n}^{i=1}exp(a^{_{i}})}" />  
# 근데 이 문제를 보완하는 방법은?  
  <div class="colorscripter-code" style="color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#fafafa;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px;border-right:2px solid #e5e5e5"><div style="margin:0;padding:0;word-break:normal;text-align:right;color:#666;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="line-height:130%">1</div><div style="line-height:130%">2</div><div style="line-height:130%">3</div><div style="line-height:130%">4</div><div style="line-height:130%">5</div><div style="line-height:130%">6</div><div style="line-height:130%">7</div><div style="line-height:130%">8</div></div></td><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#010101;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">exp_a&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">=</span>np.exp(a)</div><div style="padding:0 6px; white-space:pre; line-height:130%">sum_exp_a&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">=</span>np.sum(exp_a)</div><div style="padding:0 6px; white-space:pre; line-height:130%">y&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">=</span>&nbsp;exp_a&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">/</span>sum_exp_a</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%">c&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">=</span>np.max(a)</div><div style="padding:0 6px; white-space:pre; line-height:130%">exp_a&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">=</span>np.exp(a<span style="color:#0086b3"></span><span style="color:#a71d5d">-</span>c)&nbsp;:&nbsp;오버플로우&nbsp;대책</div><div style="padding:0 6px; white-space:pre; line-height:130%">sum_exp_a&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">=</span>np.sum(exp_a)</div><div style="padding:0 6px; white-space:pre; line-height:130%">y&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">=</span>&nbsp;exp_a&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">/</span>sum_exp_a</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#e5e5e5;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>

# batch 와 epoch 헷갈리지 말자
batch의 크기는 내부 모델 파라미터를 업데이트 하기 전 샘플의 개수  
즉, 200개의 샘플 데이터가 있는데 batch zise =20 이라면, 총 batch가 10개 있다는 말  
만약에 201개 샘플 데이터를 20 배치사이즈로 한다면 딱 맞아떨어지는 사이즈가 아닐때는 평등하게 나눠지도록 고려하여 1개를 제거하고 평등하게 배치 사이즈 크기를 고려 하면 된다.  

epoch의 개수는 알고리즘이 전체 훈련 데이터셋을 반복해서 학습하는 횟수를 의미함
epoch의 사이즈는 한개 혹은 무한히 결정될수 있음
eopch =1 이라면, 전체 샘플데이터 200을 반복없이 학습한다는 말  

`즉, batch=1 는 데이터 셋(20) , epoch=1 은 데이터 셋 전체(200)`  
참고로, 확률적 경사하강법은 전체 데이터(200)에서 반복당(1 epoch 당) 무작위로 20개 선택한 데이터 하나의 예(batch size 1)만을 사용하는 거 말함  

**예제**  
200개의 샘플을 가진 훈련데이터셋이 있다. batch size =20, epoch =1000  
결과) 데이터셋은 10개의 batch size 생성되고 모델의 가중치는 각 배치들이 수행될대마다 업데이트 됨  
      1개의 epoch 수행하는데 10번의 가중치가 업데이트 된다는 것  
      1000개의 epoch 이므로 총 10,000번의 가중치 업데이트가 수행됨  
      (추가) 오류를 최소화하는 가중치 업데이트는 확률적 경사 하강법을 이용해서 업데이트되 됩니다
      
# 확률적 경사 하강법(Sthochastic Gradient Desent)  
**인공신경망 모형**  
<img src="https://latex.codecogs.com/gif.latex?Y=f(X)=\sigma&space;(\sum_{i}^{n}w_{i}g_{i}(X))" title="Y=f(X)=\sigma (\sum_{i}^{n}w_{i}g_{i}(X))" >  
f: 비선형 함수  
X: 연속형 혹은 이산형 변수들의 벡터, input nodes  
Y: 연속형 혹은 이산현 변수들의 벡터, output nodes  
g: X의 함수, g(X)은 hidden nodes  
<img src="https://latex.codecogs.com/gif.latex?\sigma" title="\sigma" >: Activation Function  
<img src="https://latex.codecogs.com/gif.latex?w_{i}" title="w_{i}" >: 가중치  
  
**경사하강법(Gradient Desent)** 은 주어진 모든 데이터에 손실 함수를 계산해 구하고 손실함수를 최소화하기 위해 사용되는 것이 가중치이고 이 가중치를 업데이트 하는 방법론이다.  
즉, 손실(cost)을 줄이는 알고리즘!, 미분값(기울기)이 최소가 되는 점을 찾아 알맞은 weight을 찾아 낸다.  

<img src="https://latex.codecogs.com/gif.latex?x_{0}=x_{0}-\eta&space;\frac{\partial&space;f}{\partial&space;x_{0}}" title="x_{0}=x_{0}-\eta \frac{\partial f}{\partial x_{0}}" >

<img src="https://latex.codecogs.com/gif.latex?\eta" title="\eta" />: step size(기계학습에선 learning rate)  
<img src="https://latex.codecogs.com/gif.latex?\frac{\partial&space;f}{\partial&space;x_{0}}" title="\frac{\partial f}{\partial x_{0}}" >: 미분값=기울기(단일 가중치에 대한 손실의 기울기)  
만약에 이동하는 폭이 항상 일정하다면??  
최저점을 지나칠수도 있다(오버슈팅)  
이동폭이 2인데 최저점까지 거리가 0.5라면 다음 걸음에선 최저점을 지나치게 될 것이다....  
그래서 `**이동폭의 크기를 기울기의 크기에 비례하도록 조정**`한다면 목적지에 거의 도달 했을때 작은 폭으로 이동할 수 있을 거다  
local minima에 빠지는 것을 피하려면 각각 다른 출발점에서 시작해 여러번 학습하는 방법을 하면 된다. 즉, `신경망에선 가중치의 초기값을 다르게 주는 것을 의미한다.` 근데 이 방법도 지역 최적화 하거나 데이터양이 많을 때는 컴퓨터 자원이 부족한 상황 등이 발생하여 적합한 방법이 아니다.  
`데이터 일부를 선택한 후 반복실행해서 가중치를 업데이트하는 학습과 같은 효과를 얻는 확률적 경사 하강법`을 사용한다.  
근데 **확률적 경사 하강법(Stochastic Gradient Descent)** 은 주어진 데이터 전체를 모두 업데이트 하는게 아니라 데이터 일부만 활용해서 가중치를 업데이트 하는 것(한 번만 아닌 일부를 여러번 사용해서 업데이트 함)  
배치크기가 1인 경사하강법 알고리즘  
즉, 데이터 세트에서 무작위로 균일하게 선택한 하나의 예를 의존하여 각 단계의 예측 경사를 계산한다.  
예를 들어 데이터 1000개 있다면 5등분 해서 처음에서는 200개 데이터 가중치 업데이트하고, 두번째 200개를 가중치 업데이트 진행 함  

**확률적 경사 하강법** 의 목적은 global minima인데 local minima에 빠지는 문제점이 발생한다.  
이때 가중치 업데이트는 기울기에 비례해서 업데이트(움직) 되는데 기울기가 작아지다(local minima)가 커지는 부분(local minima를 지나는 부분)에서 오류가 높아지는 걸 착각하고 더 이상 업데이트를 진행하지 않는다.  

이 오르막길를 오르기 위해서는 **모멤텀(Momemtum)** 이 필요하다.  


**모멤텀(Momemtum)이란?**  
운동량을 뜻하는 단어로 물리 현상과 관련 있다.  
<img src="https://latex.codecogs.com/gif.latex?v_{t&plus;1}=&space;\mu&space;v_{t}-\epsilon&space;g(\theta&space;_{t})" title="v_{t+1}= \mu v_{t}-\epsilon g(\theta _{t})" >  
<img src="https://latex.codecogs.com/gif.latex?\theta_{t&plus;1}=&space;\theta_{t}&plus;v_{t&plus;1}" title="\theta_{t+1}= \theta_{t}+v_{t+1}" >

<img src="https://latex.codecogs.com/gif.latex?\epsilon" title="\epsilon" >-epxilon은 학습속도, <img src="https://latex.codecogs.com/gif.latex?\epsilon" title="\epsilon" > 는 모멘트 효과에 대한 가중치, <img src="https://latex.codecogs.com/gif.latex?v_{t}" title="v_{t}" >는 0으로 초기화 되어 있고 반복이 될때마다 현재의 그래디언트 <img src="https://latex.codecogs.com/gif.latex?-\epsilon&space;g(\theta&space;_{t})" title="-\epsilon g(\theta _{t})" >가 다음번 모멘트<img src="https://latex.codecogs.com/gif.latex?v_{t&plus;1}" title="v_{t+1}" >에 누적된다. 그리고 다음번 반복에서 <img src="https://latex.codecogs.com/gif.latex?v_{t&plus;1}" title="v_{t+1}" >가 현재의 모멘트<img src="https://latex.codecogs.com/gif.latex?v_{t}" title="v_{t+1}" >로 사용된다. 경사하강법(Gradient Desent)에서 모멘트 항이 추가된 것이다.

# 확률적 경사하강법(SGD)의 단점과 극복하기
**단점**  
반복이 충분하면 SGD가 효과는 있지만 노이즈가 매우 심하다  
SGD는 여러 변형 함수의 최저점에 가까운 점을 찾을 가능성이 높지만 항상 보장되지는 않다(최저점을 못찾을수 있음)  
**단점 극복하기**
**미니 배치 확률적 경사하강법(Mini-batch Gradient Descent)** 은 전체 배치 반복과 SGD의 절충안  
한개 epoch에서 미니배치라는 임의의 샘플 세트만으로 계산을 진행 하는 것



  
  

참고해서 보자  
[1] https://seamless.tistory.com/38, 딥러닝 살펴보기 2탄  
[2] https://www.kakaobrain.com/blog/113, 배치(batch) 크기에 따른 모델의 훈련 시간과 학습 곡선(learning curve)[2]의 상관관계, LARS의 특징, torchlars 개발 프로젝트  
참고  
[1] 밑바닥부터 시작하는 딥러닝 p93  
[2] https://m.blog.naver.com/PostView.nhn?blogId=tjdudwo93&logNo=221325685474&proxyReferer=https%3A%2F%2Fwww.google.com%2F, 신경망의 핵심 parameter인 batch 그리고 epoch  
[3] https://everyday-deeplearning.tistory.com/entry/SGD-Stochastic-Gradient-Descent-%ED%99%95%EB%A5%A0%EC%A0%81-%EA%B2%BD%EC%82%AC%ED%95%98%EA%B0%95%EB%B2%95, Gradient Descent(경사하강법) 와 SGD( Stochastic Gradient Descent) 확률적 경사하강법  
[4] https://m.blog.naver.com/PostView.nhn?blogId=tjdudwo93&logNo=221081308760&navType=tl, 심층신경망에서의 확률적 경사 하강법 그리고 DNN R 실습
