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

