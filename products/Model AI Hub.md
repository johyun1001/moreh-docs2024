# Moreh AI Model Hub 


**Moreh AI Model Hub(MAMH)는 무엇인가요?**

Moreh AI Model Hub는 텍스트 및 이미지를 생성하고 언어를 번역하며 다양한 종류의 창의적인 콘텐츠를 작성하는 등의 작업을 하는 도구입니다. 

**MAMH**의 목표는 AMD GPU만으로도 학습이 가능한 AI 모델을 사용하고 공유하는 과정을 단순화하고 개선하는 것입니다. 이 서비스는 다음 목적을 충족하기 위해 탄생하였습니다:

1. **모델 검색 및 선택의 용이성**: Model Hub는 하드웨어 자원 및 시간 대비 학습 성능이 좋은 대규모 생성형 AI 모델을 검색하고 선택하는 과정을 단순화합니다. 사용자는 원하는 기능 및 작업에 적합한 모델을 쉽게 찾을 수 있습니다.
2. **공동 작업 및 공유**: 모델 허브는 사용자 간에 AI 모델을 공동으로 작업하고 공유하는 데 편리한 방법을 제공합니다. 모델을 만들고 수정한 후 다른 사용자와 공유하거나 공동 작업할 수 있습니다. (To Be Determined)

**Moreh AI Model Hub(MAMH) 작동 방식**

**Moreh AI Model Hub**는 대규모 모델을 종합적으로 제공하는 서비스로, 언어뿐만 아니라 이미지 생성 및 모델 비교와 같은 다양한 작업을 수행합니다.
s
1. **Text Generate AI**
    - Chatbot_Small, Chatbot_Medium, Chatbot_Large: 챗봇의 명칭은 사용된 언어 모델의 크기에 따라 구분되었습니다. 3개의 챗봇 모두 대형 언어 데이터를 기반으로 문맥을 이해하고 문장을 생성하며 다양한 주제에 대한 정보 제공, 질문 응답, 일상 대화를 통해 사용자와 상호작용합니다.
    - Code Generator: 사용자가 지정한 규칙 및 요구 사항에 따라, 프로그래밍 코드를 자동으로 생성하여 제공합니다.
        - Generate code: 사용자가 작성한 주석을 수행하는 코드 작성합니다.
        - Explain code: 사용자가 입력한 코드가 어떻게 작동하는지 설명합니다.
        - Debugging: 입력한 함수를 디버깅 가능한 test case를 작성합니다.
2. **Image Generate AI**
    - Text to Image: 텍스트 입력을 기반으로 시각적 콘텐츠를 생성합니다.
    - Random Image: 무작위로 선택된 이미지를 제공하는데, 일반적으로 사용자의 요청에 따라 랜덤하게 이미지를 생성합니다.
3. **Multi Modal AI**
    - Text to Image Editing: 사용자가 입력한 텍스트 설명에 따라 이미지를 편집합니다.
    - Visual Question Answering: 이미지와 관련된 질문에 대답하는 기능을 제공합니다. 사용자가 이미지에 대한 질문을 하면, VQA는 이미지를 분석하고 자연어 처리 기술을 활용하여 해당 질문에 대한 응답을 생성하여 제공합니다.
4. **Compare Model**
    - Chatbot Comparison: 동일한 모델에 대한 파라미터 별 학습 시간 및 생성된 답변의 질을 비교하여 각 모델의 성능 차이를 비교할 수 있습니다.

# 2. **Moreh AI Model Hub(MAMH) 사용 방법**

좌측 Navigation바에서 MAMH에서 제공하는 모델중 하나를 선택합니다.

![Screenshot 2023-12-12 at 2.21.56 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/59a50975-2c9c-4aae-9f9b-5eafac2881b4/07c5721e-3a0c-435f-9a6c-d10c873f8421/Screenshot_2023-12-12_at_2.21.56_PM.png)

1. **Text Generate AI**
    - Chatbot_Small
    - Chatbot_Medium
    - Chatbot_Large
    - Code Generator
2. **Image Generate AI**
    - Text to Image
    - Random Image
3. **Multi Modal AI**
    - Text to Image Editing
    - Visual Question Answering
4. **Compare Model**
    - Chatbot Comparison

## 1. **Text Generate AI**

### Chatbot (Small, Medium, Large)

하단 Textbox에 프롬프트를 입력하면 MAMH가 학습한 정보를 사용하여 답변을 제공합니다.

다음은 한글/영어 특화 언어 모델을 사용한 Chatbot_Small, Chatbot_Medium, Chatbot_Large에서 시도해 볼 수 있는 몇 가지 **프롬프트 예시**입니다.

