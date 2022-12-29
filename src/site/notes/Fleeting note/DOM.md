### 2022-07-22 17:43  

### 주제 : 돔이 무엇이냐!!
----
### 인풋

DOM이란? html에 자바스크립트가 접근할 수 있도록 객체로 만들어졌고 트리 형태로 만들어졌으며 요소 하나하나를 NODE 라고 한다. 자바스크립트로 노드를 제어할 수 있는 것은 노드가 모두 API 이다. 

1. 어떻게 접근?
2. 어떻게 제어? 


#### DOM이란
문서 객체 모델은 HTML,XML 문서의 프로그래밍 interface이다. DOM은 문서의 **구조화된 표현(structured representation)을 제공**하며 프로그래밍(자바스크립트) 언어가 DOM 구조에 접근할 수 있는 방법을 제공하여 그들이 **문서 구조, 스타일, 내용** 등을 변경할 수 있게 돕는다.

웹 페이지는 일종의 문서(document)다.  이 문서는 웹 [[브라우저 동작원리]] 를 통해 그 내용이 해석되어 웹 브라우저 화면에 나타나거나 HTML 소스 자체로 나타나기도 한다. 동일한 문서를 사용하여 이처럼 다른 형태로 나타날 수 있다는 점에 주목할 필요가 있다. **DOM 은 동일한 문서를 표현하고, 저장하고, 조작하는 방법을 제공한다**. **DOM 은 웹 페이지의 객체 지향 표현이며**, 자바스크립트와 같은 스크립팅 언어를 이용해 DOM 을 수정할 수 있다.

많은 브라우저들이 표준 규약(W3C , WHATWG)에서 제공하는 기능 외에도 추가적인 기능들을 제공하기 때문에 사용자가 작성한 문서들이 각기 다른 DOM 이 적용된 다양한 브라우저 환경에서 동작할 수 있다는 사실을 항상 인지하고 있어야 한다.

웹 페이지를 수정하거나 생성하는데 사용되는 모든 **property, method, event 들은 objects 로 구성된다.** 예를 들어 document object 는 document 자체를 의미하며, table object 는 HTML table 에 접근하기 위한 `HTMLTableElement` DOM 인터페이스를 구현한 것이다. 이 문서는 Gecko 기반의 브라우저에서 구현된 DOM 에 대한 object-by-object reference 를 제공한다.

#### DOM과 자바스크립트
문서(document) 와 문서의 요소(element) 에 접근하기 위해 DOM 이 사용되었다. DOM 은 프로그래밍 언어는 아니지만 **DOM 이 없다면 자바스크립트 언어는 웹 페이지 또는 XML 페이지 및 요소들과 관련된 모델이나 개념들에 대한 정보를 갖지 못하게 된다.** 문서의 모든 element - 전체 문서, 헤드, 문서 안의 table, table header, table cell 안의 text - 는 문서를 위한 document object model 의 한 부분이다. 때문에, 이러한 요소들을 DOM 과 자바스크립트와 같은 스크립팅 언어를 통해 접근하고 조작할 수 있는 것이다.

DOM 은 프로그래밍 언어와 독립적으로 디자인되었다. 때문에 **문서의 구조적인 표현은 단일 API 를 통해 이용가능**(??)하다.  이 문서에서는 자바스크립트를 주로 사용하였지만, DOM 의 구현은 어떠한 언어에서도 가능하다.

#### DOM에 어떻게 접근할 수 있는가? 
모든 웹 브라우저는 스크립트가 접근할 수 있는 웹 페이지를 만들기 위해 **어느 정도의 DOM** 을 항상 사용한다. 

스크립트를 작성할 때(인라인 <script 요소를 사용하거나 웹 페이지 안에 있는 스크립트 로딩 명령을 사용하여), 문서 자체를 조작하거나 문서의 children 을 얻기 위해 [document] 또는 [window] elements 를 위한 API 를 즉시 사용할 수 있다. 


#### 중요한 타입
- document : 
- element : 이 method 가 DOM 안에서 생생되는 `element` 를 리턴한다고 좀 더 단순하게 말할 수 있다.
- nodeLIst : elements 의 배열 각 인덱스 접근 방법 2가지 list[1] 와 list.item(1) 후자는 nodeList의 단일 메소드! !
- attributes 는 DOM 에서 elements 와 같은 nodes 이다.


#### 얄팍한 코딩 DOM
브라우저 = 공장
html = 공장으로 보내는 주문서 ( 구채적 구조들이 있음) 

즉 #HTML 이란 코드로 설계된 웹페이지가 브라우저 안에서 화면에 나타나고 이벤트에 반응하고 값을 입력 받는 등 기능들을 수행할 객체들로 실체화된 형태

