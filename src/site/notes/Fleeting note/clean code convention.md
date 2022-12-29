---
aliases: []
tags : 
---

출처 : github
저자 : 박명호 프론트앤드 개발자 
URL : https://github.com/qkraudghgh/clean-code-javascript-ko#%EC%86%8C%EA%B0%9Cintroduction
인용 : 


## **변수(Variables)**

### 1. 의미있고 발음하기 쉬운 변수 이름을 사용하세요

좋은 예: const currentDate = moment().format('YYYY/MM/DD');

### 2. 동일한 유형의 변수에 동일한 어휘를 사용하세요
**안좋은 예:**
	getUserInfo();
	getClientData();
	getCustomerRecord();

**좋은 예:**
	getUser();

### 3. 검색가능한 이름을 사용하세요

우리는 작성할 코드보다 ==읽을 코드가 더 많습니다==(원인). 그렇기 때문에 ==코드를 읽기 쉽고 검색 가능하게 작성==(결과)해야 합니다. 그렇지 않으면 여러분의 코드를 이해하려고 하는 사람들에게 큰 어려움을 줍니다. 검색가능한 이름으로 만드세요. [buddy.js](https://github.com/danielstjules/buddy.js) 그리고 [ESLint](https://github.com/eslint/eslint/blob/660e0918933e6e7fede26bc675a0763a6b357c94/docs/rules/no-magic-numbers.md) 와 같은 도구들이 이름이 정해져있지 않은 상수들을 발견하고 고칠 수 있게 도와줍니다.

**안좋은 예:**
```jsx
// 대체 86400000 무엇을 의미하는 걸까요?
setTimeout(blastOff, 86400000);
```

**좋은 예**
```jsx
// 대문자로 `const` 전역 변수를 선언하세요
const MILLISECONDS_IN_A_DAY = 86400000;
setTimeout(blastOff, MILLISECONDS_IN_A_DAY);
```

### 4. 의도를 나타내는 변수들을 사용하세요

**안좋은 예:**
```jsx
const address = 'One Infinite Loop, Cupertino 95014';
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
saveCityZipCode(address.match(cityZipCodeRegex)[1], address.match(cityZipCodeRegex)[2]);
```

**좋은 예:**
```jsx
const address = 'One Infinite Loop, Cupertino 95014';
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
const [, city, zipCode] = address.match(cityZipCodeRegex) || [];
saveCityZipCode(city, zipCode);
```

### 5. 자신만 알아볼 수 있는 작명을 피하세요
![[스크린샷 2022-09-19 오후 9.06.17.png]]


### 6.문맥상 필요없는 것들을 쓰지 마세요

**안좋은 예:**
```jsx
const Car = {
  carMake: 'BMW',
  carModel: 'M3',
  carColor: '파란색'
};

function paintCar(car) {
  car.carColor = '빨간색';
}
```

**좋은 예:**
``` jsx
const Car = {
  make: 'BMW',
  model: 'M3',
  color: '파란색'
};

function paintCar(car) {
  car.color = '빨간색';
}
```


### 7. 기본 매개변수가 short circuiting 트릭이나 조건문 보다 깔끔합니다

기본 매개변수는 종종 [[short circuiting 트릭]]보다 깔끔합니다. 기본 매개변수는 매개변수가 `undefined`일때만 적용됩니다. `''`, `""`, `false`, `null`, `0`, `NaN` 같은 `falsy`한 값들은 기본 매개변수가 적용되지 않습니다.


### 생각의 연결고리
분야 :

키워드 :

관련있는 메모 : [[클린코드 MOC]]
