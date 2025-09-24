override메서드인 build 메서드는 **구현한 UI 위젯들을 화면에 출력**될 수 있도록 리턴해준다.

그렇다면 이 메서드에서 인수로 받는 BuildContext타입의 context는 무엇일까?
**BuildContext 타입은** **현재 위젯의 위젯트리상에서 위치에 관한 정보를 담고 있다.**  

context는 어떤 위젯의 정보를 담고있을까? 
바로 return 하는 위젯의 부모 위젯에 대한 위치 정보를 가지고 있다.

```dart
class MyHomePage extends StatelessWidget {
  const MyHomePage({ Key? key }) : super(key: key);

  @override
	// 여기서 context는 이 MyHomePage를 부르는 부모위젯의 위치정보를 담고 있음
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar( title: Text("MyHomePage"), ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            const Text('Test', ),
          ],
        ),
      ),
    );
  }
}
```