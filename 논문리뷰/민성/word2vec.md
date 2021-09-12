## Motivation

기존 NNLM의 training cost가 expensive하기 때문에 적은 cost로 높은 accuracy를 낼 수 있는 모델을 만들려고 했습니다.

## Problem Statement

기존 모델에서의 training complexity를 줄이는 것을 문제로 정의하고 NNLM 모델에서 어느 부분이 complexity를 유발하는지 확인했습니다.

- 대부분의 complexity는 Non-linear hidden layer에서 발생

또한 모델이 얼마나 단어를 잘 분류할 수 있는 방법을 찾으려고 했습니다.

## Methodology

연구진은 CBoW, Skip-gram 두 가지 모델을 제안했습니다.

먼저, Continuous Bag-of-Words(CBoW)모델은 NNLM과 크게 다르지 않지만 Non-linear hidden layer는 제거되고 Projection layer는 모든 단어에 대해 공유되도록 설계했습니다.

다음, Skip-gram 모델은 중심단어(center)를 기준으로 특정 range안에 어떤 단어가 나올 지 예측하는 모델입니다. range가 증가할 수록 word vector의 퀄리티가 증가하지만 동시에 complexity또한 증가합니다.

## Contribution

두 모델은 NNLM에서 많은 complexity를 차지하는 Non-linear hidden layer를 제거함으로써 complexity를 대폭 줄일 수 있는 모델입니다. 또한, 높은 퀄리티의 word embedding vector를 얻을 수 있어 기존 NLP 모델 개선에 도움이 될 수 있습니다.

## Limitation

중의적인 표현과 같이 하나의 단어가 여러 의미를 가지게 되는 경우 더 많은 relationhsip을 표현하는 vector들이 학습에 필요할 것

## Note
- [Link](https://gelatinous-rat-732.notion.site/Efficient-Estimation-of-Word-Representations-in-Vector-Space-e5f9c749c38d4a44aab45977c7a2c88c)
