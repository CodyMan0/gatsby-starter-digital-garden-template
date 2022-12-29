

---
aliases: []
tags : 
---
Up : [[HOME 🌎]]

출처 :
저자 :
URL : 
인용 : 

단순하게 : html 의 path를 바꾸는 것을 [[routing]]!! 다른 경로에 따라 다른 화면을 보여주는 것을 말한다..

XML = JSON 과 같음

# 가장 중요
[[critical rendering path]] : 브라우저에 웹페이지를 렌더링 하는 과정

-> 완전 정리하기


cloneNode -> 

더 효율적으로 하는 방법

html -> html Parser (꺾쇄가닫힐때까지 읽어주는 기계)-> DOM tree를 만들어준다. 

css -< css parser -> style rule

-> 돔과 쏨을 합쳐서 Render Tree가 그려진다 (정말 보이게 되는 것들만) {lay out}ex)head , meta , display:none

-> 랜더트리 브라우저에 넘겨지면 layout(요소가 화면에서 얼마만큼 공간, 위치 정보) 계산이 이뤄진다. painting(색생, 그림자)으로 그려진다 -> display(겹쳐있는 것을 정리 1)
-> 성능에 미치는 영향!!!!! 이 중요


위에는 배경지식 

리액트 CSR 최적화하는 원리 
변화가 일어났을때 화면을 그린다. -> 풍부한 인터렉션 -> 필연적으로 렌더 발생 -> 너무 많은 렌더로 인한 성능 저하 -> 리액트는 scheduler(cloneNode의 아이디어가 합쳐지면 놀라운 마법!! )가 있다 -> setState가 비동기적으로 돌게 됨 -> 

-> [[reconcilation]] 필요한 것만 업데이트 한다.






























### 생각의 연결고리
분야 :

키워드 : [[react MOC]] 


관련있는 메모 :
