 
 DOM 요소에 변화가 생기면 웹 브라우저는 다시 렌더 트리(DOM 트리 + CSSOM 트리)를 그리고, 레이아웃 위치를 계산하고(layout), 화면에 그리는 작업(paint)을 수행합니다. 


블로그로 아예 정리!! 하기 비유 -> 하노이 탑 

1.  HTML을 파싱해서 DOM을 만든다. 
2.  CSS를 파싱해서 CSSOM을 만든다.
3.  DOM과 CSSOM을 결합해서 Render Tree를 만든다.
4.  Render Tree와 Viewport의 width를 통해서 각 요소들의 위치와 크기를 계산한다.**(Layout)** -> [[flow, reflow ]]
5.  지금까지 계산된 정보를 이용해 Render Tree상의 요소들을 실제 Pixel로 그려낸다. **(Paint)**


+ 보강하기 
[[브라우저 동작원리]]