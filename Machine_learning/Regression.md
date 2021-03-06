# Regression

독립변수 = 특성변수, 설명변수, 예측변수

종속변수 = 타겟변수, 반응변수



단순 회귀 : 독립변수 X가 1개

다중 회귀 : 독립변수 X가 2개 이상



일변량 회귀 : 종속변수 Y가 1개

다변량 회귀 : 종속변수 Y가 여러 개



## 단순선형회귀분석(Simple linear regression)

: 독립변수 X 하나만 가지고, 연속형(숫자형) 종속변수 Y를 예측하는 모델

선형함수



Y = α + β*X + ε



E(Y) = Y^ = α + β*X



ε 오차(관찰 불가능) = e 잔차(관찰 가능)

이 때 오차 ε는 정규, 등분산, 독립의 가정을 한다.

관찰 불가능한 오차 대신에 관찰 가능한 잔차를 사용한다.

오차에 관한 적정성 검토를 잔차를 이용하여 수행한다.



회귀계수 : 절편(α), 기울기(β)

α, β는 미지의 모수로, 상수임



우리에게 주어지는 것은 n개의 표본인 관측치(xi, yi)임.

이 n개의 점들, 즉 자료를 잘 요약하는 직선의 α^, β^을 찾아내는 것으로 모수 α, β를 추정하는 것이다.



어떻게 하면 자료를 잘 요약하는 직선인가?

최소제곱법

: n개의 ‘수직거리 제곱합’이 최소가 되도록

자료가 선과 갖는 수직 거리가 n개 있을 텐데, 그 거리가 작은 것



회귀계수의 유의성 t검정

왜 하는가?

우리가 관찰한 n개가 특이해서 우연한 값 β를 찾아낸 것이 아닌가?

과연 β가 0이 아니라고 말할 수 있는가? 하는 고민에서.



-> β에 관한 가설검정을 수행한다. (일표본에서 모수에 관한 추론 one-sample t-test와 매우 유사)

귀무가설 H0: β = 0

대립가설 H1: β != 0



귀무가설이 기각되어야만 (β가 0이 아니므로) X가 Y를 설명하기에 유용한 변수라고 할 수 있다.

-> 독립변수에 대한 유의성 검정, t-검정



귀무가설 H0이 사실일 때(β=0이면),

T라는 통계량 값(β^ / 표준오차)은 평균 0의 자유도 (n-2)의 분포



대립가설의 방향은 양쪽 꼬리 방향



p-value가 유의수준보다 작으면 귀무가설 기각

-> X가 Y를 설명하는 데 유용하다.

-> 이 회귀모델이 의미가 있다.



Y의 변동성 분해



제곱합

SST(Total: yi의 y평균으로부터의 변동) = SSR(Regression: 모형으로 설명되는 변동) + SSE(Error: 모형으로 설명되지 않는 변동)



결정계수(R\**2) = SSR/SST = 1 - SSE/SST

: 모델에 대한 적합도 지표

항상 0~1 사이 값을 가짐

yi의 총 변동 중에서, 추정된 회귀모형으로 설명되는 변동의 비중을 의미한다.

모델의 설명력을 의미!

1에 가까울수록 좋다.

두 변수 간의 상관계수 r의 제곱과 같다.

<- 선 주변의 데이터 응집력 |r|을 알 수는 있지만, 양의 상관관계인지 음의 상관관계인지는 알 수 없다.

추가로, r=1이라고 해서 기울기도 1인 것은 아니다.

r은 데이터 응집력을 의미!!



ex) R2 값이 0.65라면, Y의 총 변동 중에서 65%는 X를 이용해서 설명할 수 있다고 해석할 수 있다.



## 다중회귀분석(Multiple linear regression)

: 독립변수 X가 2개 이상

X가 1개인 단순선형회귀분석보다 적합도가 나아지고 설명력이 높아질 것으로 기대할 수 있음.



다른 변수들이 고정되어 있다는 것을 가정하고, β의 효과를 해석해야 한다.



범주형 독립변수를 회귀모형에 포함하기 위해서는 더미변수 기법을 사용해야 한다.

더미변수

: 0 또는 1의 값을 갖는 변수로 정의

더미변수의 개수 = 범주의 개수 - 1

