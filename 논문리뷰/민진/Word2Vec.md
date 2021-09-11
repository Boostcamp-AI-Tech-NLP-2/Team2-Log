#### 1. 무슨 문제(task)를 풀고 있는가?
- 단어를 continuous vector로 효율적으로 embedding함으로써 다차원에 걸친 유사도 측정이 가능해졌다.

#### 2. 해당 연구 주제에서 아직 해결하고 있지 못했던 부분(problem)은 무엇인가?
- 신경망의 은닉층에서 computational bottleneck이 생기면서 연산 복잡도가 크다.

#### 3. 제안하는 방법(method)은 무엇인가?
- NNLM의 비선형 함수인 hidden layer를 제거했다.
- encoder, decoder 개념을 도입해서 단어를 임베딩한다.
- 주변 단어를 이용해 중심단어를 예측하는 CBOW, 그리고 반대로 중심단어를 이용해 주변단어를 예측하는 skip-gram 제시했다.

#### 4. 제안된 방법은 어떤 문제를 풀었는가? (contribution)
- 학습 시간을 대폭 줄이고, 단어들의 semantic, syntactic similarity에 대한 accuracy를 늘렸다.

#### 5. 제안된 방법은 어떤 한계를 지니는가?
- 단어를 임베딩하는 과정에서 corpus 내에서의 단어가 가지고 있는 특성 / probability를 잘 반영하지 못한다 (이후에 발표된 GloVe가 해소)
