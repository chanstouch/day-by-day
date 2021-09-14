# day1_NLP Intro

작성자: 정 찬

참고문헌: 딥 러닝을 이용한 자연어 처리 입문(유원준, 안상준), boostcourse 딥러닝을 이용한 자연어 처리(조경현)



# 1. 자연어 처리Natural Language Processing

- 자연어(natural language): 일상 생활에서 사용하는 언어
- 자연어 처리(natural language processng): 자연어의 의미를 분석하여 컴퓨터가 처리할 수 있도록 하는 일

자연어 처리는 음성 인식, 내용 요약, 번역, 사용자의 감성 분석, 텍스트 분류 작업(스팸 메일 분류, 뉴스 기사 카테고리 분류), 질의 응답 시스템, 챗봇과 같은 곳에서 사용되는 분야입니다.

## 필요 프레임워크와 라이브러리
### 1. 텐서플로우
- 구글의 머신러닝 오픈소스 라이브러리. 직관적인 머신러닝과 딥러닝

### 2. 케라스
- 딥 러닝 프레임워크인 텐서플로우에 대한 추상화 된 API를 제공. 케라스는 백엔드로 텐서플로우를 사용하며, 좀 더 쉽게 딥 러닝을 사용할 수 있게 해준다.

### 3. 젠심(Gensim)
- 머신 러닝을 사용하여 토픽 모델링과 자연어 처리 등을 수행할 수 있게 해주는 오픈 소스 라이브러리
- 토픽 모델링, Word2Vec 등

### 4. 사이킷런scikit-learn
- 파이썬 머신러닝 라이브러리. 사이킷런을 통해 나이브 베이즈 분류, 서포트 벡터 머신 등 다양한 머신 러닝 모듈을 불러올 수 있다.

### 5. NLTK와 NLTK Data 설치
- 엔엘티케이(NLTK): 자연어 처리를 위한 파이썬 패키지
- 코엔엘파이(KoNLPy): 한국어 자연어 처리를 위한 형태소 분석기 패키지



# Text Classification & Sentence Representation - Supervised Learning

- input: natural language sentence, paragraph
- output: text가 속한 카테고리
- 예시:
  - sentiment analysis감성 분석: 이 리뷰가 긍정인지 부정인지
  - text classification카테고리 분류: 이 블로그 포스팅이 어떤 카테고리에 해당하는지
  - intent classification의도 분류: 이 질문이 ~에 관한 것인지

## 2.1. 어떻게 문장을 컴퓨터 언어로 표현할까?

- 문장은 토큰으로 이루어진다.

- 토큰은 미리 정의된 단어들 중 하나다.

- 토큰은 주관적, 임의적이다. 즉, 토큰을 나누는 기준은 다양하다. -> 강아지가 강아지인 이유는 없음. 임의적.

  - 공백
  - 형태소
  - 어절
  - 비트 숫자

  1. **미리 주어진 단어들의 집합인 vocabulary를 만들고, 중복되지 않는 인덱스로 만든다**. 이때, 인덱스도 주관적, 임의적. -> 강아지가 0번이고, 고양이가 1번인 이유가 있는건 아님.
  2. **정수형 인덱스 또한 원래 단어와 임의적으로 인코딩한다**. -> one-hot-encoding 등
     - one-hot-encoding: 이진binary vector로 만듦. 해당하는 것만 1, 나머지는 0인 벡터 집합이 됨.
  3. **텍스트 분류를 위해서는 토큰의 의미가 나와야 한다.** 개, 늑대가 비슷하고, 고양이, 호랑이가 비슷해야 한다. 뉴럴넷이 이 의미를 잡아낼 수 있도록 각 토큰마다 continuous vector spaces 부여 -> **Embedding**
     - **embedding**: **각** **토큰을 연속 벡터 공간continuous vector space에 투영**한다.
     - 조금 움직이는 것은 비슷하고, 많이 움직이는 것은 비슷하지 않다고 판단.
     - 뉴럴넷이 각 토큰(one-hot-vector)마다 벡터를 갖고 있는데, 해당하는(1로 표시된) col, row를 뽑아낸다. 
     - **Table Look Up**: 각 one hot encoding 된 토큰에게 벡터를 부여하는 과정. 실질적으로 one hot encoding 벡터( *x* )와 연속 벡터 공간( *W* )을 내적 한 것. 토큰에 대한 의미를 가진 벡터를 찾는 작업.
     - Table Look Up 과정을 거친후 모든 문장 토큰은 연속적이고 높은 차원의 벡터로 변함.
     - 첫번째 노드를 지나면 문장은 sequence of vector가 됨. 벡터는 토큰의 의미를 가짐. 뉴럴넷 계산을 지나면 벡터 사이즈는 카테고리 개수와 같고, 이를 소프트맥스에 넣으면 distribution이 나온다. 투입된 문장이 어떻게 카테고리화 될지 확률이 나온다. 마지막에 input의 representation이 나온다. 
     - 문장처럼 계속 벡터 길이가 변하면 어떻게 의미를 가진 벡터를 찾을 수 있을까?



## 되돌아 보기

1. table look up에 대해 이해하지 못했다.
2. 부스트코스 강의 지도학습 내용을 건너 띄고 바로 텍스트 분류로 넘어왔기 때문일 수도 있다. 내일은 [지도학습](https://www.boostcourse.org/ai331/joinLectures/195051?isDesc=false)부터 공부해야겠다.
3. '딥 러닝을 이용한 자연어 처리 입문'은 굉장히 친절하게 설명해 주었지만 깊은 이해를 도와주지는 못했다. 반면 부스트코스 강의는 모르는 내용이 많아서 찾아보면서 학습해야할 것 같다.
4. 스터디 분량: 하루에 하나의 주제를 다 학습하기는 무리일 것 같다. 롱런하기 위해 2일에 하나로 설정하고, 쉬는 날에는 하루에 하나의 주제를 학습하자.
