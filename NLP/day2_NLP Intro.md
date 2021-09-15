# day2_NLP Intro

작성자: 정 찬

참고문헌: 딥 러닝을 이용한 자연어 처리 입문(유원준, 안상준), boostcourse 딥러닝을 이용한 자연어 처리(조경현)



## 1. 토큰화Tokenization
- 데이터를 사용하고자하는 용도에 맞게 토큰화tokenization & 정제cleaning & 정규화normalization해야 함.
- 토큰화tokenization: 주어진 코퍼스corpus=단어뭉치에서 토큰token이라 불리는 단위로 나누는 작업.

### 1.1. 단어 토큰화Word Tokenization
- 토큰의 기준을 단어word를 기준으로 하는 경우
- 입력: Time is an illusion. Lunchtime double so!
- 출력 : "Time", "is", "an", "illustion", "Lunchtime", "double", "so"

(띄어쓰기 단위로 자르면 사실상 단어 토큰이 구분되는 영어와 달리, 한국어는 띄어쓰기만으로는 단어 토큰을 구분하기 어렵다.)

- 어퍼스트로피가 들어간 상황에서 Didn't와 Charlie's를 토큰화 하기

- word_tokenize

  ```python
  from nltk.tokenize import word_tokenize
  print(word_tokenize("Just then, Mr. Buchet, Charlie's father, came into the room. But didn't say anything.")
  ```

  ​    `['Just', 'then', ',', 'Mr.', 'Buchet', ',', 'Charlie', "'s", 'father', ',', 'came', 'into', 'the', 'room', '.', 'But', 'did', "n't", 'say', 'anyting', '.']`

  word_tokenize는 Didn't를 Did와 n't로 분리하였으며, 반면 Charlie's는 Charlie와 's로 분리

  - wordPunctTokenizer

    ```python
    from nltk.tokenize import WordPunctTokenizer
    print(word_tokenize("Just then, Mr. Buchet, Charlie's father, came into the room. But didn't say anyting."))```
    ```

    `['Just', 'then', ',', 'Mr.', 'Buchet', ',', 'Charlie', "'s", 'father', ',', 'came', 'into', 'the', 'room', '.', 'But', 'did', "n't", 'say', 'anyting', '.']`

    WordPunctTokenizer는 구두점을 별도로 분류하는 특징을 갖고 있기 때문에, word_tokenize와는 달리 Didn't를 Did과 '와 n't로 분리, 마찬가지로 Charlie's를 Charlie와 's로 분리.

  - keras

    ```python
    from tensorflow.keras.preprocessing.text import text_to_word_sequence
    print(text_to_word_sequence("Just then, Mr. Buchet, Charlie's father, came into the room. But didn't say anyting."))
    ```

    `['just', 'then', 'mr', 'buchet', "charlie's", 'father', 'came', 'into', 'the', 'room', 'but', "didn't", 'say', 'anyting']`

    케라스의 text_to_word_sequence는 기본적으로 모든 알파벳을 소문자로 바꾸면서 마침표나 컴마, 느낌표 등의 구두점을 제거. 하지만 didn't나 charlie's와 같은 경우 어퍼스트로피는 보존.

  

  

  ## 되돌아 보기

  오늘은 간단하게 tokenization이 무엇인지, 모듈별로 어떤 방식으로 작동하는지 학습했다. 어제의 이론적인 내용을 수행하기에 깃헙으로 심신이 망가졌기 때문.

  코사다마 블로그 업로드하는 마크다운 파일, 이미지 파일을 풀리퀘할 때 지정된 위치로 설정해 주지 못해서 에러가 많이 났다. 지정된 저장위치를 사용하고, --- 등을 통해 미리 정해진 슬롯(?)에다가 내용을 넣어주었다. 열심히 교안과 가이드라인을 만든 peniel과 ky를 볼 낯이 없다. 이 블로그도 언젠가는 예쁜 모습으로 탈바꿈할 때가 올텐데! 그때는 덜 고생했으면 좋겠다.

  

  

