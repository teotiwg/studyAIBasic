# studyAIBasic
# 학습일지 꺄

# Goal: 이번 프로젝트에서 달성하려고 한 목표

# Top-down Insight: 코드를 먼저 돌려보고 나중에 깨달은 핵심 이론 (예: "아, 여기서 미분이 쓰이는 이유는 오차를 최소화하는 방향을 찾기 위해서였음")

# Troubleshooting: 직면했던 버그와 해결 과정 



📑 Project: Titanic Survival Prediction (Kaggle)
Last Updated: 2026-02-07 Target Score: 0.85 (Current: 0.77511)

1. 전처리 파이프라인 (Data Preprocessing)
데이터의 구멍을 메우고, AI가 이해할 수 있는 언어(숫자)로 변환하는 '재료 손질' 단계.

- 결측치(Imputation) 처리:

    Age: 데이터의 중심 경향성을 유지하기 위해 **중앙값(Median)**으로 채움.

    Embarked: 가장 빈도가 높은 **최빈값(Mode)**으로 채움.

    Fare: 테스트 데이터의 결측치를 훈련 데이터의 중앙값으로 보정.

- 인코딩(Categorical Encoding):

    Sex: {'female': 1, 'male': 0}

    Embarked: {'S': 0, 'C': 1, 'Q': 2} (범주형 데이터를 수치형 데이터로 매핑)


2. 피처 엔지니어링 (Feature Engineering)
단순한 데이터를 조합해 AI에게 더 강력한 힌트를 주는 '인사이트 추출' 단계.

    Title(칭호) 추출: 이름에서 Mr, Miss, Master 등을 정규표현식(r' ([A-Za-z]+)\.')으로 추출. 사회적 지위와 연령대를 동시에 반영하여 로컬 성능 향상(약 +1.1%)에 기여.

    FamilySize: SibSp(형제/배우자) + Parch(부모/자녀) + 1(본인)을 합쳐 가족 규모 산출.

    IsAlone: 가족 없이 혼자 탄 승객인지 여부를 이진값(0, 1)으로 판별.

3. 사용 모델 및 결과 (Modeling & Score)
- 모델: RandomForestClassifier 

- 설정: n_estimators=100 (나무 100그루), max_depth=5 (과적합 방지용 깊이 제한)

로컬 검증(Validation) 점수: 82.68%

캐글 리더보드(Public) 점수: 0.77511

* 복기
에러 디버깅의 가치: NameError, ValueError, KeyError를 겪으며 파이썬의 동적 타이핑 특성과 주피터 노트북의 세션 관리 메커니즘 확인.

데이터 무결성: fillna와 map을 실행할 때마다 데이터의 원본 상태를 체크하는 것이 얼마나 중요한지 확인.

일반화(Generalization)의 어려움: 로컬 점수(82%)와 제출 점수(77%)의 차이 ㅗ
