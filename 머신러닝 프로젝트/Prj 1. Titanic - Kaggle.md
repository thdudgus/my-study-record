# Titanic Survival Prediction 
kaggle 사용
### 기본 세팅
```python
# This Python 3 environment comes with many helpful analytics libraries installed
# It is defined by the kaggle/python Docker image: https://github.com/kaggle/docker-python
# For example, here's several helpful packages to load

import numpy as np # linear algebra
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)

# Input data files are available in the read-only "../input/" directory
# For example, running this (by clicking run or pressing Shift+Enter) will list all files under the input directory

import os
for dirname, _, filenames in os.walk('/kaggle/input'):
    for filename in filenames:
        print(os.path.join(dirname, filename))

# You can write up to 20GB to the current directory (/kaggle/working/) that gets preserved as output when you create a version using "Save & Run All" 
# You can also write temporary files to /kaggle/temp/, but they won't be saved outside of the current session
```

##### 라이브러리 불러오기
```python
import pandas as pd
```

##### 데이터 읽기
```python
test_df = pd.read_csv("/kaggle/input/titanic/test.csv")
```


## [[Step1]]:
매우 간단한 예측 (Baseline 1: 모두 사망)
## [[Step2]]:
간단한 규칙 기반 예측 (Baseline 2: 성별)
##### => Step1, 2를 마쳤다면, Kaggle 제출방법을 익히고 앞으로 만들 모델이 넘어야 할 최소한의 성능 기준을 확인한 것이다.

## [[Step3]] : 
탐색적 데이터 분석 (Exploratory Data Analysis, EDA)
##### => 남성보다 여성이, 1등석일수록, 나이가 어릴수록, 60대 이상이 생존율이 높다.
## [[Step4]]:
Feature Engineering
## [[Step5]]:
**로지스틱 회귀(Logistic Regression)** 모델을 `scikit-learn` 라이브러리를 이용해 훈련시키기
## [[Step6]]:
새로운 모델 도입 (Decision Tree, Random Forest, or SVM)


