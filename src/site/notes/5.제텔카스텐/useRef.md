---
aliases: [useRef]
tags : 
---

출처 : 벨로퍼트 기술 블로그
저자 :
URL : https://react.vlpt.us/basic/12-variable-with-useRef.html
인용 : 

useRef 사용법
1. 특정 DOM 을 선택할때 사용하는 용도 
2. 컴포넌트 안에서 ==조회 및 수정 할 수 있는 변수를 관리==

useRef 특징 
`useRef` 로 관리하는 변수는 값이 바뀐다고 해서 컴포넌트가 리렌더링되지 않습니다.
`useRef` 로 관리하고 있는 변수는 설정 후 바로 조회 할 수 있습니다.


이 변수를 사용하여 다음과 같은 값을 관리 할 수 있습니다.
1. `setTimeout`, `setInterval` 을 통해서 만들어진 `id`
2. 외부 라이브러리를 사용하여 생성된 인스턴스
3. scroll 위치


Ref는 render 메서드에서 생성된 DOM 노드나 React 엘리먼트에 접근하는 방법을 제공합니다.




### 생각의 연결고리
분야 :

키워드 :

관련있는 메모 : 
