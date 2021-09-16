## Motivation
Attention weight와 Output 간의 Relatioship에 대해 의심된다. 즉, Explanable하지 않다.

## Problem Statement
Attention Distribution이 신뢰할 수 있는 explanation을 준다고 가정하면 다음과 같은 조건을 만족해야 한다고 가정한다.
  - Attention weights는 feature impotance measure들과 correlate해야 한다.
  - Alternative(or Counterfactual) attention weights configuaration은 예측에 대응하는 변화를 출력해야 한다.


## Methodoloby
Original Attention Distribution과 Adversarial Attention Distribution을 생성하여 같은 입력일 때 결과를 비교하는 방법을 사용했다.  
Adversarial attention distribution을 만드는 방법은 다음과 같다.
  - Original Attention weights를 무작위로 섞는다.
  - 원래의 결과와 반대로 내놓는 adversarial distribution을 직접 생성한다.

Output Distribution의 변화를 측정할 때는 Total Variation Distance(TVD)를 사용하고 두 Attention Distribution의 차이를 측정할 때는 Jensen-Shannon Divergence(JSD)를 사용한다.

## Contribution
Original Attention Distribution과 Adversarial Attention Distribution의 결과가 같다.  
혹은 output의 차이가 없어도 distribution의 차이가 있는 경우도 존재한다.  
따라서, Attention Distribution에 대해 의심해봐야 한다.

## Note
- [Link](https://gelatinous-rat-732.notion.site/Attention-is-not-Explanation-e89a8e67da9447b1b3f19ec47aac5a96)
