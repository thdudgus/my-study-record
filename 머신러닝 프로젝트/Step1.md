[step1, step2 in kaggle](https://www.kaggle.com/code/soyoung27/titanic-test#%EB%A7%A4%EC%9A%B0-%EA%B0%84%EB%8B%A8%ED%95%9C-%EC%98%88%EC%B8%A1-(Baseline-1:-%EB%AA%A8%EB%91%90-%EC%82%AC%EB%A7%9D))
### 매우 간단한 예측 (Baseline 1: 모두 사망)
이 단계의 목표는 모든 승객이 사망했다고 예측하는 가장 단순한 모델을 만들어 제출해보는 것.

##### 제출 파일 만들기
- `gender_submission.csv` 예시 파일처럼 `PassengerId`와 `Survived` 두 개의 열이 필요  
- `Survived` 열의 모든 값을 `0`으로 채워준다.
```python
submission = pd.DataFrame({
    "PassengerId": test_df["PassengerId"],
    "Survived": 0
})
```
##### CSV 파일로 저장
- 만든 제출 파일을 CSV 파일로 저장한다. 이 파일을 Kaggle에 제출하게 된다.  
- `index=False`는 불필요한 행 번호가 저장되지 않도록 하는 중요한 옵션

```python
submission.to_csv('submission_baseline_1.csv', index=False)
```

##### 제출 및 점수 확인
- 노트북 우측 상단의 'Save Version' 또는 'Commit' 버튼을 누른다.  
- 실행이 완료되면, 노트북 결과물 페이지에서 방금 만든 submission_baseline_1.csv 파일을 찾아 'Submit' 버튼을 누른다.  
- 리더보드에서 약 62%의 정확도 점수를 확인할 수 있다.