---
aliases:
  - 오브젝트 스페이스
  - 모델 스페이스
  - object space
  - local space
  - 로컬 스페이스
  - 3D model coordinate
  - 3d 모델 좌표
---
### 3D model coordinate
각 모델은 각자의 coordinate systme에 자신의 origin과 존재한다. (some point on the model)

- 모든 오브젝트는 origin. up/right/forward라는 개념(자체 좌표 공간)을 갖고 있음.
- 상대적인 위치와 방향을 추적하는 데에 사용

각 모델은 자체의 model space에서 정의가 된다. 
이 모델들은 world coordinate에 transformation을 통해 배치된다.