(한글 프롬프트 예시)

- “닭이 먼저야, 달걀이 먼저야?”
- “특정 사회 문제를 다루는 비영리 단체를 위한 홍보 캠페인을 계획해줘.”
- “단편 소설의 제목을 브레인스토밍하는 데 도움을 줘.”

(영문 프롬프트 예시)

- Tell me the best places to travel on a budget of $1000 including car hire, flights and accommodation.
- Write a summary of “The catcher in the rye”
- Write me a step-by-step guide to use “AI Model Hub”
- Generate a list of at least 10 keywords related to Mother nature

### Code Generator

다음은 Code Generator에서 시도해 볼 수 있는 프롬프트 예시입니다.

(영문 프롬프트 예시)

- Train a logistic regression model, predict the labels on the test set and compute the accuracy score
    
    ```python
    X_train, y_train, X_test, y_test = train_test_split(X, y, test_size=0.1)
    ```
    
- Continue writing this code in Python
    
    ```python
    #function that determines if a year is a leap year or not
    def is_leap_year(year):
        if year % 4 == 0:
            if year % 100 == 0:
    ```
    
- Generate a function ***to find the value for (a+b)^3 using lambda.***
- Generate a Docker script to create a linux machine that has python 3.11.7
installed with following libraries: Pytorch, Tensorflow, Scikit- learn, pandas, numpy.
- Generate a unit test for a function that determines if a year is a leap year or not.

(한글 프롬프트 예시)

- lambda를 사용하여 (a+b)^3의 값을 찾는 함수를 작성해봐.
- 배열을 인수로 받아 가장 큰 값을 반환하는 함수(함수 이름: findMax) 를 작성해줘.
- 파이썬 3.11.7이 설치된 Linux 머신을 생성하기 위한 도커 스크립트를 짜줘.

## 2. Image Generation

### Text to Image

다음은 Text to Image 에서 시도해 볼 수 있는 프롬프트 예시입니다.

- A creative composition of a frog wearing a crown sitting on a log
- A 3D rendering of a chair that’s round and red
- An illustration of a river winding through a meadow
- A photograph of a person sitting on a bench facing the sunset in the style of Van Gogh

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/59a50975-2c9c-4aae-9f9b-5eafac2881b4/6ad53bf3-e625-43b1-8e1a-4b71625bd083/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/59a50975-2c9c-4aae-9f9b-5eafac2881b4/df078766-a94d-44c5-bf6c-57a6931c5e5a/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/59a50975-2c9c-4aae-9f9b-5eafac2881b4/60d7529f-98c0-4bc0-b4f6-a95e6feef9bf/Untitled.png)

![Screenshot 2023-12-12 at 4.20.16 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/59a50975-2c9c-4aae-9f9b-5eafac2881b4/7afdedf6-6620-4a40-9370-87bb714f1ae0/Screenshot_2023-12-12_at_4.20.16_PM.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/59a50975-2c9c-4aae-9f9b-5eafac2881b4/92971576-dbae-423e-9c83-e5db7401d0ce/Untitled.png)

---

# 3. Model Description

### 예시: Chatbot_Small

- Modality(모델 타입): Text to Text
- Training Resource(사용한 GPU 자원): AMD MI250 8 GPU
- Training Time(학습 소요 시간)
- Model Size: 30B - 35B

---

## 3. **서비스 이용 및 개인정보 사용 정책**

### Moreh AI Model Hub 콘텐츠 사용 약관

**차별적이거나 공격적인 이미지를 생성하거나 업로드하지 마십시오.**

- 악의적이고 공격적인 내용을 담은 콘텐츠
- 혐오를 조장하거나 부추기는 콘텐츠
- 폭력, 자해를 조장하는 내용을 담은 콘텐츠
- 개인을 조롱하거나 위협하거나 괴롭히는 내용을 담은 콘텐츠
- 특정 집단과 비교하거나 정체성을 기반으로 증오를 표현하거나 조장하는 콘텐츠

**AI 생성물에 대해 현혹시키지 마십시오.**

- Model Hub에서 생성된 콘텐츠를 공유할 때 AI가 작업에 관여한 내용을 투명하게 공개하는 것이 좋습니다.
- 원하는 경우 Moreh hub 워터마크를 제거할 수 있지만 저작물의 성격에 대해 다른 사람을 오도해서는 안 됩니다. 예를 들어, 해당 작품이 전적으로 인간이 제작한 작품이거나 실제 사건을 그대로 촬영한 사진이라고 해서는 안 됩니다.

