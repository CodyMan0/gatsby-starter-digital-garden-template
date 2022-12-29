# useEffect

---

Data Fetching, 구독 등의 side effect는 매우 조심스럽게 다뤄야 합니다. 그렇다면 리액트에서 side effect는 언제 어떻게 발생시켜야 할까요?  
  

### 1-1. React에서 Side Effect의 올바른 발생 시점

아래 함수 컴포넌트는 `<h1>Hello World</h1>` 형태의 JSX를 브라우저에 렌더링 합니다. 이 상황에서 side effect를 발생시키고 싶다면 어떻게 해야 할까요?  
  

`const App = () => {   return <h1>Hello World</h1>; };`

가장 먼저 떠올릴 수 있는 생각은 ‘함수니까 함수의 return문 위에 하고 싶은 동작을 넣어두자’입니다. 그래서 아래와 같은 코드를 작성하게 됩니다.  
  

`const App = () => {   const doSideEffect = () => {    // do some side effect  };   doSideEffect();   return <h1>Hello World</h1>; };`

하지만 위와 같이 렌더링 단계(UI를 만들어내는 과정)에서 side effect를 발생시키게 되면 두 가지 문제가 발생합니다.

1.  **side effect가 렌더링을 blocking 합니다.**
2.  **매 렌더링마다 side effect가 수행됩니다.**

실제 예시 코드를 보면서 어떤 문제인지 알아봅시다.  
  

#### 1-1-1. **side effect가 렌더링을 blocking**

```
const App = () => {   
const doSideEffect = () => { 
// do some side effect  };  
doSideEffect();  
return <h1>Hello World</h1>; };
```


위 코드를 확인해 봅시다. 위 코드는 사이드 이펙트를 함수 컴포넌트 본문 안에서 실행시킵니다.  
  

기본적으로 코드는 위에서 아래 방향으로 순차적으로 실행됩니다. 따라서 App 함수 컴포넌트는`doSideEffect()` 동작이 끝날 때까지 JSX를 리턴하는 코드로 넘어가지 않습니다. 컴포넌트가 JSX를 return 하기 전까지는 UI가 브라우저상에 렌더링 되지 않기 때문에 결국 사이드 이펙트가 끝나기 전까지 렌더링을 하지 못하고 멈춰있게 됩니다.  
  

즉, ==사용자가 UI가 업데이트되는 것을 보기까지 오랜 시간이 소요된다는 것입니다. 이는 곧 사용자에게 좋지 못한 사용자 경험을 제공한다는 의미==입니다.  
  

#### 1-1-2. 매 렌더링마다 side effect가 수행

특정한 side effect들은 매번 실행될 필요가 없을 수도 있습니다. 예를 들어 인스타그램에서 피드에 대한 정보를 받아서 피드 리스트를 보여주는 화면을 생각해 봅시다. 피드 리스트를 보여주기 위해서는 최초에 피드 데이터들을 가져오는(**Data Fetching**) side effect가 필요합니다. 하지만 곰곰이 생각해 보면 외부에서 데이터를 가져오는 side effect는 매 렌더링마다 수행될 필요는 없고, 오히려 매번 수행한다면 비효율적입니다.  
  

``` jsx
const App = () => {   
// 코드 생략   // data fetching side effect  
getFeeds();   
return 피드리스트; };
```

피드 리스트에서 특정 피드에 좋아요를 눌러서 하트 색깔을 변경하는 상황을 생각 해봅시다. 하트 색깔을 변경하려면 컴포넌트에서 리렌더링을 발생시켜야 합니다. 리액트에서 함수 컴포넌트가 리렌더링 된다는 것은 곧 함수 컴포넌트를 다시 한번 호출한다는 뜻입니다.

==_(리액트는 컴포넌트의 state나 props가 변하면 자동으로 해당 함수 컴포넌트를 다시 호출하면서 리렌더링==을 수행해 줍니다)._  
  

즉, App이라는 함수가 다시 호출되고 그렇다면 다시 함수 내부의 코드를 위에서 아래 방향으로 순차적으로 실행시킵니다. 그 말은 다시 한번 `getFeeds()` side effect를 발생시킨다는 의미입니다.  
  

