# 1. CSS Preprocessor
---

웹 페이지를 만들면서 CSS를 이용해 다양한 스타일을 적용하고 관리할 수 있고, 다양한 기능들을 적용할 수 있지만 문법이 불편해서 막상 적용하기 힘든 부분들이 있습니다. 이러한 불편함을 개선하고자 나온 기술이 CSS Preprocessor 즉, **CSS 전처리기**(2006 등장)입니다.  
  
CSS 전처리기가 하는 일은 간단합니다. 여러 가지 기능들을 문법적으로 편리하게 작성할 수 있도록 제공하는 **전처리기의 양식에 맞게 파일을 작성**해두면, 그걸 최종적으로 **실제 실행 전에 처리**를 해줘서 **브라우저가 읽을 수 있는 CSS 파일로 변환**해 주는 일을 합니다. CSS 전처리기는 많은 종류가 있지만 그중에서 Sass를 사용해 보도록 하겠습니다.  
  

# 2. Sass

---

Sass의 뜻은 **Syntactically Awesome Style Sheets**, 즉 문법적으로 엄청난 스타일 시트라는 의미입니다. 그 정도로 기존 CSS 파일에서 겪었던 불편한 부분들이 Sass를 사용하며 해결할 수 있습니다==. (어떤 불편함?)==

## 2-1. Sass 설치

$ npm install sass
 
설치가 완료되었다면, 아래처럼 package.json의 dependencies 항목에서 해당 패키지 명과 버전이 잘 추가되었는지 반드시 확인해 줍니다.

## 2-2. sass & scss

공식문서를 통해 보면 **Sass를 작성하는 문법은 두 가지**로 나뉘어 있습니다.  .sass 파일은 sass 문법을 활용한 방법이고, .scss 파일은 scss 문법을 활용한 방법입니다. 두 가지 문법을 보면 큰 차이가 있어 보이지 않습니다. 그렇다면 어떤 문법을 사용하는 것이 좋을까요?  
  
처음 Sass가 등장했을 때는 sass 문법을 활용했는데, ==현재는 sass보다 **scss 문법을 사용하는 것을 권장== 하고 있습니다. 왜냐하면 ==sass의 문법 개선==을 통해 나온 것이 scss이기도 하고, 여러 가지 문법의 차이가 있지만 ==scss가 더 넓은 범용성과 CSS의 호환성==** 등의 장점이 있기 때문입니다. 따라서 sass 문법보다 scss 문법을 익히는 것이 좋습니다.  
  
_(이후부터 사용하는 예시 코드는 전부 scss 문법으로 작성 되었다는 점을 인지해주시기 바랍니다!)_

##  2-3. Sass 적용하기

