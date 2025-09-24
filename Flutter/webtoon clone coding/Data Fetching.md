JSON은 여러 object로 이루어진 리스트
1. lib 폴더 안에 services라는 새 폴더 생성
2. services폴더 안에 api_services.dart 파일 생성

	```dart
	class ApiService {
		final String baseUrl = "https://webtoon-crawler.nomadcoders.workers.dev";
		final String today = '';
		} 
	```

	baseUrl에서 today에 추가한 URL에서 데이터를 가져오는 것. JSON 데이터로 리스트를 받을 것임.
3. lib 폴더 안에 models라는 새 폴더 생성 : API에서 받아온 정보들을 여러 클래스로 이루어진 리스트로 변환해야 함.
4. models 폴더 안에 webtoon_model.dart 파일 생성
