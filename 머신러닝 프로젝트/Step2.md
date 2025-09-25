### 간단한 규칙 기반 예측 (Baseline 2: 성별)

조금 더 발전시켜, '여성은 생존, 남성은 사망'이라는 규칙으로 예측 파일을 만들어본다.
##### 규칙 적용하기
- test.csv의 'Sex'을 기준으로 'female'이면 1(생존), 'male'이면 0(사망)을 예측하는 Sruvived 열을 만든다.
```python
# 방법 1: .apply와 lambda 함수 사용
submission['Survived'] = test_df['Sex'].apply(lambda x: 1 if x == 'female' else 0)

# 방법 2: 더 간단한 방법
submission['Survived'] = (test_df['Sex'] == 'female').astype(int)
```

##### CSV 파일로 저장
- 위와 동일하게 이번에는 다른 이름으로 파일을 저장.
```python
submission.to_csv('submission_baseline_2.csv', index=False)
```

##### 제출 및 점수 확인
- 다시 노트북을 저장/커밋 후 새로 만든 파일을 제출한다.  
- 약 76%로 점수가 크게 오르는 것을 확인할 수 있다.