기존의 CSS 파일이 있다면 해당 파일의 **확장자명을 scss로 변경**하고, CSS를 적용한 js 파일에서도 import 한 **CSS 파일의 확장자명을 scss로 변경**해 줍니다. 확장자명을 변경한 뒤, 실제 코드에서 확인해 보면 기존에 CSS 파일에서 적용했던 스타일이 잘 적용이 되는 부분도 있지만, 다른 스타일이 적용되어 스타일이 깨지는 모습을 보게 되기도 합니다. [예시 링크](https://codesandbox.io/s/sharp-davinci-6fys94?file=/src/Router.js)에서 어떤 문제가 발생하는지 확인할 수 있습니다. 이러한 문제가 생기는 이유는 SPA와 연관되어 있습니다. MPA 환경에서는 각각의 페이지마다 CSS 파일을 독립적으로 import해 사용하기 때문에 선택자가 해당 페이지에서만 중복되지 않으면 됐지만, SPA 환경에서는 각각의 JS 파일에서 독립적으로 CSS 파일을 import 했다 하더라도, Router.js에 모든 페이지 컴포넌트가 모이고, index.js를 거쳐 결국 index.html에 모이게 되는 구조기 때문에 각각의 ==CSS 파일에서 겹치는 선택자가 있다면,스타일이 깨질 수 밖에 없는 것입니다.==

![[스크린샷 2022-08-01 오후 1.53.20.png]]

위와 같은 문제를 해결하기 위한 방법으로는 ==모든 태그에 className을 다르게 주는 방법==과 ==CSS의 자손결합자를 사용하는 방법==이 있습니다. className을 모두 다르게 주는 방법은 처음에는 가능할지 몰라도, 컴포넌트가 많아지고 관리하는 태그들이 많아지게 된다면 나도 모르게 **중복해서 사용하는 className이 있을 수 있고**, 그렇게 된다면 **유지보수를 하거나 에러를 고치는데 상당히 복잡**해질 수 있는 문제점이 있습니다.  


그래서 ==CSS의 자손결합자를 이용하는 방법이 가장 효율적인 해결책==입니다.

1.  자손결합자를 이용하는 방법은 여러 가지가 있지만, 그중 **가장 최상위 부모 태그의 className에 컴포넌트 이름과 동일한 className을 부여**하는 방법을 사용해 보겠습니다. 왜냐하면 각 컴포넌트에서 사용하는 className은 겹칠 수 있지만, 컴포넌트의 이름은 겹치면 안 되기 때문입니다. 그렇기 때문에 최상위 부모 태그의 className에 컴포넌트 이름을 부여하면, 각 컴포넌트끼리 겹치는 className이더라도 **어떤 컴포넌트에서 사용하는 className이란 것**을 명확하게 구분할 수 있게 됩니다. 주의할 점은 첫 번째 글자를 대문자로 적는 것은 컴포넌트 이름에 적용되는 네이밍 컨벤션이기 때문에, 최상위 부모 태그의 className은 **카멜 케이스(camelCase)로 작성**해야 합니다.
2.  ==scss 파일에서 자손결합자를 활용해 스타일을 적용하고자 하는 선택자 앞에 최상위 부모 태그의 className으로 부여했던 선택자를 작성해서 컴포넌트별로 스타일이 적용될 수 있도록 구현해 줍니다.== 위와 같은 방식으로 스타일을 적용하면 컴포넌트끼리 CSS가 겹치지 않게 됩니다.

depth가 깊어지더라도 자손결합자는 스타일을 적용하고 싶은 선택자 앞에 조상 선택자 (부모의 부모 / 부모의 부모의 부모 ...)를 입력해 정확하게 해당 요소를 선택할 수 있는 CSS 문법이기 때문에 자손결합자를 사용하면 CSS가 겹치는 문제를 해결할 수 있습니다. 하지만 사용할 때마다 매번 조상 선택자를 작성해 줘야 하기 때문에 적용해야 할 스타일이 많아지면 쓰기 불편해지게 됩니다. 이때, 우리는 ==Sass의 nesting 기능을 통해 자손결합자를 더 편하게 작성==해 줄 수 있습니다.  
  
위와 같은 방법 외에도 같은 문제를 해결하는 방법은 여러 가지가 있지만, 지금은 자손선택자와 아래에서 배우게 될 Sass의 nesting 기능을 통해 문제를 해결하겠습니다.

## 2-4. Sass의 활용

### 2-4-1. Nesting

컴포넌트 간 CSS가 겹치지 않도록 설정하는 방법으로 ==className을 전부 다르게 적용==하거나, ==자손결합자 기능을 활용해 설정==할 수 있지만, 여러 문제점과 불편한 점이 있다고 언급했습니다. 이러한 부분을 Sass에서 사용하는 nesting 방식을 통해 해결할 수 있습니다.  

![[스크린샷 2022-08-01 오후 3.35.09.png|300]]\
위 코드를 보면 Sass의 nesting은 **마치 HTML 구조처럼** nav로 자식 관계에 있는 스타일을 품고, 그 안에 다른 태그들의 스타일을 적용하는 방법으로 구현할 수 있습니다. 위와 같이 스타일을 관리하게 되면, 스타일의 변경을 주고 싶거나, 오류가 발생한 부분을 비교적 빠르게 찾아 수정이 가능해집니다.

![session img](https://api-media-storage.s3.amazonaws.com/session-media/58f7b71834d148ae969ff8c0f4440e96?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIASTLUR2MM35PNGV2K%2F20220801%2Fap-northeast-2%2Fs3%2Faws4_request&X-Amz-Date=20220801T043617Z&X-Amz-Expires=60&X-Amz-SignedHeaders=host&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEP3%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaDmFwLW5vcnRoZWFzdC0yIkYwRAIgZ4wilya3JM7cwMHfuXU0D9nHV8p5ehuK8B71utjXjyYCICiFzflhRwTpMxloaVzcpnmuzP02vBsHp5LiIymN1Ay6KusCCFYQBBoMMTc5MDIyNDUxNDgxIgy1r5P0NgsBdeIQnYMqyAIbFYVhdZtuqgnGDaaNapx4pWuPp1qfxOoH1FMqPmy%2FR3g861GLE8ovGOkDYOdFY410DsHFNqgSDan%2FKOcvpqgHG3xMo%2FOnvH%2BSUhN%2FGmnZZsQD3FLvJsrTiIEhRQnpEm0mYIhxz9TdzVXPmef8AzigfI2vOoyfaj917rlUng4C%2F7ioKAkONA1uQh5wuhPgxpxpiCpjlVgNtHmBbgQrK5Dg%2B2AqChzFz7oQAmDN5VkNfMi4gxT0SrV%2BMsZmXT66GwEXNYB8SaL0BbT2PGd9gAicfEw%2FxZuKgw668L4L%2FIshTWZmjNwxBvibEswIDdFQbfjzlZYa8rn7mOdxqS2COKYh05fVF0PL4ygE9CAgr13sgM%2BbRyTNrckFAMjjUyJnSHPVIvSOn4lNOnY5PBo9YUAtRsXAb0wELYimpTc181XiVSCaedae5PpOMPutnZcGOp8BmV%2FFWYQn3pHihVBP%2B4W0nCAJ4T3MCEzqTi8Ngow9fRpwHigepU9YPfGXwDJ%2Bb8sOoX0GicYxrunULe%2BEKqU27YzxeOW%2F4O60fHuXuVjW9bvRMiJ%2BXbzOfjfejThRNx9XHwI9ihDOaa3qkLg6I9B1ysH4%2BK8GxIivit8dg3KmmCucpM1c8oXPgS8yqbYKSjlKhN7yzqnG1xF5JhDwMpAb&X-Amz-Signature=7fa98c06cbe51b28f9ba8685a16b18fee4cec8fa48f7bf40b0447b19f6a47e7d)

[그림 2-1] Sass가 실제 페이지에서 반영되는 모습  
  
위의 scss 예시 코드를 적용한 결과를 개발자 도구에서 확인해보면, scss로 작성한 파일이 CSS로 변환되어 반영된 것을 확인할 수 있습니다. 이렇게 변환된 이유는 Sass가 CSS 전처리기이기 때문에 scss 문법을 이용해 편리하게 작성한 scss 파일을 실제 화면에 그려지게 될 때는, **컴퓨터가 읽을 수 있는 CSS 파일로 자동으로 변환**되기 때문입니다.  
  

### 2-4-2. 변수

CSS 스타일을 작성하다 보면 동일한 스타일 속성인데, **여러 곳에서 사용되거나 오타가 나기 쉬운 속성** (예를 들면 rgb로 컬러를 구현하거나, HEX 코드로 컬러를 구현할 때)을 종종 사용하게 됩니다. Sass에서는 이러한 **속성들을 변수**로 만들어 그 변수를 원하는 곳에 넣어서 사용하는 기능이 있습니다.  
  
``` js
// Sass 변수 활용 예시 

$primary-color: #333;

body { 
border: 1px solid black; 
color: $primary-color; 
} 

.inverse {   
background-color: $primary-color; 
color: white; 
}

```

### 2-4-3. & 선택자

Nesting 내부에서 & 선택자는 부모 선택자로 치환됩니다. 예를 들어, button 태그에 스타일을 부여하고, 해당 버튼에 hover 효과도 부여하고 싶다면 아래와 같이 구현할 수 있습니다.  
  

버튼 과 버튼:hover을 button 안에 &:hover


### 2-4-4. mixin

mixin은 앞선 변수 기능과 마찬가지로 중복되는 스타일 속성이 있을 때 사용하는 방법인데, **중복되는 스타일 속성이 여러 개가 있을 때 한 번에 묶어서** 사용하기 좋은 방법입니다.

mixin은 @mixin 변수 이름 { 여러 가지 스타일 속성 } 과 같은 형식으로 구현할 수 있습니다. 예를 들어 어떤 UI를 가운데 정렬할 때, 아래 예시와 같은 속성을 자주 사용하는데, 이 속성을 하나로 묶어서 flexCenter라는 이름으로 만들고 해당 스타일들이 사용되는 부분에 @include 변수 이름을 사용하면 mixin으로 만들어둔 해당 속성이 적용됩니다.  
  

// Sass mixin 활용 예시
@mixin flexCenter {  
display: flex;  justify-content: center;  align-items: center; }

.info {   @include flexCenter; }

위와 같이 여러 스타일을 고정적으로 묶어서 사용하는 방법도 있지만 인자를 넣어서 **스타일 속성의 틀은 유지한 채, 스타일 속성에 적용되는 값을 변경**해서 적용해 줄 수도 있습니다.  
  

// Sass mixin 인수 활용 예시 @mixin flexSort($justify, $alignItems) {   display: flex;  justify-content: $justify;  align-items: $alignItems; } .info {   @include flexSort('space-between', 'center'); } .feed {   @include flexSort('space-around', 'center'); }

인자를 사용하면 마치 **함수를 사용하는 것**처럼 인자를 받아 원하는 **스타일 속성값에 인자를 넣어주고**, 호출해 주는 부분에서는 **실제 들어가야 할 속성값을 입력**해주는 방식으로 구현할 수 있습니다. 이렇게 mixin에 인자를 사용하는 방식으로 활용하면 중복되는 속성이지만 속성값을 다르게 적용해야 하는 스타일에서 다양하게 적용할 수 있습니다.  
  
_(이외에도 ==mixin을 활용한 여러 가지 기능==이 있는데, [공식문서](https://sass-lang.com/documentation/at-rules/mixin)를 참고해 직접 적용해 보시기 바랍니다.)_  
  

### 2-4-5. variables.scss 적용

지금까지 같은 파일에서 변수나 mixin을 만들어 원하는 스타일 속성에 사용하는 방법을 알아봤습니다. 하지만 만들어둔 변수나 mixin을 다른 스타일 파일에서도 사용하고 싶다면 어떻게 하면 될까요?  ==(다른 파일에서도 사용하고 싶을떄)==
  
![[스크린샷 2022-08-01 오후 4.39.18.png|300]]


위의 예시를 보면 variables.scss 파일을 만들었고, 변수나 mixin 등 여러 스타일 파일에서 공통으로 사용되는 속성들을 이 파일에 작성해 줍니다.  
  

// src/pages/Login/Login.scss @import "../../styles/variables.scss" body {   border: 1px solid black;  color: $primary-color; } .inverse {   @include flexCenter;  color: white; }

그리고 작성해 둔 변수나 mixin 등을 사용해야 하는 스타일 파일에서 마치 컴포넌트에서 다른 컴포넌트를 불러올 때 사용하는 것처럼 @import를 이용해 공통 스타일을 관리하는 파일을 불러오게 되면, 그 파일 안에 있는 변수 혹은 mixin 등을 사용해 줄 수 있게 됩니다.  
  

# 3. Summary

---

-   Sass는 CSS 문법을 조금 더 편하게 작성할 수 있게 하고, scss 문법으로 작성한 파일을 실행 전에 처리를 해줘서 브라우저가 읽을 수 있는 CSS 파일로 변환해 주는 CSS 전처리기입니다.
-   기존 CSS 파일의 확장자를 scss로 변경하면 scss 문법이 사용 가능해 집니다.
-   Sass의 nesting, mixin 등 다양한 기능을 활용해서 문법적으로 조금 더 편하게 스타일을 작성할 수 있습니다.
-   개발을 하며 새로운 기술을 학습하고 프로젝트에 적용하는 가장 확실한 방법은 공식문서를 보는 것입니다. 공식 문서에 들어가 설치 방법부터 여러 가지 기능을 살펴보면서 효율적으로 활용하시길 바랍니다.