(독립변수들 간에 완벽한 선형관계가 존재하면, 최소제곱법으로 모수(회귀계수), 즉 회귀모형 추정이 되지 않는다. 그래서 마지막 더미변수는 뺀다.)



각 범주별로 더미값 0, 1을 대입해서 회귀계수 추정식을 다시 각각 써보면, 

절편의 차이로 범주형 독립변수들에 따른 평균값 차이를 알 수 있다.



다중회귀모형의 변수선택

: 가능한 적은 수의 독립변수(설명변수)로 좋은 예측력을 갖는 모형을 찾고자 함.

적은 수의 최적의 독립변수 조합을 찾아내기!!

정보가 중복되거나, Y를 설명하는 데에 도움이 안되는 X들 걸러내고 꼭 필요한 것들만 남기자.



변수선택법 Filter, Wrapper, Embedded 가운데 Wrapper 방식

- 모든 가능한 조합의 회귀분석

​	: X가 너무 많으면 비효율적이거나 불가능

- 전진선택법 (forward selection)

​	: 절편만 있는 모델에서 출발하여 가장 중요한 변수를 하나씩 추가하는 방식

​	부분 F검정을 통해 변수의 유의성을 판단한다.

​	한번 선택된 변수는 제거되지 않는 단점이 있음 (기존에 선택된 변수와 중복된 정보를 공유하고 있는 변수가 추가될 수 있음)

- 후진제거법 (backward elimination)

​	: 모든 변수가 포함된 모델에서 가장 중요하지 않은 변수부터 하나씩 제거

​	제거하느냐 마느냐도 부분 F검정을 통해 판단

​	한번 제거된 변수는 선택되지 않는 단점이 있음

- 단계별 방법 (stepwise method)

​	: 한 번의 스텝에 전진선택법, 후진제거법을 순차적으로 하는 것.

​	선택과 제거를 매번 고민하여, 의미를 상실한 변수를 제거한다.

​	절편만 포함된 모델에서 출발해 가장 중요한 변수부터 추가하고, 모델에 포함되어 있는 변수 중에서 중요하지 않은 변수를 제거함.

​	더이상 새롭게 추가되는 변수가 없을 때까지 변수의 추가 또는 삭제를 반복.



모형 선택의 기준

: 변수 선택의 매 스텝을 진행하는 데 부분 F검정, T검정을 활용하기도 하고, 적합도 지표를 통해서 판단하기도 한다.

그러나 R2는 변수선택 고려에서는 사용하면 안 된다.

SSE는 독립변수가 늘어나면 줄어들 소지가 있다.

따라서 결정계수 R2 = SSR/SST는 새로운 독립변수가 추가되면 항상 증가한다.

(불필요한 독립변수가 추가되어도 R2가 개선된다는 것)

그러므로 R2로 판단한다면 무조건 독립변수를 많이 추가하라고 할 것이다.



이를 보완하기 위한

수정결정계수 (adjusted R\**2) = 1 - (SSE/(n-k-1)) / (SST-(n-1))

각 제곱합을 각각의 자유도로 나눈다. (k는 독립변수의 개수)

모형에 새로운 독립변수가 k만큼 추가되어도 분자, 분모가 동시에 작아진다.

자유도에 비해 SSE가 많이 줄어드는 경우, 수정결정계수가 커지는 것이다.

자유도가 패널티 역할을 하는 것이다. -> 패널티를 감안해도 SSE가 충분히 작아진다면, 수정결정계수가 증가한다고 해석하면 된다.



-> 따라서, 독립변수 선택 문제에서는 결정계수(R2)가 아니라 수정결정계수(adjusted R2)를 사용해야 가능한 한 적은 독립변수로 설명력 있는 모형을 만드는 최적의 독립변수 조합을 남길 수 있다.



이 밖에도 AIC, BIC, Mallow’s Cp 등의 다양한 적합도 지표를 이용할 수 있음.



결정계수(R2), 수정결정계수(adjusted R2)는 클수록 좋다.

AIC, BIC, Mallow’s Cp는 작을수록 좋다.

-> 이러한 적합도 지표를 통해 그 변수가 유입되는 것이 유용하다는 판단



회귀분석의 마지막 단계에서는

회귀모형에서 가정이 적절한 것인지? 체크