어떤 언어든 #라이브러리 만 갖춰지면 DOM을 조작할 수 있는 이유 = DOM이 #API 를 가지고 있어서  


DOM 안에는 각종 #node 들이 #트리구조 로 들어있다.

트리구조 : html을 보면 각 요소들이 다른 요소들을 포함하는 식, 그래서 그런 관계도를 표현한 방식

node : DOM의 모든 요소 (html, div ,radio , table) 는 **node**로 부터 **상속**받는다. node는 **EventTarget**으로부터 상속 받는다. 즉 노드는 클릭 등의 이벤트가 가해지는 EventTarget


CSS 는 CSSOM으로 따로 만들어진다. html과 마찬가지로 트리구조로 생성
브라우저는 DOM 트리와 CSSOM 트리를 융합해서 화면을 생성




### #위코드_수업 
1.  웹에서 `HTML, CSS, Javascript`가 어떤 기능을 하는지 설명할 수 있다.
2.  `HTML`에서 `Javascript`를 연결하는 방법 2가지를 설명할 수 있다.
3.  `DOM`의 정의와 기능에 대해 설명할 수 있다.
4.  `DOM`을 이용해서 `Javascript`로 `HTML`에 접근하고 조작할 수 있다.
5.  `DOM`에 접근하기 위해 사용하는 메소드들(`getElement(s), querySelector(All)`)의 차이점을 설명할 수 있다.
6.  `addEventListener` 함수를 사용해 웹페이지를 동적으로 변화시킬 수 있다.


- [x] 돔은 HTML 계층화 시켜 트리구조로 만든 객체 모델
- [x] 자바스크립트 위치 : body 밑에서 불러옴  :  왜? html이 있어야 노드로 찍을 수 있다.
 - [x]  해드 안에도 적을 수 있따 -> < script>  안에 defer 
 - [ ] - #innerHTML -> 단순 스트링 뿐이나라 **HTML 형태로 추가할 수 있다.** 사용해보기
 - [ ] dom에 접근 :
- dom에 접근하는 방법
	- getElementById
	- getElementsByClass : return 값 복수 **html collection**
	- querySelector : 
	- querySelectorAll :  리턴 값 복수 nodeList

- [ ] #nodeLIst 는 foreach가 접근 할 수 없다.
- [ ] addEvnetListener는 요소에 붙는다. 노드 
- [ ] $0 하면 개발자요소에서 사용하면 가지고 올 수 있다고 하신다. ( 사용해보기)
- [ ] keyDown , keyUp, keyPress 차이를 westagram할때 찾아보기
-> **The keydown event occurs when the key is pressed, followed immediately by the keypress event.** **Then the keyup event is generated when the key is released**.
- [x] addEventListner 말고 html에도 추가 가능 -> onclink 그런데 onclike은 확정성때문에 사용을 비추하심. 이벤트를 하나밖에 주지 못한다. 
- [x] - #변수명_짓기
	- 변수는 camelCase
	- 불리언은 isValueValid으로 
	- 함수가 하는 역할을 명확하게 보여주는 이름 (동사형)
	- #component 는 #react 

- 자바스크립트 문제 풀이 병행하기 
- [x] for in 과 for of -> for of는 사용 가능 for in은 사용 불가!!!!  노드 접근하는 방식이 다르다. 찾아보기 
->  The only difference between them is the entities they iterate over: 

**for..in iterates over all enumerable(열거 할 수 있는) property keys of an object**
Object 자료형에 저장된 자료들을 하나씩 꺼내고 싶을 때 사용﻿ - 정확히는 ﻿enumerable 속성이 true인 자료형들만 for in 반복문을 돌릴 수 있다.

. **for..of iterates over the values of an iterable object**. 
Examples of iterable objects are **arrays, strings, and NodeLists.**


- [ ] (getElementByClass) forEach 사용불가 . 하지만 얕은 복사 -> !! 
- [ ] (querySelectorAll) 일때 foreach
- [ ] getElementByClassName은 #htmlCollection / #querySelectorAll 은 nodeList 정리
- [ ] [[Spread 문법]] 문법은 깊은 복사 :   


#### Questions
**동적 사용하는 이유** : 변수에 할당된 내용만 바뀌면 되기때문에!! 데이터 추출방법.
**interface** : 서로 잇는 것(매개체).





### 나의 언어로 정리
자바스크립트 언어로 document와 element에 접근할 수 있게 하는 것이 DOM.





### 출처(참고문헌)
1. MDN : https://developer.mozilla.org/ko/docs/Web/API/Document_Object_Model/Introduction
2. 얄코 : https://www.youtube.com/watch?v=1ojA5mLWts8
### 연결문서
- 
