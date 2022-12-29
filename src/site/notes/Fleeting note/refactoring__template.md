# 1. Code Refactoring

1. Code Refactoring

-   코드는 한번 작성되고 끝나는 게 아닙니다. 계속해서 많은 추가와 수정을 겪고, 이를 **유지보수**라고 합니다. 유지보수를 용이하게 하기 위해서는 코드의 가독성과 확장성이 좋아야합니다.
-   `Refactoring` 이란, 코드의 가독성과 확장성을 좋게 만드는 작업을 의미합니다. 조금 더 구체적으로 설명하자면, '소프트웨어의 겉보기 동작은 그대로 유지한 채, 코드를 이해하고 수정하기 쉽도록, 내부 구조를 변경하는 기법'이라고 할 수 있겠습니다.
-   단순히 많은 기능을 구현할 줄 안다고 좋은 개발자가 아닙니다. 효율적이고 확장성 있는 코드, 유지보수가 용이한 코드를 작성할 줄 아는 개발자가 좋은 개발자입니다.
-   학습의 과정에서도 많은 기능을 구현하는 것에 치중하기 보다 하나의 기능을 구현 하더라도 **좋은 코드가 무엇인지 혼자 충분히 고민해보는것이 실력 향상**에 더 도움이 됩니다.

# 2. Basic

2. Basic

## 2-1. console.log 지우기!

💡테스트 끝난 콘솔은 모두 지워 주세요! 'console.log'는 테스트를 할 때는 필수적이지만 최종 결과물에는 포함되면 안됩니다.

`function add(a, b) {   return a + b; }`

`function add(a, b) {   console.log(a);  console.log(b);  console.log(a);  console.log(b);  console.log(a);  console.log(b);  console.log(a);  console.log(b);  console.log(a);  console.log(b);  console.log(a);  console.log(b);   return a + b; }`

-   위 두 코드는 동작상으로는 어떤 차이도 없습니다.
-   `console.log`는 인자로 들어온 `a`, `b`값을 확인하기 위한 테스트의 용도 외에 어떤 영향도 미치지 않습니다.
-   이러한 `console.log`가 최종 결과물에 남아있다면 가독성을 해칠 수 있습니다.
-   또한 기존의 `console.log`가 잔존한 상태로 새로운 테스트를 위해 `console.log` 를 추가했을 때 기존의 `console.log`와 혼재되어서 내가 진짜로 확인하고 싶은 값이 무엇인지 알기 어려워집니다.
-   코드의 가독성, 다른 팀원을 위한 기본적인 배려 차원에서 `console.log`를 지우는 것은 **가장 기본적인 컨벤션입니다.**
-   따라서 반드시 테스트를 끝낸 `console.log`는 지워주셔야 합니다.

## 2-2. id ・ class명, 변수명, 함수명

💡id ・ class, 변수, 함수의 이름에서 의미가 직관적으로 드러나게 작성해주세요 코드는 쓰는 경우보다 읽히는 경우가 훨씬 많습니다!

