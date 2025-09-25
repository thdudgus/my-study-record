### Feature Engineering
- EDA에서 발견한 단서를 바탕으로, 기존 데이터를 가공하거나 조합해 모델의 예측 성능을 높여줄 새로운 feature를 만드는 것.

##### 데이터클리닝: Age 결축치 채우기
- Age에 비어있는 값을 train_df의 중간값(median)으로 채워보았다.
- mean보다 중간값이 극단적인 값의 영향을 덜 받아서 더 안정적일 수 있다.
```python
test_df = pd.read_csv("/kaggle/input/titanic/test.csv")

# 1. 훈련 데이터에서 'Age'의 중간값 계산
age_median = train_df['Age'].median()

# 2. train_df와 test_df 양쪽 모두의 결측치를 위에서 계산한 중간값으로 채우기
train_df['Age'].fillna(age_median, inplace=True)
test_df['Age'].fillna(age_median, inplace=True)

print(f"Age의 비어있는 값들을 중간값인 {age_median}(으)로 채웠습니다.")
```
**result**
`Age의 비어있는 값들을 중간값인 28.0(으)로 채웠습니다.`

##### 데이터 변환: Sex, Embarked 숫자 만들기
- 문자로 된 범주형 데이터를 모델이 이해할 수 있는 숫자로 바꿔준다.

**성별 변환**
- 남성은 0, 여성은 1로 변경
```python
# .map() 함수를 이용해 문자를 숫자로 변환
train_df['Sex'] = train_df['Sex'].map({'male': 0, 'female': 1})
test_df['Sex'] = test_df['Sex'].map({'male': 0, 'female': 1})
```

**Embarked(탑승 항구) 변환**
- Embarked는 비어있는 값이 약간 있으므로, 가장 많이 등장하는 값으로 채운 뒤 숫자로 변경.
```python
# 1. 가장 흔한 탑승 항구 찾기 (훈련 데이터 기준)
embarked_mode = train_df['Embarked'].mode()[0]

# 2. 비어있는 값을 가장 흔한 값으로 채우기
train_df['Embarked'].fillna(embarked_mode, inplace=True)
test_df['Embarked'].fillna(embarked_mode, inplace=True)

# 3. 각 항구를 숫자로 변환
train_df['Embarked'] = train_df['Embarked'].map({'S': 0, 'C': 1, 'Q': 2})
test_df['Embarked'] = test_df['Embarked'].map({'S': 0, 'C': 1, 'Q': 2})
```


##### new feature 만들기
- 과제 안내 파일에서 제안된 새로운 특성들을 만들어보자

**family size 생성**
- `SibSp` (형제/배우자 수)와 `ParCh` (부모/자녀 수)를 더하고 본인(1)을 포함
```python
train_df['FamilySize'] = train_df['SibSp'] + train_df['Parch'] + 1
test_df['FamilySize'] = test_df['SibSp'] + test_df['Parch'] + 1
```

**title(호칭) 추출 및 변환**
- 'Name' 컬럼에서 정규표현식을 사용해 'Mr.', 'Miss.' 같은 호칭을 추출
```python
# 1. 이름에서 호칭(Title) 추출
train_df['Title'] = train_df['Name'].str.extract(' ([A-Za-z]+)\.', expand=False)
test_df['Title'] = test_df['Name'].str.extract(' ([A-Za-z]+)\.', expand=False)

# 2. 대표적인 호칭들을 숫자로 변환하고, 나머지는 'Other'로 통합
title_mapping = {'Mr': 1, 'Miss': 2, 'Mrs': 3, 'Master': 4}
train_df['Title'] = train_df['Title'].map(title_mapping).fillna(5) # 5는 'Other'
test_df['Title'] = test_df['Title'].map(title_mapping).fillna(5)
```

**age group 생성**
- 이전에 EDA에서 했던 것처럼 10년 단위의 나이 그룹 생성
```python
train_df['AgeGroup'] = (train_df['Age'] // 10 * 10).astype(int)
test_df['AgeGroup'] = (test_df['Age'] // 10 * 10).astype(int)
```

##### => 이 코드들을 실행하고 나면, 데이터가 훨씬 더 풍부해지고 모델이 학습하기 좋은 형태로 준비되었을 것이다.


