---
aliases:
  - handle
  - 핸들
---
production의 완전한 RHS와(production의 결과string과) 매치되고 reduction에 사용되는 substring
X->β일때, αβ|ω을 reduction하면, αX|ω가 된다. 
β는 αβω의 handle이다.

handle은 shift-reduce parsing을 하는 동안, 항상 left substring의 [[suffix]]이다. 
###### handle이 있으면 reduction을 하고, 없으면 shift를 한다.
어떻게 handle이 있는지 알 수 있을까?