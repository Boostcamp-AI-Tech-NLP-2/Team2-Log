## Efficient Estimation of Word Representations in Vector Space (Word2Vec)

- Task

  - introducing continuous word vector that can be trained from very large data set with light model structures

- Problem

  - Previously in word embedding, the popular methods were N-gram and NNLM. However, these methods were computationally expensive for training.

- Methodology

  - CBOW:

    - Similar to NNLM, but removed hidden layer and the projection layer is shared for all words.

    - Use future words

    - predicts current word based on the context

  - Skip-gram:

    - predicts surrounding words given the current words

    - use each current word as an input to a log-linear classifier with continuous projection layer

    - increasing the range improves the quality but also increases computational complexity


- Contribution

  - The relationship between words can be represented by simple algerbric operations with the vector representation of words.

  - Words can be trained into high dimensional word vectors on a large amount of data which can answer very subtle sementic realtionship between words.


- Personal Review

  - 처음 보는 용어, 기술들이 많아서 이해 하기 어려웠다.

  - 논문만 보는 것보다는 논문을 구현한 코드와 같이 봐야 이해가 될 것 같다. 
