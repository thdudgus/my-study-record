### 탐색적 데이터 분석 (Exploratory Data Analysis, EDA)
- 데이터 속에서 생존에 영향을 미친 단서, 즉 **패턴을 찾는 것**이 목표이다.
본격적인 모델링에 앞서 데이터를 깊이 이해하는 과정.

> 주요 feature별로 생존율을 분석한다!
> `Sex, Pclass, Age, Sibsp, Parch`

- Step 3에서는 제출 파일을 만드는 대신, `train.csv` 데이터를 가지고 분석하고 시각화한다.
- `train.csv`에는 'Survived'라는 정답이 있기 때문에, 이 정답과 다른 특징들(Pclass, Sex, Age 등)의 관계를 파헤칠 수 있다.
- 예를 들어, 노트북에 다음과 같은 코드를 작성하여 객실 등급(Pclass)별 생존율을 계산하고 막대그래프로 그려볼 수 있다.
##### 좌석 등급 기준
```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# 정답이 있는 train.csv 파일 불러오기.
train_df = pd.read_csv("/kaggle/input/titanic/train.csv")

# Pclass를 기준으로 그룹화하고, 각 그룹의 평균 생존율 계산
pclass_survival_rate = train_df.groupby('Pclass')['Survived'].mean()
print(pclass_survival_rate)

# 결과 시각화
sns.barplot(x=pclass_survival_rate.index, y=pclass_survival_rate.values)
plt.title('Survival Rate by Pclass')
plt.ylabel('Survival Rate')
plt.show()
```
**result**
![[Pasted image 20250924172736.png]]

##### 성별 기준
```python
# Sex를 기준으로 그룹화하고, 각 그룹의 평균 생존율 계산
sex_survival_rate = train_df.groupby('Sex')['Survived'].mean()
print(sex_survival_rate)

# 결과 시각화
sns.barplot(x=sex_survival_rate.index, y=sex_survival_rate.values)
plt.title('Survival Rate by Sex')
plt.ylabel('Survival Rate')
plt.show
```
**result**
![[Pasted image 20250924173306.png]]

##### 나이 기준
10살 기준 (10대, 20대, .... )
```python
# 나이 분포
age_group = train_df.groupby((train_df['Age'] // 10) * 10).size()
print(age_group)

# 결과 시각화
sns.barplot(x=age_group.index, y=age_group.values)
plt.title('The Number of Age Group')
plt.xlabel('age group')
plt.ylabel('count')
plt.show()
```
**result**
```text
Age
0.0      62
10.0    102
20.0    220
30.0    167
40.0     89
50.0     48
60.0     19
70.0      6
80.0      1
dtype: int64
```
![[Pasted image 20250924173417.png]]

나이 기준 생존율
```python
# Age를 10으로 나눈 몫을 기준으로 그룹화 (연령대별로 그룹화)
age_group_survival_rate = train_df.groupby((train_df['Age'] // 10) * 10)['Survived'].mean()
print(age_group_survival_rate)

# 결과 시각화
sns.barplot(x=age_group_survival_rate.index, y=age_group_survival_rate.values)
plt.title('Survival Rate by Age Group')
plt.xlabel('Age Group')
plt.ylabel('Survival Rate')
plt.show()
```
**result**
![[Pasted image 20250924173518.png]]

#### 가족 기준
##### SibSp 기준
Sibling = brother, sister, stepbrother, stepsister  
Spouse = husband, wife (mistresses and fiancés were ignored)
```python
# sibsp를 기준으로 그룹화
sibsp_survival_rate = train_df.groupby('SibSp')['Survived'].mean()
print(sibsp_survival_rate)

# 결과 시각화
sns.barplot(x=sibsp_survival_rate.index, y=sibsp_survival_rate.values)
plt.title('Survival Rate by SibSp')
plt.xlabel('SibSp')
plt.ylabel('Survival Rate')
plt.show()
```
**result**
![[Pasted image 20250924174023.png]]

##### Parch 기준
Parent = mother, father  
Child = daughter, son, stepdaughter, stepson  
Some children travelled only with a nanny, therefore parch=0 for them.
```python
# Parch를 기준으로 그룹화
parch_survival_rate = train_df.groupby('Parch')['Survived'].mean()
print(parch_survival_rate)

# 결과 시각화
sns.barplot(x=parch_survival_rate.index, y=parch_survival_rate.values)
plt.title('Survival Rate by Parch')
plt.xlabel('Parch')
plt.ylabel('Survival Rate')
plt.show()
```
**result**
![[Pasted image 20250924174342.png]]


##### 성별, 나이, 좌석 등급 기준
```python
# Age 그룹 컬럼 추가 (10단위로)
train_df['AgeGroup'] = (train_df['Age'] // 10) * 10

# Pclass 별 반복
for pclass in sorted(train_df['Pclass'].unique()):
    # 해당 Pclass만 필터링
    subset = train_df[train_df['Pclass'] == pclass]

    # 성별과 나이대 기준으로 그룹화 후 생존율 평균
    grouped = subset.groupby(['Sex', 'AgeGroup'])['Survived'].mean().reset_index()

    # x축 라벨을 '20s female' 이런 식으로 만들기
    grouped['GroupLabel'] = grouped['AgeGroup'].astype(int).astype(str) + 's ' + grouped['Sex']

    # 정렬 (나이순 + 성별)
    grouped = grouped.sort_values(by=['AgeGroup', 'Sex'])

    print()
    print(pclass)
    print(grouped)

    # 시각화
    plt.figure(figsize=(12, 6))
    sns.barplot(
        x='GroupLabel',
        y='Survived',
        hue='Sex',
        data=grouped,
        palette={'male': '#618eed', 'female': '#ed6b61'}
    )
    plt.title(f'Survival Rate by Age and Sex (Pclass {pclass})')
    plt.xlabel('Age Group and Sex')
    plt.ylabel('Survival Rate')
    plt.xticks(rotation=45)
    plt.ylim(0, 1)
    plt.grid(axis='y')
    plt.tight_layout()
    plt.show()
```
**result**
![[Pasted image 20250924174510.png]] ![[Pasted image 20250924174528.png]] ![[Pasted image 20250924174548.png]]


### => 남성보다 여성이, 1등석일수록, 나이가 어릴수록, 60대 이상이 생존율이 높다.
##### 1등석에서 10세 미만 데이터에서 남성이 여성보다 더 높은 생존율 (예외)
```python
# 1등석, 10세 미만 데이터만 필터링
pclass1_children = train_df[(train_df['Pclass'] == 1) & (train_df['Age'] < 10)]

# 성별과 생존 여부에 따른 인원수 확인
print(pclass1_children.value_counts(['Sex', 'Survived']))
```
**result**
```text
Sex     Survived
male    1           2
female  0           1
Name: count, dtype: int64
```
