1. 이 데이터는 무엇을 위해 만들어졌나요?

이 데이터셋은 스마트폰 센서로 사람의 활동을 자동으로 인식(HAR, Human Activity Recognition) 하기 위해 만들어졌습니다.
사람이 다음 6가지 행동을 할 때 스마트폰이 감지한 가속도 + 자이로스코프 신호를 분석하여 “지금 어떤 활동인가?”를 분류하는 데 사용됩니다.

**6가지 활동(class)**

걷기 (WALKING)

계단 오르기 (WALKING_UPSTAIRS)

계단 내려가기 (WALKING_DOWNSTAIRS)

앉기 (SITTING)

서 있기 (STANDING)

누워 있기 (LAYING)

2. 실험은 어떻게 진행되었나요?

참여자: 19~48세 사이의 성인 30명

센서 위치: 허리(벨트)에 고정한 스마트폰(갤럭시 S2)

수집 데이터:

가속도(accelerometer) – 3축 (X, Y, Z)

자이로스코프(gyro) – 3축 (X, Y, Z)

샘플링 속도: 50Hz (초당 50회 측정)

라벨링: 실험 장면을 영상 촬영하여 사람이 수작업으로 활동 레이블을 부여

데이터 분리 방식:

참가자 30명 중 70% → 학습(train)

나머지 30% → 테스트(test)

즉, 사람 단위로 분리된 데이터셋입니다.

3. 원시센서(raw signal)는 그대로 쓰나요?

아니요! 데이터셋은 전처리가 많이 되어 있습니다.

📌 전처리 과정 요약

노이즈 필터 적용

데이터를 2.56초 길이의 슬라이딩 윈도우로 자름

각 윈도우는 128개의 연속 측정값 포함

50% overlap (앞 샘플과 절반 겹침)

가속도에서 중력(gravity)와 신체 움직임(body motion)을 분리

각 윈도우에서 561개의 통계적 특징(feature) 을 추출

시간 도메인(time domain) 특징

주파수 도메인(frequency domain) 특징

그래서 X_train.txt 파일에는 561개의 가공된 피처가 이미 만들어져 있습니다.

4. 한 개의 샘플(record)에 포함된 정보는?

각 행(샘플)은 다음 정보를 포함합니다:

정규화된 561개의 센서 기반 feature

해당 샘플의 활동(Activity) 레이블 (1~6)

샘플을 수집한 참여자의 ID

즉,

한 사람(Subject)이 특정 시간구간(Window) 동안 한 행동(Activity)을
561개의 수치(feature)로 표현한 데이터

5. 데이터셋 구성 파일 설명
📁 최상위 파일
파일명	설명
README.txt	데이터셋 설명 문서
features.txt	561개의 feature 이름 목록
features_info.txt	각 feature가 의미하는 수학적 계산 설명
activity_labels.txt	1~6 → 행동 이름 매핑
📁 train 폴더
파일명	설명
X_train.txt	학습용 feature (N × 561)
y_train.txt	학습용 라벨 (N × 1)
subject_train.txt	누구(참여자)가 수행한 샘플인지 ID (1~30)
Inertial Signals/	원본에 가까운 시계열 데이터 (128개짜리 벡터)

Inertial Signals 폴더에는 다음 같은 파일이 있음:

total_acc_x_train.txt

total_acc_y_train.txt

total_acc_z_train.txt

body_acc_x_train.txt

body_gyro_x_train.txt
(각각 128개의 raw 시계열을 담고 있음)

이 폴더는 “원본 센서 시계열”이고
X_train.txt는 “전처리된 특징(feature)”입니다.

📁 test 폴더

train과 동일한 구조의 테스트 세트.

6. 데이터 단위·범위

가속도: 중력 가속도 g(9.80665 m/s²) 기준

자이로: rad/sec

561개 feature는 모두 [-1, 1] 범위로 정규화됨

7. 이 데이터셋을 사용할 때 참고해야 하는 점

연구 목적–비상업적 사용 권장

논문이나 프로젝트에 사용할 경우 README에 적힌 2013 ESANN 논문을 인용해야 함