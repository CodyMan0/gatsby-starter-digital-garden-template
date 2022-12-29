# Sass로 프로젝트 css를 scss 로 바꾸는 몇가지 규칙 (블로그 작성하기)

1. 변수는 Variable scss에 넣기 
2. 반복되는 것은 재활용 할 수 있도록 묶어두기
3. 묶어둔 재활용 코드를 더 우연하게 사용하기 위해서 인자를 넣어 사용할 수 있다.


발견한 것. 
``` scss

@mixin flexSort($justify, $alignItems) {

display: flex;

justify-content: $justify;

align-items: $alignItems;

};
```

위의 함수를 재사용할ㄷ때 @include를 사용하여 호출한다 여기서! 만약 나는 align-items를 넣고 싶지 않을때 인자의 기본값 설정을 통해 해결 할 수 있다는 것을 알게 됐다.

기본 값 설정은 ==$매개변수 : 기본값==으로 설정할 수 있다. 

``` scss

@mixin flexSort($justify : null, $alignItems : null) {

display: flex;

justify-content: $justify;

align-items: $alignItems;

};
```

이렇게 해놓으면 필요한 곳에만 인자를 넣어서 사용할 수 있고 필요없는곳에서는 호출한 함수의 인자를 넣을 필요가 없어진다.  해결!!!

### 연결문서
- 
