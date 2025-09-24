격자 형태로 요소를 배치할 때 씀. 

GridView 자체가 스크롤이 가능한 위젯.

```dart
 Column(
        children: <Widget>[
          Expanded(  
    // Expanded 위젯을 사용하여 Column 내에서 GridView가 차지할 공간을 유동적으로 할당
            child: GridView.builder(
              gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
                crossAxisCount: 2,  // 한 줄에 2개의 카드 배치
                crossAxisSpacing: 10,  // 카드 간 가로 간격
                mainAxisSpacing: 10,  // 카드 간 세로 간격
              ),
              itemCount: contents.length,
              itemBuilder: (context, index) {
                return SelectCard(  // 만들어놓은 SelectCard 위젯 추가.
                  content: contents[index],
                  isInverted: false,
                  order: index + 1,
                );
              },
            ),
          ),
          // 여기에 다른 위젯 추가 가능
        ],
      ),
```
격자 사이의 간격은 mainAxisSpacing과 crossAxisSpacing으로 조절 가능.