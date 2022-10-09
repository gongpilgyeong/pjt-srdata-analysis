# EA포털 기능 개선을 위한 Service Requests 키워드분석

---

## Project
- TITLE: NIA 정보화사업 성과관리 (2022.05-2022.12)
- CONTENTS: TF-IDF/Logistic Regression 활용 Document similarity & Q&A(SR) Analysis

## Review

#### 1. 프로젝트 내용
- 특정 조건에 해당하는 정보화사업은 '사전협의' 절차를 거쳐야 하는데, 업무처리 절치 과정 중 EA포털 시스템상 권한/기능 등 한계로 인하여 업무 요청(Service Request)을 통해 해결해야만 하는 업무가 존재
- Service Requests (SR) 게시판에서 raw data를 추출하여 분석 시작

#### 2. Preprocessing
- raw data에서 분석에 필요한 key값 역할을 하는 질문고유번호(id), 제목(title), 요청내용(content), 처리내용(action) 내용만 남기고 Cleansing 처리
- Domain 특성상 위 주요 성분에서 outlier 값이 있더라도, 의미있는 정보로 판단하여 특별한 작업을 수행하진 않음
- '요청내용(content)'를 기준으로 시스템상 한계로 인한 업무요청인지 여부(system)를 '라벨링(Labeling)=1,0' 작업

#### 3. Modeling
- 종속변수(system), 독립변수(content) 설정
- 시스템에 영향을 미친 업무의 키워드(content)를 분류하여 의미상 중요한 키워드를 분석하기 위한 것이므로, Logistic Regression Model을 활용함
- Text Mining의 similarity 측저에 가장 성능이 좋아 많이 사용되는 TF-IDF index를 활용함

#### 4. Insight
- SR data에 대한 키워드 분석 결과, 사용자의 시스템 관련 서비스요청 중 **'요청', '수정', '변경', '삭제', '등록'**에 관한 내용이 많고 중요한 의미를 갖는다는 점을 발굴함
- 해당 키워드가 포함된 Service Requests 내용을 살펴본 결과, 단순한 자료나 사업내용에 대한 수정, 변경 등 요청이 약 90% 이상으로 나타남

#### 5. Solution
- Domain 특성상 아무런 제약없이 자료를 수정, 변경하면 안 된다는 점을 고려함
- 현재 Service Requests에 글을 남기는 것으로 시작하여 여러 담당자의 확인 절차가 필요하고, 실제 변경을 서버운영자만이 할 수 있다는 Pain Point를 발굴
- 각 사용자가 직접 자료에 대한 요청을 하고, 해당 담당자가 확인하여 승인하는 방법을 설계하여 시스템 개선을 위한 **'기능요구사항(SFR-xxx)'**를 **도출**
