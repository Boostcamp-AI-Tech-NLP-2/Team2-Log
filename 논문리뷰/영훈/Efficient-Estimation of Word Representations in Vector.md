# Efficient-Estimation of Word Representations in Vector Space(2013) - word2vec

## 1. Introduction

- 논문 체택 이유
- 처음으로 하는 논문 리뷰인 만큼 nlp의 시작이 되는 word2vec와 관련된 논문을 리뷰하고 싶었고, word2vec 관련 논문들 중 잘 알려진 해당 논문을 체택하였다.
- 기존 NLP에서는 단어를 atomic unit으로서 고려했고, N-gram 모델과 같이 단어간의 유사성을 고려하지 않아 단어를 개별적으로만 유추하여 여러 한계들을 지니고 있었지만 단순한 모델에 따라 시간 복잡도는 낮았다.
위와 같은 기존 방식들은 방대한 양의 data를 적절하게 학습할 수 없다는 것과 vector로 변환된 word의 차원이 50~100으로 차원이 낮다는 한계를 지니고 있었기 때문에 NNLM, RNNLM과 같은 더 복잡한 모델들이 나오게 되었다.
- 단어간의 유사도를 여러차원에서의 유사도로 측정하고, 단어 간의 linear regularity를 최대한 보존하는 model을 개발함으로써 vector("King")-vector("Man")+vector("Woman") ⇒ Queen이 나오는 vector operation의 정확도를 최대화 하려 하였고, 시간 복잡도를 최대한 낮추려 하였다.

## 2. Model Architectures