하트 색깔을 변경하는 등 작은 UI 업데이트가 발생할 때마다 매번 모든 피드 데이터를 다 가져온다면 불필요한 동작을 계속 수행하기에 비효율적입니다.  
  

#### 1-1-3. 정리

위 내용을 통해서 우리가 React에서 side effect를 언제 발생시켜야 하는지 생각해 보면 side effect는

1.  렌더링을 Blocking 하지 않기 위해서 **렌더링이 모두 다 완료되고 난 후 실행할 수 있어야 한다.**
2.  매 렌더링마다 실행되는 것이 아니라 **내가 원할 때만 조건부로 실행할 수 있어야 한다.**

위 두 가지 조건을 충족시키면서 발생시키는 것이 가장 좋습니다. 다행히 React에서는 위의 요구사항을 모두 충족시키면서 편하게 side effect를 발생시킬 수 있게 도와주는 `useEffect`라는 훅(hook)이 이미 존재합니다.

### 1-2. useEffect 사용법

==useEffect는 React에서 side effect를 편리하고 안전하게 발생시킬 수 있게 도와주는 hook==입니다.

useEffect의 사용법은 다음과 같습니다.  
  

`useEffect(콜백 함수);`

useEffect는 함수이고, 매개변수로 콜백 함수를 가집니다. 우리는 useEffect에 인자로 전달하는 콜백 함수에서 특정한 side effect를 수행시킬 수 있습니다.

실제 예제 코드를 통해서 알아봅시다.

먼저, useEffect 없이 side effect를 발생시키는 코드입니다.  
  

``` js
const App = () => {  
doSideEffect();  

return <h1>Hello, Wecoder</h1>; };
```

위 코드에서는 side effect를 렌더링 전에 발생시키고 있습니다. 우리는 이러한 코드는 렌더링을 blocking 하기에 좋지 않다는 측면을 이미 알고 있습니다.  
  

그렇다면 이 문제를 해결하기 위해서 useEffect를 사용해 봅시다.  
  

```jsx
import { useEffect } from 'react';
const App = () => {  
// 코드 생략   
useEffect(doSideEffect); 
return <h1>Hello, Wecoder</h1>; };
```


이번에는 side effect를 발생시키는 함수를 바로 호출하는 것이 아니라 useEffect의 인자로 전달했습니다. ==위와 같이 useEffect의 인자로 전달된 콜백 함수는 곧바로 호출되는 것이 아니라 모든 렌더링이 완료된 후에 호출됩니다==. 즉 렌더링을 blocking 하지 않고 side effect를 발생시킬 수 있게 되는 것입니다.  


나만의 언어 -> rendering이 일어난 후에 실행되도록 하는 함수가 useEffect!!
  

