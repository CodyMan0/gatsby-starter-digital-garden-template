1.  자바스크립트에서 Object, array는 [[흰 메모리]]에 관리가 된다. 실제 변수를 선언한 시점에는 흰 메모리에 대한 참조 주소만 가지고 있다. 만약에 바로 키로 접근해서 (input[id] = value) 바꾸면 리액트가 값이 바뀌었는지 모른다. 리액트가 알고 있는 것은 참조값!! 실제 오브젝트의 블록 상태는 모른다.
2. 오브젝트 깊은 복사 #깊은복사 ...spread 문법을 사용하여 복사한다. 그렇게 되면 기존 state 객체가 아니라 새로운 state 객체

## useState use cases

-   State management
-   Conditional rendering
-   Toggle flags (true/false)
-   Counter
-   Get API data and store it in state


### 연결 문서
- [[JS-객체와 배열은 참조값만 저장하고 있다.]]

### 참고자료
- why should i use useState 
-> https://dev.to/colocodes/5-use-cases-of-the-usestate-reactjs-hook-4n00