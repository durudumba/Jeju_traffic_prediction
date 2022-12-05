## 제주도 도로 교통량 예측 AI 경진대회

1. **대회정보** : [DACON](https://dacon.io/competitions/official/235985/overview/description)

2. **개요** : 날짜, 시간, 교통 및 도로구간 및 정보들을 활용해 도로의 평균 차량 속도 예측

3. **과정**

   - EDA

     EDA.ipynb

   - Feature Engineering

     1. 학습에 불필요한 / 의미가 없는 / 중복적인 의미를 가진 데이터 제거

        → [id, road_name(str), vehicle_restricted, height_restricted, start_node_name, start_longitude, end_node_name, end_latitude]

        start_longitude-end_longitude, start_latitude-end_latitude간의 상관관계가 매우 높아 교차로 하나씩만 사용

     2. 범주화

        → [road_rating, lane_count, road_type]

        수치로 표현되었지만 고유값 갯수가 적은 데이터 범주화

     3. 타입 변환

        → [maximum_speed_limit, weight_restricted]

        모든 데이터 소수아래 값이 0이므로 정수화

     4. 기타

        → [start_turn_restricted, end_turn_restircted, day_of_week]

        start_turn_restricted와 end_turn_restricted의 경우의 수가 4개이므로 범주화해서 병합

        요일은 평일과 휴일로 이진화

   - HyperParameter Tuning

     Optuna 사용

     AIBoo님의 [신용카드 사용자 연체 예측 AI 경진대회 [Private 8위 0.66203] | TYKIM | Catboost](https://dacon.io/competitions/official/235713/codeshare/2750?page=1&dtype=recent)를 참고

   - Modeling & Submit

     과적합 방지를 위해 학습데이터 : 검증데이터(0.2)로 분할

     CatBoost를 이용하여 모델링 및 결과제출

   

4. **결과 및 후기**

   MAE : 3.31396(128th)

   kFold, NN, Stacking 기법을 사용해보고 파라미터를 계속 수정하면서 진행했는데 과적합을 해결할 수 없었다. 또한, 자원의 한계로 Optuna, Stacking 등의 기법에서 많은 시도를 해보지 못했다는 점에 아쉬움이 남는다.

