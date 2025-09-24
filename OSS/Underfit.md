---
aliases:
  - underfitting
  - 언더핏
  - 과소적합
---
parameter가 너무 적은 model은 **==large bias==**, 부정확.**(==not enough flexibility==)**
	**==Underfit==**
	![[Pasted image 20240510150258.png|400]]

### 예시 : kNN
k-Nearest Neighbor Classification
각 test data point에 가장 가까운 training data label을 할당.
![[Pasted image 20240510151130.png]]
![[Pasted image 20240510151208.png]]
**k가 너무 작아 변화에 민감 : Overfit**
**k가 너무 커 변화에 둔감 : Underfit**

![[Pasted image 20240510152446.png]]


## Underfitting and Overfitting
- **Underfitting** : model이 너무 simple 하거나 변화에 둔감. to represent all the relevant class characteristics.
	높은 bias
	(usually) 낮은 variance
	높은 training error
	높은 test error
	=> bias가 높으니까 대체로 variance가 낮아지고, 변화에 둔감하기 때문에 training data가 높고, test error도 높음.
	variance(분산)가 작아서 모여있어 underfit, 변화에 둔감.

- **Overfitting** : model이 너무 complex. 변화에 민감. fits irrelevant characteristics(noise) in the data.
	낮은 bias
	(usually) 높은 variance
	낮은 training error
	높은 test error
	=> bias가 낮으니까 대체로 variance가 높아지고, 변화에 민감하기 때문에 training data는 낮지만, test error는 높음. 
	variance(분산)가 크니까 넓게 퍼져있어 overfit, 변화에 민감

underfit, overfit 둘다 test error는 높아서 피해야 함. 그러나 overfit은 넓게 퍼져 있어 training error는 낮음.

![[Pasted image 20240510152207.png]]
![[Pasted image 20240510152246.png]]
variace와 bias는 trade-off 관계.

testing(validation) loss를 보며, 빠른 stop을 해야할 필요가 있음.
![[Pasted image 20240510152343.png|300]] ![[Pasted image 20240510152405.png|300]]