오차에 대한 가정(정규, 등분산, 독립)이 적절한가?를 확인하는 것이 필요

이것을 오차에 대한 추정치 개념인 잔차를 이용하여 분석한다.

이것이 잔차분석



잔차분석방법은 검정을 통한 방법과 그래프를 통한 시각적 확인 방법이 가능하다.

진단방법



시각적 방법을 이용할 경우 : 히스토그램, QQ플롯, 잔차산점도

- 오차의 정규성 확인 : 히스토그램(구간의 간격을 어떻게 설정하느냐에 그래프 모양이 영향을 많이 받음), QQ플롯(이 더 선호된다. 이론분위수와 샘플분위수를 그 표본자료를 이용해서 관찰한 다양한 p-value에 대해서 산점도 형태로 표현한 것. 직선을 기준으로 점들이 잘 모여있으면 정규분포를 따른다고 볼 수 있음. 점들의 분포가 지수함수처럼 생겼으면 오른꼬리가 긴 분포, 로그함수처럼 생겼으면 왼꼬리가 긴 분포.)
- 오차의 등분산성 확인 : 잔차산점도(가로축은 보통 y^(y추정치), xi, i 등이 올 수 있고, 세로축이 잔차 ei. x축에 따라 분산이 일정하면 등분산으로 본다.)
- 오차의 독립성 확인 : 잔차산점도(특별한 함수적인 패턴관계가 보이지 않으면 독립을 가정하는 것으로 본다.)



가정 위반이 진단되면 어떻게 해결하느냐?

해결방법

- 오차의 정규성 위반 : 변수변환(박스콕스 변환)
- 오차의 등분산성 위반 : 가중최소제곱(WLS)회귀(최소제곱합을 분산의 역수곱으로 가중치를 두는 것. 변동성이 큰 자료는 적은 비중으로 계수 추정에 반영되고, 변동성이 작은 자료는 안정적인 것이므로 가중치를 높여주는 효과를 주는 것.)
- 오차의 독립성 위반 : 시계열 분석(정상성 조건을 만족하는지, 만족한다면 autocorrelation의 구조가 어떤지 먼저 판단해야 함. -> 적절한 모델을 선택하여 분석)



다중선형회귀모형에서 하나의 Y를 여러 개의 X로 설명할 때, X들 간에는 상관관계가 어느 정도 존재하는 것은 자연스러운 현상이다. 그러나 너무 상관관계가 심해서 중복된 정보가 많으면 모형의 회귀계수 추정에 부정적 영향을 미친다.



다중공선성(multicollinearity)

: 독립변수들 간 강한 상관관계가 존재하여 회귀계수 추정에 부정적 영향을 미치는 현상

- 개별적 회귀계수 추정의 신뢰성이 떨어져 추정치를 믿을 수 없게 만듦(표본이 조금만 달라져도 회귀계수 추정량 β^의 변동성(분산)이 커지게 된다. 중복효과 때문에)
- 그런데 전반적인 모형의 적합성, 정확도는 크게 변하지 않음

결국 β는 이상하게 추정되지만, y는 안정적으로 추정이 잘 되는 현상.



다중공선성 진단 방법

VIF계수(variance inflation factor: 분산팽창요인) = 1 / (1 - Rj\**2)

Rj2 = xj를 종속변수로 두고 나머지 독립변수들로 xj를 설명하는 다중선형회귀모델에서의 결정계수

Rj2가 크다는 것은 나머지 독립변수들로 xj가 설명이 많이 된다는 뜻이다.

Rj2가 커지면 VIF계수가 커진다.

VIF계수가 5(Rj2=0.8) 또는 10(Rj2=0.9) 이상이면 다중공선성이 심각한 것으로 본다.

Rj2=0.8 이라는 것은 나머지 변수들로 xj가 80% 설명된다는 것이다.



다중공선성의 해결책

- 변수선택으로 중복된 변수를 제거
- PCA 등을 이용하여 중복된 변수를 변환하여 새로운 변수 생성
- 변수를 그대로 넣되, Rigde, Lasso 등으로 규제를 반영하여 중복된 변수의 영향력을 통제, 일부만 사용



## 규제가 있는 선형회귀모델 : Ridge, Lasso, Elastic Net

회귀계수 β, 파라미터들이 너무 커지지 않도록 규제하는 추정법