실제 [예시 링크](https://codesandbox.io/s/useeffect-hx7gwc?file=/src/App.js)에서 useEffect를 통해 발생시킨 side effect가 렌더링 이후에 실행되는 것을 확인해 보세요.

### 1-3. 조건부로 Side Effect 발생시키기

useEffect를 통해서 **렌더링이 모두 다 완료되고 난 후 side effect를 실행한다는 요구사항은 충족되었지만** 아직도 매 렌더링마다 side effect가 실행된다는 사실은 변함이 없습니다.  
  

이제는 side effect를 특정 조건이 충족할 때만 발생시키는 방법에 대해서 알아봅시다. 앞서 useEffect의 형태는 아래와 같다고 했습니다.  
  

`useEffect(콜백 함수);`

사실 useEffect는 ==콜백 함수 외에 한 가지 매개변==수를 더 가지고 있습니다. useEffect의 완전한 형태는 아래와 같습니다.  
  

`useEffect(콜백 함수, 의존성 배열);`

useEffect는 콜백 함수 외에 의존성 배열(dependencyArray)이라는 두번째 매개변수를 가집니다. 의존성 배열은 이름에서부터 알 수 있듯이 배열의 형태입니다. 이 배열이 바로 ==side effect의 발생 여부를 결정짓는 조건입니다==.  
  

useEffect의 동작 방식은 간단합니다.

첫 번째 렌더링 이후에는 무조건 useEffect에 전달된 콜백 함수를 호출하고 다음 렌더링부터는 아래의 조건에 따라 동작합니다.

1.  의존성 배열이 전달되지 않았다면 매 렌더링마다 콜백 함수를 호출한다.
2.  의존성 배열이 전달되었다면 의존성 배열의 값을 검사한다.
    -   a. 의존성 배열에 있는 값 중 **하나라도 이전 렌더링과 비교했을 때 달라졌다면** 콜백 함수를 호출한다.
    -   b. 의존성 배열에 있는 값이 **이전 렌더링과 비교했을 때 모두 다 같다면** 콜백 함수를 호출하지 않는다.

즉, ==useEffect에서 첫 번째 인자인 콜백 함수는 **실행시킬 동작**을 결정하고 두 번째 인자인 의존성 배열은 **실행시킬 타이밍을** 결정짓는다고 할 수 있습니다.==  
  

이를 코드와 함께 보자면 다음과 같습니다.  
  
![[스크린샷 2022-08-07 오후 12.16.00.png]]



정답은, “첫 번째 렌더링 이후에만 실행되고 그 뒤에는 실행되지 않는다”입니다. 의존성 배열이 전달은 되었지만 배열 안에 값이 아무것도 없기 때문에 변화를 비교할 값이 없고 따라서 첫 번째 렌더링 이후에만 실행되고 그 뒤에는 실행되지 않습니다.  
  

==이를 응용하자면 우리가 Data Fetching을 최초 한 번만 실행하면 될 경우에는 useEffect를 활용하면서 의존성 배열에 빈 배열을 넣어주면 최초 한 번만 데이터를 가져오는 side effect를 발생시키고, 그 이후에는 리렌더링이 되더라도 다시 데이터를 가져오지 않도록 만들 수 있습니다.==  
  

`useEffect(() => {   // data fetching side effect }, []);`

 실행되는 방법
 ``` jsx

const App = () => {

const [countOne, setCountOne] = useState(0);

const [countTwo, setCountTwo] = useState(0);

  

const raiseCountOne = () => {

setCountOne((countOne) => countOne + 1);

};

  

const raiseCountTwo = () => {

setCountTwo((countTwo) => countTwo + 1);

};

  

  

useEffect(() => {

// console.log("[]");

--> 첫 렌더링 이후에만 한번 실행

  

useEffect(() => {

// console.log("[countOne]");

// }, [countOne]);

--> 해당 스테이트가 변할때만 실행
  

// useEffect(() => {

// // 의존성배열에 countTwo만 포함

// // 렌더링 이후 countTwo가 변했을때만 실행

// console.log("[countTwo]");

// }, [countTwo]);

  

// useEffect(() => {

// // 의존성배열에 countOne, countTwo 둘 다 포함

**렌더링 이후 둘 중 하나라도 변하면 실행**

// console.log("[countOne, countTwo]");

// }, [countOne, countTwo]);
```


###  Rendering & Effect Cycle

아래 다이어그램은 `useEffect` 와 `React Component`가 렌더링 되는 과정을 함께 도식화 한 다이어그램입니다.
![[스크린샷 2022-08-08 오전 8.57.47.png|300]]
[그림 1-1] Rendering & Effect Cycle 다이어그램 출처: [https://dmitripavlutin.com/react-useeffect-explanation/](https://dmitripavlutin.com/react-useeffect-explanation/)  
  
함수 컴포넌트의 렌더링과 useEffect가 발생하는 과정을 풀어서 설명하자면 아래와 같습니다.

1.  컴포넌트가 렌더링 된다.
    
    _(최초로 진행되는 렌더링은 브라우저에 처음으로 이 컴포넌트가 보였다는 의미로 `mount` 라고 표현합니다.)_
    
2.  useEffect 첫 번째 인자로 넘겨준 콜백 함수가 호출된다. **(Side Effect)**
    
3.  컴포넌트의 state 또는 props가 변경되었을 경우 리렌더링이 발생한다. `(update)`
    
4.  useEffect는 두 번째 인자에 들어있는 의존성 배열을 확인한다
    
    -   a. **만약 의존성 배열이 전달되지 않았거나** / **의존성 배열 내부의 값 중 이전 렌더링과 비교했을 때 변경된 값이 하나라도 있다면** 첫 번째 인자로 넘겨준 콜백 함수가 호출된다. (**Side Effect**)
    -   b. 의존성 배열 **내부의 값 중 이전 렌더링과 비교했을 때 변경된 값이 없다면** 콜백 함수를 호출하지 않는다.
    -   c. state 또는 props가 변경된다면 3~4의 과정을 반복
5.  컴포넌트가 더 이상 필요 없어지면 화면에서 사라진다.
    
    _(컴포넌트가 브라우저의 화면에서 사라졌다는 의미로 `unmount`라고 표현합니다.)_
    

## 2. Clean Up Effect

---

clean up은 무언가를 정리하고 치운다는 의미입니다. useEffect hook은 side effect를 clean up 해주는 기능 또한 가지고 있습니다. 그렇다면 side effect를 clean up 하는 것이 왜 필요한지, 어떻게 할 수 있는지에 대해 알아봅시다.

### 2-1. Clean Up의 필요성

side effect에는 여러 종류가 있을 수 있습니다. 그중에서는 반드시 clean up이 필요한 effect들이 있을 수도 있습니다. 어떤 종류의 side effect가 clean up이 필요할까요? 그 기준은 해당 side effect가 ==지속적으로 남아있는가?==를 생각해 보시면 됩니다. 아래의 side effect는 지속적으로 남아있지 않기 때문에 clean up이 필요하지 않습니다.  
  

`useEffect(() => {   console.log('Hello, Wecoder'); }, []);`

그렇다면 아래의 side effect는 어떨까요?  
  
```
useEffect(() => {
	const countTime = () => {
	console.log('100ms가 지났습니다');
	};

	setInterval(countTime,100);
},[])
```

위의 side effect는 cleanup이 필요합니다.

코드를 해석해 보자면, 이 side effect는 `setInterval` 함수를 이용해서 100ms마다 `countTime` 함수가 호출되도록 하고 있습니다. useEffect의 의존성 배열에 빈 배열이 전달되었으므로 첫 번째 렌더링 이후에 side effect가 실행됩니다. 그런데 이 side effect를 clean up 해주지 않는다면 컴포넌트가 unmount 되는 경우 등 `setInterval`을 통한 구독이 필요 없어진 상황에서도 계속해서 콘솔이 출력되고 있을 것입니다.  
  

또 다른 상황을 살펴봅시다.  
  

```js
useEffect(() => { 
const button = document.getElementById('consoleButton'); // 1 
const printConsole = () => {  
	console.log('button clicked'); 
	 }; // 2 
	 
button.addEventListener('click', printConsole); // 3 });
```

이번에는 useEffect에 의존성 배열을 전달하지 않았습니다. 따라서, 이 side effect는 매 렌더링마다 실행됩니다. side effect가 하는 일을 살펴봅시다.

1.  `document.getElementById` 메서드를 통해서 `consoleButton` 이란 ID를 가진 요소를 가져와서 button 변수에 할당한다.
2.  printConsole 함수를 선언한다 이 함수는 `console.log`를 출력하는 함수이다.
3.  button에 click 이벤트가 발생할 때마다 printConsole이 실행되도록 button에 eventListener로 등록한다.

이 side effect는 위의 동작을 하고 있습니다. 그런데 이 side effect는 매 렌더링마다 실행되기에 렌더링이 될 때 마다 button에 eventListener가 추가됩니다. 즉 eventListener가 계속해서 중첩되고 있다는 의미입니다.  
  

따라서, 첫 렌더링 이후에는 버튼을 누르면 콘솔이 한 번만 출력되지만, 두 번째 렌더링이 되게 되면 eventListener가 한 번 더 추가되기에 콘솔이 두 번 출력되고, 그다음부터는 렌더링이 될 때마다 버튼을 눌렀을 때 콘솔이 출력되는 횟수가 점점 더 늘어납니다.  
  

실제 동작이 궁금하시다면 [예시 링크](https://codesandbox.io/s/useeffect-without-cleanup-npj947?file=/src/App.js)를 참고해보세요  
  

(_**경고**: 리액트를 사용하면서 위 코드처럼 DOM에 ID를 부여하고, ==직접 접근해서 eventListener를 부착하는 등의 행위는 반드시 필요한 경우를 제외하고는 사용을 권장하지 않는 안티 패턴입니다==. 이해를 돕기 위한 예시로만 생각하고 실제 코드를 작성할 때는 위와 같은 방법은 지양해 주세요)_  

  

정리하자면, 불필요하게 계속해서 side effect가 남아있어서 비효율적으로 작동할 수 있고, 프로그램의 동작이 의도한 대로 되지 않을 수도 있기 때문에 지속적으로 남아있는 side effect는 반드시 **clean up**을 해줘야 합니다. 이제 useEffect에서 어떤 방식으로 cleanup side effect를 할 수 있는지 알아봅시다.

### 2-2. Clean Up 방법

==useEffect는 side effect를 clean up 할 수 있는 방법을 제공해 줍니다.== 결론부터 말하자면 useEffect에서 side effect를 cleanup 하기 위해서는 **useEffect에 전달한 콜백 함수에서 clean up을 하는 함수를 리턴하면 됩니다.**  
  

함수를 리턴한다는 말이 잘 와닿지 않을 수도 있습니다. 실제 예시 코드와 함께 알아봅시다.  
  

``` jsx
useEffect(() => { 
const button = document.getElementById('consoleButton');   

const printConsole = () => {    console.log('button clicked');  
};   

button.addEventListener('click', printConsole); });
```

이전에 봤던 예제와 동일한 상황입니다. 이 코드에서 **useEffect에 전달한 콜백 함수에서 clean up을 하는 함수를 리턴해 봅시다.**  
  

``` jsx
useEffect(() => {   
const button = document.getElementById('consoleButton'); 

const printConsole = () => {    
console.log('button clicked');  };   button.addEventListener('click', printConsole);  
// side effect를 clean up 하기 위한 함수를 선언한다.  

const removeEventListener = () => {    button.removeEventListener('click', printConsole);  };   
// clean up 함수를 return 한다.  return removeEventListener; });
```


위와 같이 발생시킨 side effect를 상쇄하기 위한 함수를 만든 뒤 그 함수를 return 해주면 됩니다.

`addEventListener`로 등록한 `eventListner`는 `removeEventListener` 함수를 통해서 제거할 수 있기 때문에 해당 동작을 하는 함수(clean up 함수)를 만든 뒤 콜백 함수 내에서 clean up 함수를 리턴해줬습니다.

clean up 함수를 return만 해준다면 clean up 함수를 적절한 시점에 호출해 주는 일은 useEffect가 알아서 처리해 줍니다.  
  

useEffect는 clean up 함수를 두가지 경우에 호출해줍니다.

1.  **다음 side effect를 발생시키기 전**
2.  **컴포넌트가 unmount 될 때**

==위 두 가지 경우가 발생하면 useEffect는 clean up 함수를 호출==해 줍니다.  
  

이제 위의 예시 코드의 동작을 차근차근 이해해 보면 아래와 같습니다.

1.  useEffect에 의존성 배열을 전달하지 않았기 때문에 해당 effect는 매 렌더링마다 실행된다.
2.  리렌더링이 발생해서 useEffect가 다시 호출되는 상황이 발생한다.
    -   a. clean up 함수를 리턴해줬기 때문에 clean up 함수가 호출된다.
    -   b. clean up 함수가 호출된 뒤 effect가 발생된다.
    -   c. 리렌더링이 발생하면 **a ~ b**의 과정이 반복된다.
3.  컴포넌트가 unmount 되면 clean up 함수가 호출된다.  
      
    

실제 [예시 링크](https://codesandbox.io/s/useeffect-with-cleanup-thpwcp?file=/src/App.js)에서 clean up 동작을 아래 세가지 사항에 초점을 두고 확인해 보세요

1.  이전의 clean up을 하지 않았던 예시와 다르게 리렌더링을 해도 버튼을 누르면 정상적으로 콘솔이 한 번씩만 출력되는 것
2.  `console.log("effect start")`, `console.log("clean up effect")` 가 언제 출력되는지를 보면서 clean up 함수가 호출되는 시점을 확인
3.  컴포넌트가 unmount 될 때 clean up effect가 발생하는 것

## 3. Summary

---

-   React에서 Side Effect를 발생시킬 때는 아래의 두 조건을 충족시켜야 합니다.
    ==1.  렌더링 이후에 발생시켜야 한다.
    ==2.  매 렌더링 이후가 아니라 조건부로 원하는 순간에만 실행할 수 있어야 한다.====
-   React에서는 위의 조건을 충족시키면서 Side Effect를 발생시킬 수 있는 `useEffect`라는 hook을 제공해 주며 이를 통해서 손쉽게 Side Effect를 발생시킬 수 있습니다.
-   ==일부 Side Effect는 발생시킨 후 다시 Clean Up 하는 과정이 필요할 수 있습니다.==
-   `useEffect`에 인자로 전달한 콜백 함수에서 함수를 return 하면 **다음 effect가 실행되기 전과, 컴포넌트가 unmount 될 때** return된 함수를 호출해 주며 이를 통해 기존의 side effect를 clean up 할 수 있습니다.

## 4. FAQ

---

**Q. 컴포넌트당 하나의 useEffect만 사용해야 하나요?**

A. 아닙니다.

컴포넌트가 사용할 수 있는 useEffect 횟수에 대한 제한은 없습니다. 오히려 하나의 useEffect에서 모든 동작을 다 처리하려고 하면 코드가 관심사(목적)에 따라서 적절하게 분리가 되지 않아서 유지 보수하기 힘들어 질 수 있습니다. 따라서, 내가 발생시키고자 하는 side effect를 관심사별로 분리한 뒤 각각의 useEffect에서 활용하는 것이 더 좋은 코드를 짜는 방법입니다.  
  

``` jsx
const App = () => {   
//bad 
 useEffect(() => {   
	// do data fetching 
	// subscribe 
	// read and manipulate DOM  }); }; 

//good
const App = () => {  

useEffect(() => {   
// do data fetching  });   

useEffect(() => {    
// subscribe  });  

useEffect(() => {    
// read and manipulate DOM  }); };
```



### useEffect Q and A (연욱님)
useEffect 는 로직을 넣고 싶을때 사용하는 것. 데이터를 가져오거나 싶을때 즉 UI 만드는 것외에 외부적인 모든 것. 직접 사용해보면 알 수 있다.

-> 리액트가 useEffect를 쓰라는 것은 컴포넌트에 x를 넣으면 y가 나올 것이라는 확신이 있도록 하려고 랜더링 다 한다음 

-> addEventListenr를 지양하라는 이유 랜더링에 영향을 줄 수 있어서 그런가요? 
 : 리액트의 사고 하는 방식은 선언적 질문!! 

-> useEffect  
	1. 랜더링 되고 실행
	2. 유전성 배열에 해당하는 state 변경

-> props 는 읽기 전용

-> 과거의 복잡했던 class형 컴포넌트를 알아야 리액트를 잘다루는 것이 아니다. function이 기능이 없어서 안쓴것.

-> ==구독하고 있는 애들은 무조건 clean up==을 해줘야한다. 

-> 구독이라는 것 -> 프로그램 실행,종료까지 어떤 행위를 지켜보는 것을 말한다.

-> 인자로 받은 x 는 이미 내가 가지고 있는 값이라고 useEffect는 판단. 외부의 값을 읽어 온다라는 것은 함수 외부에 값을 코드로 가지고 있고 그 값을 그대로 함수 내에서 쓸데는 side Effect가 있다고 생각한다.  

-> ==virtal 돔은 리액트 내부에서 일어나는 것이고 효율적으로 UI를 바꾸기 위한 최적화 도구== / ==useEffect 는 effect를 일으킬 수 있도록 개발자에게 허용되는 도구== 

-> useEffect 백앤드와 통신하고 그 통신을 UI로 보여주려면 state값을 바꿔주면 가능하다. 

-> ==TIP== 프로젝트 시 클론을 받으면 무엇부터 봐야한다?  제일 루트에 있는 폴더를 봐야한다. 그러면 그 안에 코드들이 있고 그안에 다른 것들은 import하고 있고 그 다음으로 쫙 찾아가야한다. 흐름을 타면서 소스 코드 봐야함. 

-> 코어 리액트를 dom에 넣으면 react / IOS 에 넣으면 React Native

-> mount -> side Effect -> update -> 두번쨰 인자에 들어있는 의존성 배열확인 -> 있으면 콜백 없으면 넘어감. -> Unmount

-> ==useEffect에서의 클린업  이펙트를 정리하고 치우는 것== -> 1.  ==클린업 함수를 만들어 리턴해주는 것==. 2. ==페이지가 언마운트 될때도 이 클린 업함수를 호출해준다==.
 

### 연결문서
- [[sideEffect]]
