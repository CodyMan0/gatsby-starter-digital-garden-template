
리액트 앱을 개발할 때 백엔드와 연동하는데 ==큰 도움을 주는 Proxy==를 다루고 있습니다.

리액트 개발서버 http://localhost:3000 백엔드 서버(php, Django...) http://localhost:8000 리액트에서 백엔드에 접속 하려면 아래와 같이 코드를 작성해야 합니다. fetch('http://localhost:8000/data.json') 이 상태에서 build를 하면 localhost:8000에서 data.json 에 접속을 시도하기 때문에 제대로 동작하지 않습니다. 개발 할 때 fetch('/data.json')이라고 입력하면 리액트 개발 서버가 알아서 http://localhost:8000/data.json 서버에 접속해서 정보를 응답해준다면 얼마나 좋을까요? 이것을 가능하게 해주는 기술이 proxy 입니다. package.json 파일에 "proxy":"http://localhost:8000"이라고만 적어주면 됩니다. 이 수업에서는 proxy의 개념과 사용법을 다루고 있습니다.


### 참고 문헌 
- 생활 코딩 