독립변수들 중 중요하지 않은 변수, 중복된 변수의 영향력을 규제하는 것

변수선택, 변수제거와 같은 효과를 기대할 수 있음

모델의 가중치를 제한하여 과적합 방지



머신러닝에서는 최소제곱합, loss function을 최소화하고자 함.

이 때 규제가 있다는 것은 길이가 긴 β^에 대해서 패널티를 두는 것. 이를 비용으로 인식하고 낮추게 됨.

즉, 수직거리 제곱합도 최소로 만들면서, 동시에 β의 값들도 전반적으로 작게 만드는 것

둘 중 무엇에 더 비중을 둘 것이냐를 결정하는 게 λ이다. λ가 크면 패널티의 비용이 높은 비중으로 인식되고, λ가 작으면 수직거리 제곱합을 최소화하는 데 보다 더 비중을 두는 것이다. λ가 0이면 패널티가 없는 것이므로 일반적인 회귀모형의 최소제곱합. λ가 크면 클수록 패널티에 대한 비중이 높아져서 β는 더욱 더 작은 값으로 추정된다.



벡터의 길이에 패널티를 두는데,

벡터의 길이를 어떻게 정의할 것인가?



- Ridge 회귀

: L2 규제

L2 norm을 패널티 항으로 정의.

βj 제곱의 합이 패널티

벡터의 길이를 인식



λ가 크면 규제 많음 -> 회귀계수 추정치가 작아짐

적절한 λ를 찾는 방법은 작은 λ에서 출발해서 시행착오를 거쳐 찾거나, 교차검증 등으로 최적화



결국 비용함수를 최소로 하는 회귀계수 β를 찾는 문제다.



Alternative formulation을 통해 λ에 대응하는 t를 두고 기하학적으로 해석을 해보면,

원점으로부터 어떤 원 안에서 찾되(제곱합이 t라는 조건 하, 원의 제약 하에), 항아리의 최솟값을 찾는 것(항아리의 등고선이 접하는 지점이 솔루션이 되는 것). -> 이러한 제약이 들어가서 0 부근의 β들이 추정치로 계산되는 것이다.



λ와 t는 1:1로 대응하는데

λ는 클수록 규제가 강한 것,

t는 작을수록 규제가 강한 것.



- Lasso 회귀

: L1 규제

L1 norm을 패널티 항으로 정의

βj 절댓값의 합이 패널티가 됨.



λ가 크면 클수록 규제가 강한 것



수직거리 제곱합 식이 절댓값 합 함수와 만나는 부분, 높은 확률로 코너, 즉 어떤 축 위에서 만날 것.

이게 일반적으로 성립하기 때문에

β1, β2, β3, β4를 구해보면 이 중 일부는 그냥 0이 된다.

<- 이게 바로 변수 선택으로 Lasso 회귀를 사용할 수 있는 이유. 자동 탈락됨.



-> Ridge는 파라미터가 0이 되지 않고 전반적으로 줄어드는 경향

Lasso는 제약 범위가 각진 형태라 파라미터 중 일부가 0이 되는 경향



최적의 지점으로 가지 못하도록 제약으로 묶어놓은 것이기 때문에

편의가 발생한다, 불편성을 만족하지 못한다고 표현한다. 오차가 생긴다는 것.

그러나 추정치의 분산이 더 작아지게 된다.

추정치가 0 부근에서만 추정되도록 한정해 놓았기 때문에.

일반화 오차는 편의2+분산인데, 분산이 줄어드는 효과가 있기 때문에 일반화 오차가 작아지기도 한다. (패널티 없는 모형에 비하여)(잘 튜닝된 λ를 쓰면)



이 아이디어는 선형회귀에만 적용되는 게 아니다.

오버피팅은 분산이 커서 생기는 문제이기 때문에, 오버피팅 문제가 있는 알고리즘에 가중치 제약을 두는 Ridge, Lasso 방식과 결합을 하면 분산을 줄여서 오버피팅 현상을 개선할 수 있다.



- Elastic Net 

: L2, L1의 규제를 혼합한 방식.

Ridge, Lasso회귀의 장점을 모두 가짐

이론적으로는 둘의 장점을 결합했지만,

추정이 복잡하기 때문에 항상 우월한 것은 아님


