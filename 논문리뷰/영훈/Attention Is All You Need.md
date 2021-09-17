# Attention Is All You Need

## 0. Conclusion

- 해결하고자 하는 문제
⇒ 기존에 sequence transduction model으로 RNN(or CNN)과 attention이 함께 사용되던 모델들은 RNN의 sequential computation 문제를 안고 있어 효율성이 떨어짐
- 제안하는 방법 ( Method )
⇒ RNN(or CNN) model과의 혼용없이 attention mechanism만이 사용된 network architecture( Transformer )를 제안.
⇒
- 제안된 방법은 어떤 문제를 풀었는가?(contribution)
⇒ RNN을 혼용하지 않는 only attention mechanism model로서 기존 모델들이 갖고 있던 sequential computation문제를 해결하고, output quality또한 향상시킴.

## 1. Introduction

- 논문 채택 이유
- 부스트캠프에서 NLP과정을 수강하던 중 본 논문이 다시 한 번 더 상기되었고, 팀원들과 함께 간단하게라도 리뷰를 하기로 하였음. 또한 8월에 진행한 이론 강의에서도 중요하게 다루었었기 때문에 리뷰를 한 번쯤 해보고자 하는 생각이 있었기에 리뷰를 진행함.
- Abstract
- 지배적인 sequence transduction model은 하나의 encoder와 하나의 decoder를 갖는 RNN or CNN 에 기반을 두고 있다. 본 논문에서는 오직 attention mechanism에만 기반을 둔 간단한 network architecture( Transformer )를 제안한다. 해당 model은 two machine translation task에 대해 높은 quality와 빠른 train을 제공한다.
- Introduction
- RNN, 특히 LSTM과 GRU는 sequence modeling과 language modeling이나 machine translation 같은 transduction problem에서 가장 성능이 좋은 모델로서 자리 잡았는데, Recurrent 모델의 순차적인 특성은 학습에서 병렬화를 제한하는데 메모리의 제약으로 batch에도 제한이 생겨 sequence의 길이가 길어질수록 큰 문제가 된다. 
- Attention mechanism은 input, output sequence의 길이에 상관없이 dependency를 모델링 해줄 수 있어 sequence modeling이나 transduction model에서 중요한 요소가 되었지만, 대부분 RNN이 함께 사용된다. 이 논문에서는 recurrence를 피하는 대신 input과 output 사이의 global dependecy를 찾는 attention mechanism만 사용하는 Transformer 구조를 제안한다. Transformer는 더 많은 병렬처리가 가능하며 기존의 state-of-the-art보다 높은 성능을 보인다.

## 2. Model Architecture

![Untitled](Attention%20Is%20All%20You%20Need%20372100f683a44b918ddb6786423fd5df/Untitled.png)

                                                          ( Transformer model architecture )

- **Encoder & Decoder**
⇒ Encoder : multi-head self-attention과 position-wise FC feed-forward로 이루어진 layer가 N(6, 12, ... )만큼 연결되어 구성되어 있는데, *residual connection* 기법을 사용하였기 때문에 각 layer의 input과 output vector의 dimension이 동일하도록 설정되어있다.
⇒ Decoder : Encoder에서 Masked Multi Head Attention을 추가적으로 사용하며 N개의 layer로 구성되어 있다. 여기서 *Masking* 기법은 미래의 time step에 존재하는 정보를 이용하지 않고 prediction하게끔 하는 기법이다.
- **Attention**
⇒ Q(query)와 K(key)-V(value) 쌍의 집합을 output에 mapping하는 구조.
⇒ Scaled Dot-Product Attention : Attention(Q, K, V) = softmax(QK.T / d(k).sqrt)V와 같이 나타낼 수 있으며, Q와 K는 동일하게 d(k) 차원을 갖고, V는 d(v)로 d(k)와 동일하지 않은 값이어도 된다. d(k).sqrt로 scaling을 하는 이유는 input vector의 차원이 클 때, scaling을 하지 않으면 softmax에서 값이 큰 index에 의해 gradient값이 매우 작아지는 현상이 일어나기 때문에 scaling을 한다.
⇒ Multi-Head Attention : Scaled Dot-Product Attention을 같은 V, K, Q에 대해 h개 만큼 독립적으로 실행하고 concat한 후 선형변환하여 output을 뽑아내는 기법으로, *각각의 attention이 서로 다른 부분에 집중* 함으로써 더 나은 성능을 보여준다.

![Untitled](Attention%20Is%20All%20You%20Need%20372100f683a44b918ddb6786423fd5df/Untitled%201.png)

- **Position-wise Feed-Forward Networks**
⇒ position(차원?)에 독립적으로, 동등하게 적용되는 fully connected feed-forward network
⇒ input과 output의 차원은 동일하게 유지되지만, FFN 내부의 hidden layer는 input,output의 차원보다 보통 4배 만큼의 크기를 갖는다.
⇒ 선형변환-Relu-선형변환 으로 구성되어 있으며, 아래와 같이 나타낼 수 있다.

![Untitled](Attention%20Is%20All%20You%20Need%20372100f683a44b918ddb6786423fd5df/Untitled%202.png)

- **Embeddings and Softmax**
⇒ d{model}은 embedding된 input vector의 차원을 의미하고, d{k}는 embedding된 vector를 이용할 때, Key의 dimension을 의미한다.
⇒ embedding층들에서는 일반적으로 d{model}.sqrt를 결과에 곱하여 output을 뽑아낸다.
- **Positional Encoding**
⇒ embedding된 vector와 같은 d{model}을 차원으로 갖고있고, 모델이 시퀀스의 순서를 반영 및 사용할 수 있도록 시퀀스 내의 토큰들의 상대적/절대적 위치에 관한 정보들을 주입
⇒ 각 dimension및 position에서의 값은 다음과 같은 함수들에 따라서 값을 갖게 되고, sin&cos 함수를 사용함으로써 항상 unique한 vector를 생성하고 time step간의 거리를 일정하게 유지할 수 있다.

![Untitled](Attention%20Is%20All%20You%20Need%20372100f683a44b918ddb6786423fd5df/Untitled%203.png)

## 2. Model Architecture

## 참조

- 논문 - [https://arxiv.org/abs/1706.03762](https://arxiv.org/abs/1706.03762)
- blog - [https://velog.io/@changdaeoh/Transformer-논문리뷰#abstract](https://velog.io/@changdaeoh/Transformer-%EB%85%BC%EB%AC%B8%EB%A6%AC%EB%B7%B0#abstract)
        - [https://dladustn95.github.io/nlp/Transformer_paper_review/](https://dladustn95.github.io/nlp/Transformer_paper_review/)
- positional encoding - [https://skyjwoo.tistory.com/entry/positional-encoding이란-무엇인가](https://skyjwoo.tistory.com/entry/positional-encoding%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)
 - [https://www.youtube.com/watch?v=dichIcUZfOwhttps://www.youtube.com/watch?v=dichIcUZfOw](https://www.youtube.com/watch?v=dichIcUZfOw)