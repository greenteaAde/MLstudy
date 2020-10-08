# Tree Model Review

## 1. Decision Tree

- 독립 변수에 대한 기준값(threshold)를 기준으로 나눔
- 잎 노드들의 **엔트로피(entropy)값이 최소가 되는 방향으로** 분류를 수행
- 상위 노드부터 분류 규칙을 적용하여 잎 노드의 조건부 확률 분포를 이용하여 분류 예측

### 크로스 엔트로피(Cross-Entropy)
<br/>
<p align="center"><img src="https://blogfiles.pstatic.net/MjAyMDAzMTRfMjYw/MDAxNTg0MTgxNzczOTAw.y-ZuV0sFZPZ83OV-viY1Ls6w-7fPMDE-0oyHFdUxyhEg.g9-bcpMY4p-PM3f6U5kuiPqPAmm0mjluaeVRwbz0XIkg.JPEG.mint_vkkk/6.JPG?type=w2"></p>
<br/>

&nbsp; *D*는 Distance, 즉 거리를 뜻하고, *S*는 예측한 값, *L*은 실제 값을 뜻한다.
Cross Entropy를 이해하기 위해서는 먼저 **정보이론**(Information Theory)를 알아야 한다.


- **정보량(Information Gain)**: degree of surprise, 즉 놀람의 정도. 일어날 확률이 낮은 사건일수록 정보량이 큼

&nbsp; 정보량를 식으로 나타내면 다음과 같다.

<br/>
<p align="center"><img src="https://blogfiles.pstatic.net/MjAyMDAzMTRfMjYw/MDAxNTg0MTgxNzczOTAw.y-ZuV0sFZPZ83OV-viY1Ls6w-7fPMDE-0oyHFdUxyhEg.g9-bcpMY4p-PM3f6U5kuiPqPAmm0mjluaeVRwbz0XIkg.JPEG.mint_vkkk/6.JPG?type=w2"></p>
<br/>

&nbsp; 윗 식에서 *S*는 확률값이므로 [0,1]의 값을 가진다. 그러니 *-log(S)*는 0에 가까울수록 무한대, 1에 가까울수록 0이 된다.
그래프로 표현하면 다음과 같다.

<br/>
<p align="center"><img src="https://blogfiles.pstatic.net/MjAyMDAzMTRfMjEg/MDAxNTg0MTgxNzc3NTg3.9RpboFQr__oZ9JtMbDI7YhMrZDhh5K0j-75uXhSPg_Ig.v3voZ_2SDv0duntSK8fsBIM7TQ5GkbRGGPQh8RTNStAg.PNG.mint_vkkk/cross_entropy.png?type=w2"></p>
<br/>

&nbsp; 따라서 사건이 일어날 확률 *S*가 낮을수록 더욱 놀라운 사건이라고 판단하고, 정보의 가치가 높아지는 것이다.

- **엔트로피(Entropy)**: 정보량의 평균. 불확실성의 정도를 나타내며 높을수록 집단의 특성을 찾는 것이 어려움

&nbsp; 앞서 Tree Model은 엔트로피를 최소화하는 방향으로 학습을 진행한다고 말했다.
왜 학습을 엔트로피가 최소화하는 방향으로 진행해야 하냐고 묻는다면 바로 예측값 *S*와 실제값 *L*의 거리를 최소화하는 것이 곧 *S*의 엔트로피를 최소화하는 것과 같기 때문이라고 답할 수 있을 것이다. 이를 이해하기 위해 상대적 엔트로피(relative entropy)라고 불리는 **KL-Divergence**를 알아보자. KL-Divergence의 식은 다음과 같다.

<br/>
<p align="center"><img src="https://blogfiles.pstatic.net/MjAyMDAzMTZfMTA5/MDAxNTg0MzYxNTY4NjE4.MZxh8hE4WkO11Ne3-8dmvmHgwi8vr_h3VWx0n2avQVYg.DqTjTlhqHU0A3VoilI58n3aKMKLuEKZ5oX7DL-bCo-Ag.JPEG.mint_vkkk/1.JPG?type=w2"></p>
<br/>

&nbsp; 윗 식의 두번째 줄은 *S*와 *L*의 엔트로피의 차이를 표현하고 있다.
KLD 값은 예측한 확률이 실제 값과 같아질수록 0에 가까워진다.
즉, KLD가 0인 모형이 이상적인 모형이 된다. 
윗 식에서 KLD를 어떻게 0으로 만들 것인지는 쉽게 확인할 수 있다. 바로,

<br/>
<p align="center"><img src="https://blogfiles.pstatic.net/MjAyMDAzMTZfMTU1/MDAxNTg0MzYzNjI4Nzc3.XtEtHzAe4ELbsJmpjELVvIJZFQwec2VSgaQCdaNl1Jkg.F3Scle6G29Lop1_MPSG729Z4dWg2CU9R056aCHSyxa4g.JPEG.mint_vkkk/q.JPG?type=w2"></p>
<br/>

를 최소화하는 것이다. 본래 entropy를 구하려면 *logS* 대신 *logL*을 넣어주어야 하나, 모형의 최적화를 위해 *S*를 넣어주기 때문에 cross entropy라고 부른다.

<br/>
## Random Forest

