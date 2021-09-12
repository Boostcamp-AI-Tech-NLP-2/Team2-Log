## Motivation
vector space representation을 학습하는 최근 방법은 벡터 산술(vector arithmetic)을 사용하여 세분화된(fine-grained) semantic, syntatic regularities를 잡는데 성공했지만 이러한 규칙성의 origin은 아직 불투명하다.

## Problem Statement
현재 자주 쓰이고 있는 모델들의 장단점을 분석하고 이를 모두 해결하려고 시도했습니다.
- Global matrix factorization method : LSA -> sub-optimal vector space structure를 가리키는 word analogy task에 약하다.
- Local context window method : Skip-gram model -> corpus의 통계 정보를 활용하지 못한다.

## Methodology
word-word 동시발생 카운트 정보를 활용하여 weighted least squares model을 제안한다. -> 통계정보를 효율적으로 사용할 수 있다.
또한, word-word 동시발생 matrix에서 0이 아닌 elements들만 연산에 참여시켜 complexity도 줄일 수 있다.
GloVe 모델은 미리 word-word 동시 발생 카운트를 계산해놓고 이를 사용하여 기존 방법론들에 대한 약점을 해결할 수 있다.
### Related work
- Matrix Factorization Methods
- Shallow Window-Based Methods

## Contribution
GloVe 모델은 비지도 학습에서 새로운 log-bilinear regression model이고 다른 모델보다 좋은 성능을 내준다.

## Note
- [Link](https://gelatinous-rat-732.notion.site/GloVe-Global-Vectors-for-Word-Representation-e7673930c7aa48f2a2c9d95e506a31bb)
