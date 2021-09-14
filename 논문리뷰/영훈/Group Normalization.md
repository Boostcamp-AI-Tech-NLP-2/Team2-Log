# Group Normalization

## 논문 채택 이유

⇒ NLP강의 수강 중 further reading으로 Group Normalization이 소개되어 리뷰하게 되었음.

## 해결하고자 하는 문제

⇒ Batch Normalization은 batch size를 작게 설정할 경우 성능이 떨어지는 문제있는데, batch size를 작게 설정해야하는 task의 경우 batch 통계값이 전체 분포를 부정확하게 추정하여 성능이 저하되는 문제가 있다.

## 제안하는 방법(Method)

⇒ Normalization을 할 때, batch size의 영향을 받지 않도록 하기 위해 batch 단위로 normalize하는 부분을 없애고, Layer Normalization과 Instance Normalization과 유사하게 채널을 그룹화하여 normalization을 진행.

## 제안된 방법은 어떤 문제를 풀었는가?(contribution)

⇒ batch size가 필연적으로 작게 설정되는 task에서 batch normalization을 사용했을 때, 성능이 저하되는 문제를 채널 단위로 normalization함으로써 해결.

### 참조

- GN 논문 - [https://openaccess.thecvf.com/content_ECCV_2018/papers/Yuxin_Wu_Group_Normalization_ECCV_2018_paper.pdf](https://openaccess.thecvf.com/content_ECCV_2018/papers/Yuxin_Wu_Group_Normalization_ECCV_2018_paper.pdf)
- GN 논문 리뷰 blog - [https://deep-learning-study.tistory.com/726](https://deep-learning-study.tistory.com/726)