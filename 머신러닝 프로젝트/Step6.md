새로운 모델 도입 (Decision Tree, Random Forest, or SVM)

### Random Forest
- 랜덤 포레스트는 여러 개의 작은 결정 트리(Decision Tree)를 결합한 모델
- logistic regression보다 훨씬 복잡하고 비선형적인 관계를 잘 학습
```python
from sklearn.ensemble import RandomForestClassifier

# 1. 랜덤 포레스트 모델 생성
# n_estimators는 만들 나무의 개수, random_state는 재현성을 위함
model_rf = RandomForestClassifier(n_estimators=100, random_state=42)

# 2. 모델 훈련
model_rf.fit(X_train, y_train)

# 3. 예측 및 제출 파일 생성
test_predictions_rf = model_rf.predict(X_test)

submission_rf = pd.DataFrame({
    "PassengerId": test_df["PassengerId"],
    "Survived": test_predictions_rf
})

submission_rf.to_csv('submission_random_forest.csv', index=False)
print("Kaggle 제출 파일 'submission_random_forest.csv'이 생성되었습니다.")
```
**result**
Kaggle 제출 파일 'submission_random_forest.csv'이 생성되었습니다.

=> Logistic Regression과 크게 다르지 않은 정확도...

위 랜덤 포레스틑 default parameter로 작동했다. 
따라서 Hyperparameter을 조정하여 최적의 설정을 찾으면 정확도가 더 향상된다.

**Hyperparameter**
- `n_estimators: 
	숲을 구성하는 tree의 개수 (**많을수록 좋지만 시간 소요**)

- **`max_depth`**:
	각 tree의 최대 깊이. 너무 깊으면 훈련 데이터에만 과적합(overfitting)될 수 있다. **가장 중요한 설정 중 하나이다.**

- **`min_samples_leaf`**: 
	leaf node(가장 끝 node)가 되기 위해 필요한 최소한의 데이터 수. 과적합을 방지하는 데 도움이 됩니다.

##### 직접 튜닝하기
- 아래 코드처럼 몇 가지 다른 설정값으로 모델을 만들어 **검증 데이터(`X_val`)로 성능을 테스트**
- 어떤 설정이 가장 높은 검증 정확도를 보이는지 찾는 것이다.
```python
# --- 1. 다양한 설정으로 모델 여러 개 만들어보기 ---

# 모델 A: tree의 깊이를 5로 제한
model_A = RandomForestClassifier(n_estimators=100, max_depth=5, random_state=42)

# 모델 B: tree의 깊이를 10으로 제한
model_B = RandomForestClassifier(n_estimators=100, max_depth=10, random_state=42)

# 모델 C: leaf node의 최소 샘플 수를 10으로 설정
model_C = RandomForestClassifier(n_estimators=100, min_samples_leaf=10, random_state=42)


# --- 2. 각 모델을 훈련시키고 검증 데이터로 정확도 확인하기 ---

# 모델 A 훈련 및 평가
model_A.fit(X_train_split, y_train_split)
pred_A = model_A.predict(X_val)
acc_A = accuracy_score(y_val, pred_A)
print(f"모델 A (max_depth=5) 검증 정확도: {acc_A:.4f}")

# 모델 B 훈련 및 평가
model_B.fit(X_train_split, y_train_split)
pred_B = model_B.predict(X_val)
acc_B = accuracy_score(y_val, pred_B)
print(f"모델 B (max_depth=10) 검증 정확도: {acc_B:.4f}")

# 모델 C 훈련 및 평가
model_C.fit(X_train_split, y_train_split)
pred_C = model_C.predict(X_val)
acc_C = accuracy_score(y_val, pred_C)
print(f"모델 C (min_samples_leaf=10) 검증 정확도: {acc_C:.4f}")
```
**result**
```text
모델 A (max_depth=5) 검증 정확도: 0.8324
모델 B (max_depth=10) 검증 정확도: 0.8156
모델 C (min_samples_leaf=10) 검증 정확도: 0.8101
```


##### 최종 모델 선택 및 제출
성능이 비슷할 때는, 더 단순한 모델을 선택하는 것이 일반적이다.
(B보다는 A가 더 단순)
```python
# 가장 성능이 좋았던 모델 A의 설정으로 최종 모델 생성
final_model = RandomForestClassifier(n_estimators=100, max_depth=5, random_state=42)

