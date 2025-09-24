### ListView

> **크기가 고정적인 리스트일때 사용**, 고정된 목록을 생성할 때 사용. 목록의 아이템 수가 적거나 고정된 경우에 적합.   
> ex) 개발자가 정해놓은 게시판 카테고리 리스트
```dart
ListView(
  children: <Widget>[
    ListTile(
      title: Text('아이템 1'),
    ),
    ListTile(
      title: Text('아이템 2'),
    ),
    // ... 이하 추가적인 리스트 아이템 (위젯)
  ],
)
```
<br>

### ListView.builder

> **itemCount와 itemBuilder를 사용하여 동적으로 아이템을 생성하며, 많은 아이템을 사용할 시 사용**. 동적인 목록을 생성할 때 사용. 아이템이 동적으로 변경되거나 많은 수의 아이템을 효율적으로 처리해야할 때 적합.
> ex) 서버 요청으로 댓글 리스트, 알림 리스트 등 쿼리에 따라 리스트 아이템이 동적으로 가져올 때, 개발자가 크기를 정하지 못 하는 게시판의 작성된 글 리스트 
```bash
ListView.builder(
  itemCount: yourItemList.length,  //itemCount 속성에 전체 아이템의 수
  itemBuilder: (BuildContext context, int index) {  
  // itemBuilder에 각 아이템을 생성하는 함수
    return ListTile(
      title: Text(yourItemList[index]),
    );
  },
)
```
itemCount 속성에 전체 아이템의 수를, itemBuilder에 각 아이템을 생성하는 함수를 지정,
추가 기능으론 현재 화면에 보일 수 있는 아이템의 수만 화면에 렌더링하므로 효율적