![session img](https://api-media-storage.s3.amazonaws.com/session-media/966865797a48498ea942f90b4f56a4cd?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIASTLUR2MMSOFDROON%2F20220728%2Fap-northeast-2%2Fs3%2Faws4_request&X-Amz-Date=20220728T050947Z&X-Amz-Expires=60&X-Amz-SignedHeaders=host&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEJ3%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaDmFwLW5vcnRoZWFzdC0yIkcwRQIhAK2zZ%2BZLA5juqc%2FNadhjpvgQwA%2FWB9DD1izkE5kbFLjEAiB%2Fw9xbasd8qavlpukY2CE3374yaV3KwjKKPETWWAe%2Bbir0Agjm%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAQaDDE3OTAyMjQ1MTQ4MSIMCiwVZASdkXmfLAcSKsgCZvfoEyZprPIgMGKP%2B5BT%2Bu5tx4rKUyZX37V7MVME1VVZdxc%2F5X%2FvitHWo7PYXG5E0P1MKp64SZv%2B8TZwnukgXeuvfcddD4aZgUXSbw4o4ooP1ngJZ1idTljeMMFVLU20l1rqCE5IlVouNk4n16fpPFKsfhKX0RYr%2F5GXXeJesZtCUi7aaaCB0feAxXxOSixj7KV%2FckTYZlrOvzT9cfQ4WQmcR9km9YebPB0DTwh3c%2B2jJC0SkSTVtYnGDzhnae4KuM72p91%2BQgi0aqpSRvZOhdPZwHFMVn85PO62YOck5kKa0U2JGRQezhDH74GNMVRit%2BnNoJHZpIp9%2FPlr2ExO7np%2BWJxws8PO2vkirQZfhcsbpDEtefI%2Ftu8TrzsfAcP7bNKnE6h8doPey%2FYFlI19z8%2BhTEa2mhtSSMGrlEyudNQufItwLdA4tTChrIiXBjqeATXi1PtnCnUZ6RXzaadAFgVeUYzYUXlaossafnTfcyIG0fhSZyAjB1VKmjUS9nwks2AS3MU20aga8QDN6%2BKnbBl8Iyvotl8ailmJauU9eCYfckj8F4Wx6E3BKRrwdT86iOVvmZ4GNNtcYzVTVfIgMRCJkf%2FlPUweTr0cpN3BdV4OGf32cgpk3yAQZTPMXysIayZzlQQVSPvMhc7G8984&X-Amz-Signature=8850051450db9777d85369227c038d69bbf0d8c905014caa0b28cddf238c7ebe)

-   프로그래머가 가장 힘들어하는 일 중 대표적인 것이 이름짓기 입니다.
-   그럼에도 불구하고 변수, 함수, id ・ class의 이름에서 의미가 직관적으로 드러나게 작성해주셔야 합니다.
-   그렇다면 왜 이렇게 어려운 이름짓기(naming)에 신경을 써야할까요?

`// bad let value = "Tom"; let value2 = "Cruise" // good let firstName = "Tom" let lastName = "Cruise"`

-   bad의 예시에서 `value`와 `value2`라는 변수가 무슨 값을 담고있는지 바로 이해하실 수 있으신가요?
-   뒤의 "John"과 "Cruise"라는 값을 보고 각각이 무엇인지 한참동안 생각하고 유추해봐야 합니다.
-   하지만 밑의 `firstName`과 `lastName`이라는 변수명을 보면 각각의 변수가 이름과 성을 나타내고있다는것을 바로 알 수 있습니다.
-   이처럼 변수명은 해당 변수가 어떤 의미를 나타내고 있는지 명확하고 직관적으로 이해가 되도록 지어주셔야 합니다.

---

`// bad const data = ["tory", "mozzi"]; // good const petsOfYeonuk = ["tory", "mozzi"];`

-   bad의 예시에서 `data`라는 변수에 담긴 배열이 어떤 `data` 인지 명확히 인식이 되시나요?
-   `data` 인 건 알겠는데, 무슨 `data` 인지 알 수가 없습니다.
-   위와 같은 이유로 `data`, `value` 등의 포괄적인 이름은 지양해주셔야 합니다.
-   good의 예시에서는 변수명을 보고 이 배열이 어떤 값을 담고있는지(`petsOfYeonuk`) 바로 이해할 수 있습니다.

---

개발자가 보내는 시간 중 코드를 짜는 시간은 10% 밖에 안된다고 합니다.

나머지 90% 시간은 모두 코드를 읽고 해석하면서 시간을 보낸다고 합니다.

그렇기 때문에 내가 짠 코드를 미래의 내가, 그리고 협업하는 다른 팀원들이 읽기 쉽게 만드는 일은 가장 기본이면서 가장 중요한 일입니다.

따라서, 모두 명확하고 직관적인 네이밍을 통해서 가독성이 좋은 코드를 짜셔야 합니다.

## 2-3. 들여 쓰기

💡프로그래밍 언어에서 규칙성 있는 들여 쓰기는 가독성 측면에서 매우 중요합니다.

    
-   javascript는 2칸 들여 쓰기를 컨벤션으로 정하고 있습니다.
    
-   컨벤션에 맞는 들여쓰기 적용해주세요
    

# 3. HTML


3. HTML

## 3-1. Semantic Tag의 사용

💡HTML에는 다양한 태그가 존재하며 그 중에서도 Semantic Tag를 적절하게 사용하는 것은 가독성 ・ SEO측면에서 너무나 중요합니다. 'div', 'span' 태그를 남발하기 보다는 상황에 맞게 적절한 태그를 사용해주세요

-   HTML은 언제 사용하나요?
-   HTML은 웹브라우저가 읽을 수 있는 문서를 작성하기 위해 사용합니다.
-   문서는 명확히 어떤 정보를 나타내고 있는지 알 수 있어야 가치있는 문서라고 할 수 있습니다.
-   아래의 예시를 봅시다.

`셀프 리팩토링 리팩토링이무엇일까요? 리팩토링은 소프트웨어의 겉보기 동작은 그대로 유지한 채, 코드를 이해하고 수정하기 쉽도록 내부 구조를 변경하는 기법입니다.`

-   위의 문서에서 어디가 제목이고 어디가 본문인지 이해가 되시나요?

`제목:셀프 리팩토링  본문:  리팩토링이무엇일까요? 리팩토링은 소프트웨어의 겉보기 동작은 그대로 유지한 채, 코드를 이해하고 수정하기 쉽도록 내부 구조를 변경하는 기법입니다.`

-   한결 이해하기 쉬워졌습니다.
-   위에서 어디가 제목이고, 어디가 본문인지 구분을 지어준 것 처럼 HTML에서는 tag를 이용해서 문서의 각 부분이 어떤 의미를 지니고 있는지 표시(Markup)할 수 있습니다.
-   위의 문서를 HTML로 표현해보면 아래와 같습니다.

`<article>   <h1>셀프 리팩토링</h1>  <p>    리팩토링이무엇일까요? 리팩토링은 소프트웨어의 겉보기 동작은 그대로 유지한    채, 코드를 이해하고 수정하기 쉽도록 내부 구조를 변경하는 기법입니다.  </p> </article>`

-   이처럼 Semantic Tag를 이용해서 HTML을 작성하면 사람과 웹 브라우저 모두 읽기 편해집니다.
-   따라서, SEO 최적화, 접근성 향상, 가독성 높은 코드 등의 이점을 얻을 수 있습니다.

### semantic vs non-semantic tag

`<!-- non-semantic  --> <div style="font-size:32px">제목</div> <!-- semantic  --> <h1>제목</h1>`

`<!-- non-semantic  --> <div class="mentorList">   <div>Joonsik</div>  <div>Dohyun</div>  <div>ShinYoung</div>  <div>Yeonuk</div>  <div>lang</div>  <div>Jungil</div>  <div>Myungsung</div>  <div>Youjin</div> </div> <!-- semantic  --> <ul class="mentorList">   <li>Joonsik</li>  <li>Dohyun</li>  <li>ShinYoung</li>  <li>Yeonuk</li>  <li>lang</li>  <li>Jungil</li>  <li>Myungsung</li>  <li>Youjin</li> </ul>`

## 3-2. img tag alt 속성

💡img tag를 사용하실 때 반드시 alt 속성 부여해주세요

-   img 태그를 사용하실 때는 아래와 같은 이유로 반드시 alt 속성을 부여해주셔야 합니다.
    
    1.  이미지가 로딩되지 않을 경우 alt 속성에 적힌 값이 보여짐.
    2.  시각장애인의 경우 alt 속성을 통해 어떤 이미지가 보여지는지 알 수 있음.
    3.  SEO 검색엔진 최적화에서 어떤 img인지 인식하는 코드는 alt 속성임.
-   **위와 같은 이유로 `alt` 속성은 중요하기 때문에 `src` 속성보다 먼저 작성하는게 좋습니다.**
    

`<!-- Bad  --> <img src="/images/branding/googlelogo/2x/googlelogo_color_272x92dp.png" /> <!-- Good  --> <img alt="Google Logo" src="/images/branding/googlelogo/2x/googlelogo_color_272x92dp.png" />`

## 3-3. Self Closing Tag

💡Self Closing이 가능한 tag들은 Self Closing을 적용시켜 주세요

-   HTML tag는 일반적으로 여는태그(`<div>`) 와 닫는태그 (`</div>` )로 이루어져 있습니다.
    
-   하지만, 열고닫는 태그 없이 스스로 닫을 수 있는(Self Closing) tag들이 있습니다.
    
-   불필요하게 모든 태그를 열고 닫으면 가독성을 해칠 수 있습니다.
    
    `<!-- Bad  --> <input type="password"></input> <!-- Good  --> <input type="password" />`
    
-   아래는 Self Closing을 적용할 수 있는 단일 tag들의 목록입니다.
    
    -   `<br />`
    -   `<hr />`
    -   `<img />`
    -   `<meta />`
    -   `<link />`
    -   `<input />`

# 4. CSS

4. CSS

## 4-1. CSS 속성 순서

💡CSS 속성은 **레이아웃에 영향을 많이 주는 순서대로, 인접 속성끼리 묶어서** 작성해주는게 좋습니다.

우리의 옷장을 생각해봅시다. 우리는 자연스럽게 상의, 하의, 겨울옷, 여름옷 등의 기준으로 보관하는 공간을 분리합니다. 기준없이 뒤섞여 있어도 옷에는 어떠한 영향도 미치지 않지만 우리는 자연스럽게 옷을 찾기 편하게 하기 위함입니다.

---

-   CSS 속성은 작성 순서는 성능향상이나 적용 순서에 유의미한 영향을 주지는 않습니다.
-   하지만 우리가 작성한 수많은 css 속성들이 규칙없이 뒤섞여 있다면, 원하는 속성이 어디에 있는지, 이 선택자에 어떤 속성이 적용되고 있는지 한눈에 파악하기 힘들어집니다.
-   CSS는 서로 영향을 미치는 구조로 이루어져 있고, 이 연관관계가 코드가 길어질수록 복잡해집니다. 이러한 이유로, **CSS 유지보수가 `Javascript` 유지보수보다 힘듭니다.**
-   따라서, 연관관계를 조금이라도 쉽게 파악하기 위해서 반드시 컨벤션을 지켜서 작성하는 습관을 들이셔야 합니다.
-   CSS 속성은 **레이아웃에 영향을 많이 주는 순서대로 , 인접 속성끼리 묶어서** 작성해주는게 좋습니다.
-   권장되는 속성 순서는 아래와 같습니다.
    1.  Layout Properties (position, float, clear, display)
    2.  Box Model Properties (width, height, margin, padding)
    3.  Visual Properties (color, background, border, box-shadow)
    4.  Typography Properties (font-size, font-family, text-align, text-transform)
    5.  Misc Properties (cursor, overflow, z-index)

## 4-2. 다른 CSS 선택자들 사이 한줄 띄우기

💡각자 다른 CSS 선택자들 사이에는 한 줄씩 공백을 주는 게 가독성 측면에서 좋습니다.

-   우리는 CSS 파일에서 수많은 선택자를 사용해서 HTML 요소를 특정하고 스타일을 입힙니다.
-   이렇게 수많은 선택자들이 공백 없이 붙어있다면 요소들이 구분되어 있는지 확인하기 쉽지 않습니다.

`.login-btn {   height: 2.5rem;  margin: 0.625rem 0px;  border: 0;  border-radius: 0.3125rem;  background-color: var(--disabled);  color: var(--white);  font-weight: 700;  font-size: 0.9375rem; } .find-password {   margin: 3.75rem 0 1.25rem 0;  color: #00376b;  text-align: center;  font-size: 12px; } .enabled-btn {   background-color: var(--enabled);  cursor: pointer; } .disabled-btn {   background-color: var(--disabled);  cursor: default; }`

`.login-btn {   height: 2.5rem;  margin: 0.625rem 0px;  border: 0;  border-radius: 0.3125rem;  background-color: var(--disabled);  color: var(--white);  font-weight: 700;  font-size: 0.9375rem; } .find-password {   margin: 3.75rem 0 1.25rem 0;  color: #00376b;  text-align: center;  font-size: 12px; } .enabled-btn {   background-color: var(--enabled);  cursor: pointer; } .disabled-btn {   background-color: var(--disabled);  cursor: default; }`

-   똑같은 두개의 예시코드에서 선택자 사이의 공백으로 인해 아래 예시 코드의 가독성이 훨씬 좋습니다.
-   가독성을 위해 다른 css 선택자들 사이는 한 줄 공백을 추가해주세요

## 4-3. 불필요한 style 속성 작성 지양

💡불필요한 style 속성은 작성할 필요가 없습니다.

1.  block 요소에 불필요하게 `display:block;` 을 부여하는 것
2.  block 요소에 불필요하게 `width:100%` 를 부여하는 것

-   위 두가지 예시처럼 불필요한 style 속성을 부여할 필요가 없습니다.
-   `<div>, <article>` 등 수많은 요소는 이미 display:block을 default style로 적용이 되고 있습니다.
-   이러한 tag들에 `display:block` 을 선언해줘서 불필요한 코드를 작성할 필요는 없습니다.
-   또한, `display:block` 요소들은 기본적으로 부모요소의 너비를 모두 차지하고 있습니다.
-   따라서, `display:block` 요소들에 불필요하게 `width:100%` 를 선언해줄 필요도 없습니다.
-   CSS의 기본 동작 원리를 잘 이해하고, 각 HTML tag들이 어떤 default css value를 가지고 있는지 확인해서 불필요한 style 속성 작성을 지양해주세요

---

**📎 참고자료**

1.  [CSS Default Values Reference](https://www.w3schools.com/cssref/css_default_values.asp)

## 4-4. 레이아웃은 bottom-up 방식으로 구성

💡레이아웃을 구성할 때 부모요소의 높이를 미리 정해두고 자식요소의 크기를 정하는 top-down 방식이 아닌, 자식요소의 높이에 따라 부모요소의 높이가 유동적으로 결정되는 bottom-up 방식으로 구성해주세요.

-   레이아웃을 구성할 때 부모요소의 크기를 고정적으로 정해둔다면, 자식요소의 크기가 변함에 따라서 부모요소의 크기가 유동적으로 변하지 않습니다.
-   이런 상황에서 만약 자식요소의 크기가 변해야 한다면, 부모요소의 CSS도 같이 수정해줘야 하는 불편함이 있습니다.
-   이런 구성이 겹겹이 쌓인다면 추후에 CSS 유지보수가 매우 힘들어집니다.
-   다시 한번 기억합시다, `CSS` 유지보수가 `Javascript` 유지보수보다 힘듭니다.

`// bad .feedList {   height:100vh; } .feed{   height:300px; } // good .feedList {   padding-top:20px; } .feed{   height:300px; }`

-   feedList안에 여러개의 feed가 들어있는 상황을 가정해봅시다. `(feedList > feed * n)`
-   bad의 경우 여러 feed들을 감싸고 있는 feedList에 고정 height를 부여했습니다.
-   feedList가 안에 feed가 몇개나 생성될 지 모르기에 feedList의 크기는 feed의 개수에 따라서 유동적으로 조정되어야 합니다.
-   하지만 bad의 예시에서는 feedList는 고정 height를 가지고 있으므로 feed가 1개일 때도, 그리고 20개일 때도 똑같이 100vh의 height를 가지고 있습니다.
-   즉 자식요소의 크기에 따라서 부모의 크기가 유동적으로 조정이 안되고 있습니다.
-   하지만 good의 예시를 보면 feedList에는 고정 height를 부여하지 않았습니다. 이 경우에는 feedList의 크기가 자식요소의 크기만큼 자동으로 조정됩니다.
-   즉, feedList의 높이가 내부의 `자식요소의 높이 + 20px(padding-top 값)` 로 유동적으로 변할 수 있게 됩니다.
-   레이아웃을 구성할 때는 자식요소에 따라 부모요소가 조정되도록 bottom-up 방식으로 구성해주세요

고정 height를 부여해서 레이아웃에 문제가 생긴 상황

![session img](https://api-media-storage.s3.amazonaws.com/session-media/debd7ed7ab7149fe9caa9ab93325975a?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIASTLUR2MMSOFDROON%2F20220728%2Fap-northeast-2%2Fs3%2Faws4_request&X-Amz-Date=20220728T050947Z&X-Amz-Expires=60&X-Amz-SignedHeaders=host&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEJ3%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaDmFwLW5vcnRoZWFzdC0yIkcwRQIhAK2zZ%2BZLA5juqc%2FNadhjpvgQwA%2FWB9DD1izkE5kbFLjEAiB%2Fw9xbasd8qavlpukY2CE3374yaV3KwjKKPETWWAe%2Bbir0Agjm%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAQaDDE3OTAyMjQ1MTQ4MSIMCiwVZASdkXmfLAcSKsgCZvfoEyZprPIgMGKP%2B5BT%2Bu5tx4rKUyZX37V7MVME1VVZdxc%2F5X%2FvitHWo7PYXG5E0P1MKp64SZv%2B8TZwnukgXeuvfcddD4aZgUXSbw4o4ooP1ngJZ1idTljeMMFVLU20l1rqCE5IlVouNk4n16fpPFKsfhKX0RYr%2F5GXXeJesZtCUi7aaaCB0feAxXxOSixj7KV%2FckTYZlrOvzT9cfQ4WQmcR9km9YebPB0DTwh3c%2B2jJC0SkSTVtYnGDzhnae4KuM72p91%2BQgi0aqpSRvZOhdPZwHFMVn85PO62YOck5kKa0U2JGRQezhDH74GNMVRit%2BnNoJHZpIp9%2FPlr2ExO7np%2BWJxws8PO2vkirQZfhcsbpDEtefI%2Ftu8TrzsfAcP7bNKnE6h8doPey%2FYFlI19z8%2BhTEa2mhtSSMGrlEyudNQufItwLdA4tTChrIiXBjqeATXi1PtnCnUZ6RXzaadAFgVeUYzYUXlaossafnTfcyIG0fhSZyAjB1VKmjUS9nwks2AS3MU20aga8QDN6%2BKnbBl8Iyvotl8ailmJauU9eCYfckj8F4Wx6E3BKRrwdT86iOVvmZ4GNNtcYzVTVfIgMRCJkf%2FlPUweTr0cpN3BdV4OGf32cgpk3yAQZTPMXysIayZzlQQVSPvMhc7G8984&X-Amz-Signature=74db3ed7aeb3970a8cffc778141e9e3e8759387cb9e3c1fbcf2b86e79844a67b)

![session img](https://api-media-storage.s3.amazonaws.com/session-media/e4d52e7f85254910b17e3f60d487fe44?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIASTLUR2MMSOFDROON%2F20220728%2Fap-northeast-2%2Fs3%2Faws4_request&X-Amz-Date=20220728T050947Z&X-Amz-Expires=60&X-Amz-SignedHeaders=host&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEJ3%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaDmFwLW5vcnRoZWFzdC0yIkcwRQIhAK2zZ%2BZLA5juqc%2FNadhjpvgQwA%2FWB9DD1izkE5kbFLjEAiB%2Fw9xbasd8qavlpukY2CE3374yaV3KwjKKPETWWAe%2Bbir0Agjm%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAQaDDE3OTAyMjQ1MTQ4MSIMCiwVZASdkXmfLAcSKsgCZvfoEyZprPIgMGKP%2B5BT%2Bu5tx4rKUyZX37V7MVME1VVZdxc%2F5X%2FvitHWo7PYXG5E0P1MKp64SZv%2B8TZwnukgXeuvfcddD4aZgUXSbw4o4ooP1ngJZ1idTljeMMFVLU20l1rqCE5IlVouNk4n16fpPFKsfhKX0RYr%2F5GXXeJesZtCUi7aaaCB0feAxXxOSixj7KV%2FckTYZlrOvzT9cfQ4WQmcR9km9YebPB0DTwh3c%2B2jJC0SkSTVtYnGDzhnae4KuM72p91%2BQgi0aqpSRvZOhdPZwHFMVn85PO62YOck5kKa0U2JGRQezhDH74GNMVRit%2BnNoJHZpIp9%2FPlr2ExO7np%2BWJxws8PO2vkirQZfhcsbpDEtefI%2Ftu8TrzsfAcP7bNKnE6h8doPey%2FYFlI19z8%2BhTEa2mhtSSMGrlEyudNQufItwLdA4tTChrIiXBjqeATXi1PtnCnUZ6RXzaadAFgVeUYzYUXlaossafnTfcyIG0fhSZyAjB1VKmjUS9nwks2AS3MU20aga8QDN6%2BKnbBl8Iyvotl8ailmJauU9eCYfckj8F4Wx6E3BKRrwdT86iOVvmZ4GNNtcYzVTVfIgMRCJkf%2FlPUweTr0cpN3BdV4OGf32cgpk3yAQZTPMXysIayZzlQQVSPvMhc7G8984&X-Amz-Signature=e9643b5f7426185b7d60ea9a477fb2c64b7263b9ce7a040b00fafe46a423577b)


#글쓰기

# HTML ,CSS 리팩토링 방법을 내 코드에 대입해보자... 🔎
## 처참할 수록 높아지는 성장 가능성.

###  📕사전개념 ) 코드 리팩토링이 무엇이냐! 

 코드의 가독성과 확장성이 좋아야 유지보수 관점에서 좋은 코드라고 한다. `리팩토링`은 가독성과 확장성을 좋게 만드는 일련의 작업을 말하고 있다. 



##  🥇 HTML 리팩토링

#### Semantic Tag의 사용

💡HTML에는 다양한 태그가 존재하며 그 중에서도 Semantic Tag를 적절하게 사용하는 것은 가독성 ・ SEO (검색 엔진 최적화)측면에서 너무나 중요하다. 


#### img tag alt 속성

img tag를 사용할때 alt 속성을 사용하면 스크린 리더 사용자에게 사진이 어떠한 사진인지 알려줄 수 있다고 한다. 오호!!! 그럼 웹 접근성이 높아지겠구나... 싶었다.
다.

#### 3-3. Self Closing Tag
- <br/>
- <hr/>
- <img />
- <meta />
- <link />
- <input />


# 4. CSS

4. CSS

## 4-1. CSS 속성 순서

💡CSS 속성은 **레이아웃에 영향을 많이 주는 순서대로, 인접 속성끼리 묶어서** 작성해주는게 좋습니다.

우리의 옷장을 생각해봅시다. 우리는 자연스럽게 상의, 하의, 겨울옷, 여름옷 등의 기준으로 보관하는 공간을 분리합니다. 기준없이 뒤섞여 있어도 옷에는 어떠한 영향도 미치지 않지만 우리는 자연스럽게 옷을 찾기 편하게 하기 위함입니다.

---

-   CSS 속성은 작성 순서는 성능향상이나 적용 순서에 유의미한 영향을 주지는 않습니다.
-   하지만 우리가 작성한 수많은 css 속성들이 규칙없이 뒤섞여 있다면, 원하는 속성이 어디에 있는지, 이 선택자에 어떤 속성이 적용되고 있는지 한눈에 파악하기 힘들어집니다.
-   CSS는 서로 영향을 미치는 구조로 이루어져 있고, 이 연관관계가 코드가 길어질수록 복잡해집니다. 이러한 이유로, **CSS 유지보수가 `Javascript` 유지보수보다 힘듭니다.**
-   따라서, 연관관계를 조금이라도 쉽게 파악하기 위해서 반드시 컨벤션을 지켜서 작성하는 습관을 들이셔야 합니다.
-   CSS 속성은 **레이아웃에 영향을 많이 주는 순서대로 , 인접 속성끼리 묶어서** 작성해주는게 좋습니다.
-   권장되는 속성 순서는 아래와 같습니다.
    1.  Layout Properties (position, float, clear, display)
    2.  Box Model Properties (width, height, margin, padding)
    3.  Visual Properties (color, background, border, box-shadow)
    4.  Typography Properties (font-size, font-family, text-align, text-transform)
    5.  Misc Properties (cursor, overflow, z-index)

## 4-2. 다른 CSS 선택자들 사이 한줄 띄우기

💡각자 다른 CSS 선택자들 사이에는 한 줄씩 공백을 주는 게 가독성 측면에서 좋습니다.

-   우리는 CSS 파일에서 수많은 선택자를 사용해서 HTML 요소를 특정하고 스타일을 입힙니다.
-   이렇게 수많은 선택자들이 공백 없이 붙어있다면 요소들이 구분되어 있는지 확인하기 쉽지 않습니다.

`.login-btn {   height: 2.5rem;  margin: 0.625rem 0px;  border: 0;  border-radius: 0.3125rem;  background-color: var(--disabled);  color: var(--white);  font-weight: 700;  font-size: 0.9375rem; } .find-password {   margin: 3.75rem 0 1.25rem 0;  color: #00376b;  text-align: center;  font-size: 12px; } .enabled-btn {   background-color: var(--enabled);  cursor: pointer; } .disabled-btn {   background-color: var(--disabled);  cursor: default; }`

`.login-btn {   height: 2.5rem;  margin: 0.625rem 0px;  border: 0;  border-radius: 0.3125rem;  background-color: var(--disabled);  color: var(--white);  font-weight: 700;  font-size: 0.9375rem; } .find-password {   margin: 3.75rem 0 1.25rem 0;  color: #00376b;  text-align: center;  font-size: 12px; } .enabled-btn {   background-color: var(--enabled);  cursor: pointer; } .disabled-btn {   background-color: var(--disabled);  cursor: default; }`

-   똑같은 두개의 예시코드에서 선택자 사이의 공백으로 인해 아래 예시 코드의 가독성이 훨씬 좋습니다.
-   가독성을 위해 다른 css 선택자들 사이는 한 줄 공백을 추가해주세요

## 4-3. 불필요한 style 속성 작성 지양

💡불필요한 style 속성은 작성할 필요가 없습니다.

1.  block 요소에 불필요하게 `display:block;` 을 부여하는 것
2.  block 요소에 불필요하게 `width:100%` 를 부여하는 것

-   위 두가지 예시처럼 불필요한 style 속성을 부여할 필요가 없습니다.
-   `<div>, <article>` 등 수많은 요소는 이미 display:block을 default style로 적용이 되고 있습니다.
-   이러한 tag들에 `display:block` 을 선언해줘서 불필요한 코드를 작성할 필요는 없습니다.
-   또한, `display:block` 요소들은 기본적으로 부모요소의 너비를 모두 차지하고 있습니다.
-   따라서, `display:block` 요소들에 불필요하게 `width:100%` 를 선언해줄 필요도 없습니다.
-   CSS의 기본 동작 원리를 잘 이해하고, 각 HTML tag들이 어떤 default css value를 가지고 있는지 확인해서 불필요한 style 속성 작성을 지양해주세요

---

**📎 참고자료**

1.  [CSS Default Values Reference](https://www.w3schools.com/cssref/css_default_values.asp)

## 4-4. 레이아웃은 bottom-up 방식으로 구성

💡레이아웃을 구성할 때 부모요소의 높이를 미리 정해두고 자식요소의 크기를 정하는 top-down 방식이 아닌, 자식요소의 높이에 따라 부모요소의 높이가 유동적으로 결정되는 bottom-up 방식으로 구성해주세요.

-   레이아웃을 구성할 때 부모요소의 크기를 고정적으로 정해둔다면, 자식요소의 크기가 변함에 따라서 부모요소의 크기가 유동적으로 변하지 않습니다.
-   이런 상황에서 만약 자식요소의 크기가 변해야 한다면, 부모요소의 CSS도 같이 수정해줘야 하는 불편함이 있습니다.
-   이런 구성이 겹겹이 쌓인다면 추후에 CSS 유지보수가 매우 힘들어집니다.
-   다시 한번 기억합시다, `CSS` 유지보수가 `Javascript` 유지보수보다 힘듭니다.

`// bad .feedList {   height:100vh; } .feed{   height:300px; } // good .feedList {   padding-top:20px; } .feed{   height:300px; }`

-   feedList안에 여러개의 feed가 들어있는 상황을 가정해봅시다. `(feedList > feed * n)`
-   bad의 경우 여러 feed들을 감싸고 있는 feedList에 고정 height를 부여했습니다.
-   feedList가 안에 feed가 몇개나 생성될 지 모르기에 feedList의 크기는 feed의 개수에 따라서 유동적으로 조정되어야 합니다.
-   하지만 bad의 예시에서는 feedList는 고정 height를 가지고 있으므로 feed가 1개일 때도, 그리고 20개일 때도 똑같이 100vh의 height를 가지고 있습니다.
-   즉 자식요소의 크기에 따라서 부모의 크기가 유동적으로 조정이 안되고 있습니다.
-   하지만 good의 예시를 보면 feedList에는 고정 height를 부여하지 않았습니다. 이 경우에는 feedList의 크기가 자식요소의 크기만큼 자동으로 조정됩니다.
-   즉, feedList의 높이가 내부의 `자식요소의 높이 + 20px(padding-top 값)` 로 유동적으로 변할 수 있게 됩니다.
-   레이아웃을 구성할 때는 자식요소에 따라 부모요소가 조정되도록 bottom-up 방식으로 구성해주세요

고정 height를 부여해서 레이아웃에 문제가 생긴 상황

![session img](https://api-media-storage.s3.amazonaws.com/session-media/debd7ed7ab7149fe9caa9ab93325975a?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIASTLUR2MMSOFDROON%2F20220728%2Fap-northeast-2%2Fs3%2Faws4_request&X-Amz-Date=20220728T050947Z&X-Amz-Expires=60&X-Amz-SignedHeaders=host&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEJ3%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaDmFwLW5vcnRoZWFzdC0yIkcwRQIhAK2zZ%2BZLA5juqc%2FNadhjpvgQwA%2FWB9DD1izkE5kbFLjEAiB%2Fw9xbasd8qavlpukY2CE3374yaV3KwjKKPETWWAe%2Bbir0Agjm%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAQaDDE3OTAyMjQ1MTQ4MSIMCiwVZASdkXmfLAcSKsgCZvfoEyZprPIgMGKP%2B5BT%2Bu5tx4rKUyZX37V7MVME1VVZdxc%2F5X%2FvitHWo7PYXG5E0P1MKp64SZv%2B8TZwnukgXeuvfcddD4aZgUXSbw4o4ooP1ngJZ1idTljeMMFVLU20l1rqCE5IlVouNk4n16fpPFKsfhKX0RYr%2F5GXXeJesZtCUi7aaaCB0feAxXxOSixj7KV%2FckTYZlrOvzT9cfQ4WQmcR9km9YebPB0DTwh3c%2B2jJC0SkSTVtYnGDzhnae4KuM72p91%2BQgi0aqpSRvZOhdPZwHFMVn85PO62YOck5kKa0U2JGRQezhDH74GNMVRit%2BnNoJHZpIp9%2FPlr2ExO7np%2BWJxws8PO2vkirQZfhcsbpDEtefI%2Ftu8TrzsfAcP7bNKnE6h8doPey%2FYFlI19z8%2BhTEa2mhtSSMGrlEyudNQufItwLdA4tTChrIiXBjqeATXi1PtnCnUZ6RXzaadAFgVeUYzYUXlaossafnTfcyIG0fhSZyAjB1VKmjUS9nwks2AS3MU20aga8QDN6%2BKnbBl8Iyvotl8ailmJauU9eCYfckj8F4Wx6E3BKRrwdT86iOVvmZ4GNNtcYzVTVfIgMRCJkf%2FlPUweTr0cpN3BdV4OGf32cgpk3yAQZTPMXysIayZzlQQVSPvMhc7G8984&X-Amz-Signature=74db3ed7aeb3970a8cffc778141e9e3e8759387cb9e3c1fbcf2b86e79844a67b)

![session img](https://api-media-storage.s3.amazonaws.com/session-media/e4d52e7f85254910b17e3f60d487fe44?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIASTLUR2MMSOFDROON%2F20220728%2Fap-northeast-2%2Fs3%2Faws4_request&X-Amz-Date=20220728T050947Z&X-Amz-Expires=60&X-Amz-SignedHeaders=host&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEJ3%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaDmFwLW5vcnRoZWFzdC0yIkcwRQIhAK2zZ%2BZLA5juqc%2FNadhjpvgQwA%2FWB9DD1izkE5kbFLjEAiB%2Fw9xbasd8qavlpukY2CE3374yaV3KwjKKPETWWAe%2Bbir0Agjm%2F%2F%2F%2F%2F%2F%2F%2F%2F%2F8BEAQaDDE3OTAyMjQ1MTQ4MSIMCiwVZASdkXmfLAcSKsgCZvfoEyZprPIgMGKP%2B5BT%2Bu5tx4rKUyZX37V7MVME1VVZdxc%2F5X%2FvitHWo7PYXG5E0P1MKp64SZv%2B8TZwnukgXeuvfcddD4aZgUXSbw4o4ooP1ngJZ1idTljeMMFVLU20l1rqCE5IlVouNk4n16fpPFKsfhKX0RYr%2F5GXXeJesZtCUi7aaaCB0feAxXxOSixj7KV%2FckTYZlrOvzT9cfQ4WQmcR9km9YebPB0DTwh3c%2B2jJC0SkSTVtYnGDzhnae4KuM72p91%2BQgi0aqpSRvZOhdPZwHFMVn85PO62YOck5kKa0U2JGRQezhDH74GNMVRit%2BnNoJHZpIp9%2FPlr2ExO7np%2BWJxws8PO2vkirQZfhcsbpDEtefI%2Ftu8TrzsfAcP7bNKnE6h8doPey%2FYFlI19z8%2BhTEa2mhtSSMGrlEyudNQufItwLdA4tTChrIiXBjqeATXi1PtnCnUZ6RXzaadAFgVeUYzYUXlaossafnTfcyIG0fhSZyAjB1VKmjUS9nwks2AS3MU20aga8QDN6%2BKnbBl8Iyvotl8ailmJauU9eCYfckj8F4Wx6E3BKRrwdT86iOVvmZ4GNNtcYzVTVfIgMRCJkf%2FlPUweTr0cpN3BdV4OGf32cgpk3yAQZTPMXysIayZzlQQVSPvMhc7G8984&X-Amz-Signature=e9643b5f7426185b7d60ea9a477fb2c64b7263b9ce7a040b00fafe46a423577b)


#글쓰기