# 전체 훈련 데이터(X_train, y_train)로 최종 모델 훈련
final_model.fit(X_train, y_train)

# 테스트 데이터로 최종 예측
final_predictions = final_model.predict(X_test)

# 제출 파일 생성
submission_final = pd.DataFrame({
    "PassengerId": test_df["PassengerId"],
    "Survived": final_predictions
})

# CSV 파일로 저장
submission_final.to_csv('submission_rf_tuned.csv', index=False)

print("하이퍼파라미터 튜닝이 완료된 최종 제출 파일 'submission_rf_tuned.csv'이 생성되었습니다.")
```

Kaggle에선 A모델의 n_estimators=200로 설정하고 83%로 나왔는데, submit하니까 79%로 감소.

=> 검증 점수(83%)보다 제출 점수(79%)가 낮게 나오는 현상은 머신러닝에서 아주 흔하게 겪는 일.
이 현상을 **과적합(Overfitting)**이라고 부름

###### 과적합(Overfitting)이란?
과적합은 모델이 훈련용 데이터에 너무 '과하게 적합'되어, 마치 정답을 외워버린 학생처럼 행동하는 것을 말한다.
- **훈련 데이터(연습 문제):** 모델이 이 데이터의 패턴뿐만 아니라 아주 사소한 잡음(noise)이나 특징까지 전부 외워버린다.
- **검증 데이터(모의고사):** 연습 문제와 매우 비슷하기 때문에, 외운 실력으로도 높은 점수(83%)를 받는다.
- **테스트 데이터(실제 수능):** 처음 보는 새로운 문제들이 출제되자, 외운 것만으로는 풀 수 없어 점수(79%)가 떨어진다.

==> 파라미터를 조정해보며 정확도를 높여야 함.
===> 해도 크게 달라지지 않아서... SVM 도입해보자...

### SVM (Support Vector Machine)
SVM은 데이터를 좌표 평면 위의 점이라고 생각하고, **생존 그룹과 사망 그룹을 가장 잘 나눌 수 있는 경계선(결정 경계)을 찾는 방식**으로 작동합니다. tree 기반 모델과는 완전히 다른 접근법이다.

- **장점:** 특정 종류의 데이터, 특히 feature가 많은 복잡한 데이터에서 강력한 성능을 보인다.
- **단점:** 데이터의 스케일에 민감해서 feature scaling 전처리 과정이 거의 필수적이다.

SVM은 각 feature들 사이의 거리를 기반으로 동작한다.
만약 'Age' (0~80)처럼 값의 범위가 큰 특성과 'Sex' (0~1)처럼 범위가 작은 특성을 그대로 사용하면, SVM은 범위가 큰 'Age' 특성을 훨씬 더 중요하게 여기는 착각을 하게 된다.
**스케일링**은 모든 특성들의 단위를 맞추는 작업
`StandardScaler`를 사용해 모든 특성들이 비슷한 범위를 갖도록 표준화해 준다.
> 스케일러는 반드시 훈련 데이터(`X_train`)에만 `fit`을 하고, 그 기준으로 테스트 데이터도 변환해야 한다.
```python
from sklearn.preprocessing import StandardScaler

# 1. 스케일러 생성
scaler = StandardScaler()

# 2. 훈련 데이터에 맞게 스케일러를 학습(fit)시키고 변환(transform)
X_train_scaled = scaler.fit_transform(X_train)

# 3. 테스트 데이터는 학습된 스케일러로 변환(transform)만 수행
X_test_scaled = scaler.transform(X_test)

## SVM 모델 훈련
from sklearn.svm import SVC

# 1. SVM 모델 생성
# kernel='rbf'는 비선형 경계선을 찾게 해주는 기본 옵션
# C는 얼마나 많은 오류를 허용할지 정하는 규제 값. 클수록 오류를 덜 허용(과적합 위험)
model_svm = SVC(kernel='rbf', C=1.0, random_state=42)

# 2. 스케일링된 훈련 데이터로 모델 학습
model_svm.fit(X_train_scaled, y_train)
```

훈련된 SVM 모델로 데이터의 생존 여부를 예측하고 제출 파일로 만든다.
```python
# 1. 스케일링된 테스트 데이터로 최종 예측
test_predictions_svm = model_svm.predict(X_test_scaled)

