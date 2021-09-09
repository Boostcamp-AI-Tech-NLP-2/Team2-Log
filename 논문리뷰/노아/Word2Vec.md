### Paper Review
- 매우 단순한 모형(CBOW, SG)으로도 높은 수준의 word vector 를 학습 시켰으며 이를 syntactic, semantic question 들에 대한 similarity task로 평가하였다.
- Scaling up이 현실적으로 가능하려면 결국 연산 복잡도에 대한 개선이 필요한 상태였으며, 해당 모형을 통해서 그것이 가능해졌다.
- 다양한 NLP task 에 활용될 수 있는 enriched word embedding 방법을 제시하였다.
- CBOW 는 semantic task acc, SG는 syntactic task acc 가 부족하다는 experimental result
  ->  이를 보완할 수 있는 방법이 필요해보임. (context뿐만아니라 문법적인 특성을 capture 할 수 있는 SG 모형?)


### Paper Flow 
1. Motivation
    - LM (NNLM, RNNLM - 예측모형) 계열에서 나타난 continous 한 임베딩 기법은 Neural Network 를 활용하여 성능은 좋지만 computational complexity 에 문제가 있기에 개선된 효율적 구조가 필요해 보인다.
2. Problem Statement
    - Word Vector 에 문맥적인 요소를 반영하면서 더 풍부하게 학습시킬 수 있는지?
3. Methodology
    - CBOW, SG 두 예측 모형을 활용하여 Word Representation 추출
4. Contribution
    - 앞으로 다양한 NLP 태스크에 활용될 수 있는 word vector 제시 + 새로운 word representation 방법에 대한 틀을 닦아놓음
5. Limitation
    - 아직은 syntactic, semantic 이해도가 높지 않은 수치 → 그래서 FastText가 나온걸까?


A lengthy summary of the paper can be found [HERE](https://nlee208.notion.site/Efficient-Estimation-of-Word-Representations-in-Vector-Space-13-dfca5c8c40f7482e812abdf70e3597f5)

