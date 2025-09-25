**로지스틱 회귀(Logistic Regression)** 모델을 `scikit-learn` 라이브러리를 이용해 훈련시키기

##### 모델에 사용할 feature 선택하기
- 먼저 Step4에서 만든 feature들 중에서 모델 훈련에 사용할 것들만 선택해야 한다.
- 이름이나 티켓 번호처럼 불필요한 정보는 제외한다.
```python
# 훈련에 사용할 특성 목록 정의
features = ['Pclass', 'Sex', 'Age', 'Embarked', 'FamilySize', 'Title', 'AgeGroup']

# 훈련 데이터(X_train, y_train)와 테스트 데이터(X_test) 준비
X_train = train_df[features]
y_train = train_df['Survived']
X_test = test_df[features]
```

##### 훈련 / 검증 데이터 분리하기
- 모델의 성능을 객관적으로 평가하기 위해, 훈련 데이터를 다시 훈련용 80%,  검ㅁ증용 20%으로 나눈다.
- 이렇게 하면 모델이 Kaggle의 테스트 데이터에서 어느 정도의 성증을 보일지 미리 가늠해볼 수 있다.
```python
from sklearn.model_selection import train_test_split

# test_size=0.2는 20%를 검증용으로 사용하겠다는 의미
# random_state는 코드를 다시 실행해도 항상 똑같이 데이터를 나누기 위한 옵션
X_train_split, X_val, y_train_split, y_val = train_test_split(
    X_train, y_train, test_size=0.2, random_state=42
)
```


##### logistic 회귀 모델 훈련 및 평가
- `scikit-learn` 라이브러리를 사용해 **로지스틱 회귀(Logistic Regression) 모델**을 훈련시키고 검증 데이터로 성능을 평가
```python
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score

# 1. 로지스틱 회귀 모델 생성
model = LogisticRegression(max_iter=1000)

# 2. 모델 훈련 (반드시 분리된 훈련용 데이터로!)
model.fit(X_train_split, y_train_split)

# 3. 검증 데이터로 생존 여부 예측
val_predictions = model.predict(X_val)

# 4. 실제 정답(y_val)과 예측값(val_predictions)을 비교해 정확도 계산
accuracy = accuracy_score(y_val, val_predictions)
print(f"모델의 검증 정확도(Validation Accuracy): {accuracy:.4f}")
```
**result**
`모델의 검증 정확도(Validation Accuracy): 0.7933`

##### Kaggle 제출 파일 생성하기
- 이제 전체 훈련 데이터(x_train, y_train)로 모델을 다시 한 번 훈련시켜 최종 예측 파일을 만든다.
- 더 많은 데이터로 학습하면 모델의 성능이 조금이라도 좋아질 수 있다.
```python
# 1. 전체 훈련 데이터로 모델을 다시 훈련
model.fit(X_train, y_train)

# 2. test.csv 데이터에 대한 최종 예측 수행
test_predictions = model.predict(X_test)

# 3. 제출 형식에 맞게 DataFrame 생성
submission = pd.DataFrame({
    "PassengerId": test_df["PassengerId"],
    "Survived": test_predictions
})

# 4. CSV 파일로 저장
submission.to_csv('submission_logistic_regression.csv', index=False)
print("Kaggle 제출 파일 'submission_logistic_regression.csv'이 생성되었습니다.")
```
**result**
`Kaggle 제출 파일 'submission_logistic_regression.csv'이 생성되었습니다.`
이제 생성된 `submission_logistic_regression.csv` 파일을 Kaggle에 제출하여 리더보드 점수를 확인하고, Step 1, 2의 베이스라인 점수와 비교한다.

=> 약 77%

==> 베이스라인과 거의 점수 차이가 없음.. 
	- 성별 특성이 그만큼 강력하다는 증거
	- 기본 모델 (Logistic Regression)의 한계: 데이터 속의 복잡한 관계 (예: 3등성 남성 중에서도 나이가 어린 아이는 생존율이 높다)를 모두 잡아내지는 못할 수 있다.
	- ==> 새로운 모델 도입 필요