# 2. 제출 파일 생성
submission_svm = pd.DataFrame({
    "PassengerId": test_df["PassengerId"],
    "Survived": test_predictions_svm
})

# 3. CSV 파일로 저장
submission_svm.to_csv('submission_svm.csv', index=False)

print("SVM 모델의 최종 제출 파일 'submission_svm.csv'이 생성되었습니다.")
```

##### SVM의 주요 하이퍼파라미터

1. **`C` (Regularization parameter)**
- **설명:** 모델이 오류를 얼마나 허용할지를 결정하는 "엄격함"을 조절합니다.
- **조정:**
    - **`C` 값이 작으면 (예: 0.1):** 약간의 오류를 너그럽게 봐주면서, 최대한 넓고 단순한 경계선을 찾으려고 합니다. **과적합을 방지**하는 효과가 있다.
    - **`C` 값이 크면 (예: 10, 100):** 오류를 거의 용납하지 않으려고 훈련 데이터 하나하나에 맞춰 복잡하고 구불구불한 경계선을 만든다. **과적합의 위험**이 있습니다.
- **시도해볼 값:** `0.1`, `1`, `10`

2.  **`gamma` (Kernel coefficient)**
- **설명:** 하나의 데이터 포인트가 경계선을 결정하는 데 미치는 "영향력의 범위"를 조절합니다. (`kernel='rbf'`일 때만 의미가 있습니다.)
- **조정:**
    - **`gamma` 값이 작으면 (예: 0.1):** 하나의 데이터가 넓은 영역에 영향을 준다. 경계선이 부드럽고 단순해진다.
    - **`gamma` 값이 크면 (예: 1, 10):** 하나의 데이터가 자기 주변의 좁은 영역에만 영향을 준다. 경계선이 매우 복잡해지며 **과적합의 위험**이 커진다
- **시도해볼 값:** `'scale'`(기본값), `0.1`, `1`

```python
# 먼저, 스케일링된 데이터를 훈련/검증용으로 다시 나눠야 합니다.
X_train_scaled_split, X_val_scaled, y_train_split, y_val = train_test_split(
    X_train_scaled, y_train, test_size=0.2, random_state=42
)

# --- 테스트해볼 모델들 ---
model_svm_A = SVC(C=0.1, random_state=42)
model_svm_B = SVC(C=10, random_state=42)
model_svm_C = SVC(C=1, gamma=0.1, random_state=42)

# --- 모델 A 평가 ---
model_svm_A.fit(X_train_scaled_split, y_train_split)
pred_A = model_svm_A.predict(X_val_scaled)
print(f"모델 A (C=0.1) 검증 정확도: {accuracy_score(y_val, pred_A):.4f}")

# --- 모델 B 평가 ---
model_svm_B.fit(X_train_scaled_split, y_train_split)
pred_B = model_svm_B.predict(X_val_scaled)
print(f"모델 B (C=10) 검증 정확도: {accuracy_score(y_val, pred_B):.4f}")

# --- 모델 C 평가 ---
model_svm_C.fit(X_train_scaled_split, y_train_split)
pred_C = model_svm_C.predict(X_val_scaled)
print(f"모델 C (C=1, gamma=0.1) 검증 정확도: {accuracy_score(y_val, pred_C):.4f}")
```

**최종 모델 훈련 및 제출 파일 생성**
```python
# 가장 성능이 좋았던 C=1, gamma=0.1 설정으로 최종 SVM 모델 생성
final_svm_model = SVC(C=1, gamma=0.1, random_state=42)

# 전체 훈련 데이터(스케일링된)로 모델 훈련
final_svm_model.fit(X_train_scaled, y_train)

# 테스트 데이터(스케일링된)로 최종 예측
final_predictions_svm = final_svm_model.predict(X_test_scaled)

# 제출 파일 생성
submission_final_svm = pd.DataFrame({
    "PassengerId": test_df["PassengerId"],
    "Survived": final_predictions_svm
})

# CSV 파일로 저장
submission_final_svm.to_csv('submission_svm_final_tuned.csv', index=False)

print("최종 튜닝된 SVM 모델의 제출 파일 'submission_svm_final_tuned.csv'이 생성되었습니다.")
```
