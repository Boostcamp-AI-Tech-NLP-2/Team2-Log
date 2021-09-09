# Glove

## 논문 채택 이유

⇒ 이전에 리뷰했던 word2vec과 동일하게 word embedding관 관련된 논문을 다루어보고자 하였고, word2vec에서 성능을 향상시키려 한 방법인 Glove 논문을 알게 되어 리뷰하기로 하였음.

## 해결하고자 하는 문제

⇒ skip-gram과 CBoW와 같은 local window 방식의 워드 벡터 표현은 단어의 전역적인 통계를 반영하지 못하는 문제가 존재하고 LSA와 같은 global matrix factorization은 단어간의 의미거리를 제대로 파악하지 못 하는 문제가 존재하는데, 이 두 문제 모두를 해결할 수 있는 방안을 제시.

## 제안하는 방법(Method)

공출현 빈도가 높은 단어의 쌍으로 단어를 정의하지만, 이때 서로 다른 두 word간의 관계성을 제 3의 단어를 이용하여 파악.

## 제안된 방법은 어떤 문제를 풀었는가?(contribution)

word2vec에서 제안된 방법에서 단어의 전역적인 통계를 반영하지 못 하는 문제를 해결함으로써 단어 벡터 표현의 성능을 향상.

### 참조

- Glove 논문 : [https://nlp.stanford.edu/pubs/glove.pdf](https://nlp.stanford.edu/pubs/glove.pdf)
- Glove 논문 리뷰 글 : [https://velog.io/@donggunseo/Glove](https://velog.io/@donggunseo/Glove),  [http://blakha.blogspot.com/2018/09/glove.html](http://blakha.blogspot.com/2018/09/glove.html), [https://dalpo0814.tistory.com/30](https://dalpo0814.tistory.com/30)