**타인의 권리를 존중하세요.**

- 동의 없이 타인의 이미지를 업로드하지 마세요.
- 적절한 사용 권한이 없는 이미지는 업로드하지 마세요.

### 개인정보 처리 방침

(주)모레 Moreh(이하 "회사"라 함)은 개인정보 보호법, 통신비밀보호법, 전기통신사업법, 정보통신망 이용촉진 및 정보보호 등에 관한 법률 등 정보통신서비스제공자가 준수하여야 할 관련 법령상의 개인정보보호 규정을 준수하며, 관련 법령에 의거한 개인정보 처리방침을 정하여 이용자 권익 보호에 최선을 다하고 있습니다.

### 1. 개인정보의 수집 및 이용목적

개인정보는 생존하는 개인에 관한 정보로서 서비스 이용자를 식별할 수 있는 정보(당해 정보만으로는 특정 개인을 식별할 수 없더라도 다른 정보와 용이하게 결합하여 식별할 수 있는 것을 포함)를 말합니다. Moreh가 수집한 개인정보는 다음의 목적을 위하여 활용하고 있으며, 다음의 목적 이외의 용도로는 이용하지 않습니다.

- Moreh Hub에서 이용자 간 주고받은 대화 기록: Moreh Hub에서 귀하가 입력한 내용을 처리하여 적절한 답변과 콘텐츠를 제공하고 이용자에게 맞춤화된 콘텐츠(메시지, 이미지, 오디오 등을 포함)를 제공하는 기본 기능을 제공하기 위해 개인정보를 활용합니다.
- 브라우징 환경을 모니터링하기 위한 쿠키 및 접속 로그
    - 쿠키 사용을 허용하는 경우 사용자 개인 정보가 명시된 용도로 저장됩니다.

### 2. **개인정보 보유 및 이용기간**

이용자의 개인정보와 가명정보는 원칙적으로 개인정보와 가명정보의 수집 및 이용목적이 달성되면 지체 없이 파기합니다. 단, 다음의 정보에 대해서는 명시한 기간 동안 보존합니다.

- 방문에 관한 기록 및 쿠키
    - 보존 이유 : 통신비밀보호법
    - 보존 기간 : 3개월
- Moreh Hub에서 이용자 간 주고받은 대화 기록
    - 보존 이유: 사용자 경험 향상 및 서비스 성능 고도화 연구를 위한 한시적 보유
    - 보존 기간: 연구 목적 달성 시까지

---

## 4. FAQ

**Q. Moreh Hub는 내 개인 데이터를 어떻게 사용하나요?**

A. Moreh Hub가 제공하는 대형 AI 모델은 공개적으로 사용 가능한 콘텐츠, 라이센스가 있는 콘텐츠, 검토자가 생성한 콘텐츠를 포함하는 광범위한 텍스트 및 이미지를 학습합니다. Moreh는 서비스 판매, 광고 또는 사람들의 프로필 등을 생성하기 위해 데이터를 사용하지 않습니다. Moreh Hub가 제공하는 모델의 답변의 질을 높이고 사람들에게 더 유용하게 만들기 위해서만 채팅 데이터를 사용합니다.

**Q. Moreh Hub로 만들어진 이미지나 텍스트를 팔 수 있나요?**

A. [콘텐츠 사용 약관](https://www.notion.so/Moreh-AI-Model-Hub-338f22816df643099046c7342184003f?pvs=21)과 **개인정보 보유 및 이용기간**에 따라 Moreh Hub로 생성된 이미지는 사용자에게 해당 이미지를 재인쇄, 판매 및 상품화할 권리가 있습니다.

**Q. Moreh Hub는 몇개의 언어를 지원하나요?**

A. 현재 Moreh Hub는 한국어, 영어 등의 언어로 제공됩니다. 사용자의 국가, 지역, 언어에 따라 일부 기능이 지원되지 않을 수 있으나 향후 기능 지원 범위를 넓혀 나갈 예정입니다.

**Q. Moreh Hub를 사용할 때 어떤 서비스 약관이 적용되나요?** 

A. Moreh Hub의 AI 모델 사용시에는 Moreh AI Model Hub 콘텐츠 사용 약관 및 [OpenAI](https://openai.com/policies/terms-of-use) 서비스 약관이 적용됩니다.

Moreh AI Model Hub ****서비스 관련 더 자세한 정보에 관한 질문이나 문의사항이 있으시면 [contact@moreh.io](https://www.notion.so/docs-moreh-io-cadaf37e9e2e4b94a680902591f67927?pvs=21)로 문의 부탁드립니다.