- [LSA](https://bkshin.tistory.com/entry/NLP-9-%EC%BD%94%EC%82%AC%EC%9D%B8-%EC%9C%A0%EC%82%AC%EB%8F%84%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%9C-%EC%98%81%ED%99%94-%EC%B6%94%EC%B2%9C-%EC%8B%9C%EC%8A%A4%ED%85%9C)(Latent Semantic Analysis)와 [LDA](https://wikidocs.net/30708)( Latent Dirichlet Allocation )와 같은 다양한 모델들이 연속적인 단어 표현을 estimating하기 위해 제시되었지만, 본 논문에서는 neural network를 이용하여 학습된 [distributed representations of words](https://soobarkbar.tistory.com/m/3)에 초점을 단어의 선형회귀를 더 잘 보존하고, 연산 비용을 낮추어 성능을 향상 시켰음.
( H = hidden layer size, V = number of word )
1. Feedforward Neural Net Language Model (NNLM)
  input, projection, hidden, output layer로 구성되어 있는 모델로, n개의 previous word를 input layer에서 1-of-V coding을 이용하여 인코딩하고 input layer를 projection layer로 projection 시킨 후 hidden layer를 거쳐 output layer로 결과가 나오게 된다. 이때 계산 복잡도는 다음과 같다.
             Q  = N * D + N * D * H + H * V
  NNLM은 projection layer에서 hidden layer로 넘어가는 과정에서 계산이 복잡해지는 문제가 있음.
본 논문에서는 Huffman Binary Tree로 표현된 vocabulary에 hierarchical softmax를 사용함으로써 H * V 복잡도를 줄임.

![Untitled](Efficient-Estimation%20of%20Word%20Representations%20in%20Ve%202f839579b9f94b00ad3b095514208ebd/Untitled.png)

1. Recurrent Neural Net Language Model ( RNNLM )
  RNN을 이용함으로써 context length를 제시해야하는 feedforward NNLM와 달리 context length를 제시하지 않고, 얕은 신경망으로 더 복잡한 패턴을 표현함으로써 feedforward NNLM의 한계를 극복하고자 제안되었다. 
  RNN을 이용한 model은 Projection Layer를 갖지 않아 input, hidden, output layer만을 갖고, 시간 딜레이를 이용하여 hidden layer가 자기 자신에 연결되게끔 하는 것이 특징이다. 이것은 짧은 기간에 대한 기억을 갖을 수 있게 되고 hidden state에 대하여 과거 정보에 대한 기억을 가지고 현재 input의 정보를 update할 수 있게 도와준다.
RNNLM의 시간 복잡도는 다음과 같다.
           Q = H * H + H * V ⇒ H * H 에 의해 대부분 결정.

## 3. New Log-linear Models

- 시간 복잡도를 최소화하며 distributed representations of words를 학습시키는 두 가지 모델을 제시하는데, previous work에서 non-linear hidden layer에 의해서 시간 복잡도가 크게 증가했다는 것을 참고하여 정확도를 조금 포기하는 대신 효율성을 높인 simpler model들을 제시했다.
1. Continuous Bag-of-Words Model(CBoW)
  CBoW model은 hidden layer가 없고, 모든 단어가 projection layer를 공유하여 모든 단어가 같은 position으로 projection 된다. 우리는 이러한 구조를 Bag of Word(BoW)모델이라 한다.
  해당 모델은 log-linear classifier를 4개의 과거 단어와 4개의 미래 단어를 input으로 사용했을 때, 현재 단어를 예측하는 것에서 가장 좋은 성능을 봄.
훈련 복잡도는 다음과 같다.
**Q = (N x D) + (D x log(V))**
우리는 continuous distributed representation of the context를 사용하는 이 구조를 기존의 표준적인 BoW와 구분되는 CBoW라고 한다. ⇒ 순서가 없고 있고의 차이가 있다.
  모든 단어들은 동일한 weight matrix를 사용하여 input layer에서 projection layer로 projection되는 것이 특징이다.

![Untitled](Efficient-Estimation%20of%20Word%20Representations%20in%20Ve%202f839579b9f94b00ad3b095514208ebd/Untitled%201.png)

1. Continuous Skip-gram Model(Skip-gram)
  Skip-gram은 문맥을 기반으로 현재의 단어를 예측하는 대신에 같은 문장 안에서 다른 단어들을 기반으로 단어 분류 성능을 최대화한다. 각각의 단어를 하나의 input으로 사용하여 정해진 범위 내에 있는 previous, future 단어들을 예측한다.
  범위를  증가시킬 수록 word vector의 결과가 향상되지만 이것은 계산 복잡성 역시 함께 증가시킨다. current word로부터 멀수록 가까운 단어보다 적게 관련되어 있기 때문에 weight를 거리에 따라 조절하였다.
Skip-gram의 훈련 복잡도는 다음과 같다.
**Q = C x (D + D x log(V))**
이때 C는 단어간 거리의 최대값이다. 또한 본 논문에서는 C를 5로 선택하였다. 각각의 training word에 대하여 1~C 사이의 임의의 수 R을 선택하였고 R개의 과거단어와 R개의 미래단어를 현재 단어의 정답 label로 설정하였고,이것은 (R x 2)의 단어 분류를 필요로한다.

![Untitled](Efficient-Estimation%20of%20Word%20Representations%20in%20Ve%202f839579b9f94b00ad3b095514208ebd/Untitled%202.png)

## 4. Result

본 논문에서는 많은 데이터를 가지고 훈련한 고차원의 word vector의 결과는 단어 사이의 매우 미묘한 의미적인 표현에 사용 할 수 있음을 밝혔고, word vector간의 단순한 대수적인 연산을 통해서 유사한 단어를 찾는 것을 가능하게 하였다. X = vector(biggest) -  vector(big) + vector(small)

### 참조

- coshin님의 논문리뷰 : [https://coshin.tistory.com/m/43](https://coshin.tistory.com/m/43)
- 논문 원본 —

[EfficientEstimationOfWordRepresentations.pdf](Efficient-Estimation%20of%20Word%20Representations%20in%20Ve%202f839579b9f94b00ad3b095514208ebd/1301.3781.pdf_.pdf)

- 선형 회귀 — [https://datascience.stackexchange.com/questions/46648/what-does-linear-regularities-among-words-mean](https://datascience.stackexchange.com/questions/46648/what-does-linear-regularities-among-words-mean)
- Feedforward NNLM — [https://www.jmlr.org/papers/volume3/tmp/bengio03a.pdf](https://www.jmlr.org/papers/volume3/tmp/bengio03a.pdf)
- wikidoc - [https://wikidocs.net/22660](https://wikidocs.net/22660)