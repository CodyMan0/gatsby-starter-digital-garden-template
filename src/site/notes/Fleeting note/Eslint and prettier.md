ESLint와 Prettier를 설치하는 몇 가지 방법이 있습니다.

크게 VS Code Extention과 NPM Package로 설치하는 방법입니다. 팀원 각자 모두 설치함으로써 동일한 개발환경으로 구성 후 작업하면 프로젝트 진행 시 편리합니다.

**다음과 같은 이유로 Extention과 NPM Package로 모두 설치할 것을 권장합니다.**

-   ==ESLint에게 linting==을, ==Prettier에게 code formating==을 전담시키기 위해서 eslint-plugin-prettier, eslint-config-prettier를 함께 설치해서 사용할 것 (eslint formatting rules와 prettier rules가 충돌하기 때문, 공식 문서에서도 권장하는 방식)을 권장합니다.
-   ==.eslintrc, .prettierrc 등의 설정파일을 활용==하기 위해
-   VS Code에서 코드를 입력할 때 ==실시간으로 수정사항을 코드에 반영==받기 위해 (원래 터미널 명령어로 작동하는 방식)

다만, CRA(create-react-app)로 시작할 경우 package.json에서 확인할 수 있듯 ==ESLint는 기본적으로 설치되어야 합니다.==




1.  **User**
    
    말 그대로 설정의 범위가 VS Code를 사용하는 로컬 유저가 됩니다. 즉, User로 설정한 값들은 모든 Workspace에 적용되지만, 다른 환경(ex. 해당 프로젝트를 clone 받은 다른 사용자)에는 적용되지 않게 됩니다.
    
2.  **Workplace (.vscode/settings.json)**
    
    프로젝트 루트 경로에 .vscode 라는 폴더를 생성하고 settings.json을 해당 폴더 안에 생성합니다. 이 파일에 작성한 내용으로부터 VS Code에 관한 설정을 적용받습니다. 즉, 이 폴더가 git에 함께 업로드 된다면, 이 파일이 포함된 프로젝트 폴더에서 작업을 하는 사용자는 해당 workplace에 대하여 .vscode/settings.json 에 작성된 값에 따른 동일한 설정을 적용 받을 수 있다는 뜻입니다. 다만, 여기에 포함되는 설정은 eslint/prettier 관련 설정에 국한되지 않습니다. 예컨대 tap width나 terminal 관련한 설정 또한 포함되어 다른 팀원들의 에디터에 영향을 미칠 수 있으므로 주의가 필요합니다. 이러한 이유로 사용할 예정이라면 컨벤션에 맞는 내용을 작성해 사용하고, 그렇지 않을 예정이라면 .gitignore 에 추가해둘 것을 권장합니다.


## 2-2. npm 패키지

`$ npm install -D prettier eslint-config-prettier eslint-plugin-prettier`

CRA에는 eslint가 내장되어있기에 eslint는 추가설치할 필요가 없습니다. 따라서, eslint 추가 설정을 위한 패키지만 설치해추고 ==package.json의 devDependencies에 추가가 되어있는지 확인==해주세요.  
  

**[참고]** **dependencies vs devDependencies**

프로젝트에 필요한 외부 패키지들은 ==package.json==에 담겨야 합니다. 이유는 잘 알고 있다시피 node_modules 폴더의 용량이 상당하기 때문에 다른 소스코드들과 GitHub에 함께 업로드할 수 없기 때문입니다. 따라서 npm을 기반으로 작성된 프로젝트를 Clone 받았을 때 package.json의 정보를 기반으로 필요한 의존성 들을 재구성(설치)하게 됩니다. 하지만 개발 단계(development)에서 사용되는 패키지와 프로젝트가 빌드 된 후, 실제 프로덕션 단계에서 사용되는 패키지는 다를 수 있습니다. ==eslint, prettier 등이 전자(로컬 개발 단계)에서만 사용되는 대표적인 예시==라고 할 수 있습니다. eslint, prettier 등 코드를 작성할 때 사용되는 라이브러리들은 사용자와 만날 이유가 없고, build 할 때는 의존성에서 제외함으로써 최종 결과물의 크기를 줄일 수 있습니다.

## 3. 추천 세팅

다양한 설정파일이 존재할 때에는 차례대로 적용한 뒤 마지막에 적용되는 설정이 최종적으로 적용되기 때문에 ==settings.json → .editorconfig → .prettierrc 순서==로 설정이 적용됩니다. 아래 설정들은 자동으로 포맷팅 하기 위한 최소한의 사항일 뿐이기 때문에 **팀 컨벤션에 따라 원하는 옵션을 추가하거나, 빼도 무방합니다.** 더 자세한 내용은 공식문서에 잘 나와 있으니 참고해 보세요. ==settins.json, .eslintrc, .prettierrc 파일을 아래와 같이 프로젝트 루트 폴더에 생성하고 내용을 기입하면, 프로젝트에 한해서, 해당 설정이 우선으로 적용==됩니다.

프로젝트 최상위에 .vscode 폴더를 생성하여, settings.json 파일을 만들어 아래의 코드를 입력해주세요.

```
// .vscode/settings.json

{ "editor.defaultFormatter": "esbenp.prettier-vscode", "editor.tabSize": 2,
"editor.insertSpaces": true, 
"editor.formatOnSave": true, 
"editor.codeActionsOnSave": { 
"source.fixAll.eslint": true 
}, 

"javascript.format.enable": false,
"eslint.alwaysShowStatus": true,
"files.autoSave": "onFocusChange" }
```


## 3-2. .eslintrc

프로젝트 최상위에 .eslintrc 파일을 만들어 아래의 코드를 입력해주세요. 팀원이 모두 맥 유저일 경우와, 그렇지 않은 경우의 세팅이 다르니 확인 후에 적용해주세요.

### 3-2-1. 팀원이 모두 맥 유저일 경우

```

{ "extends": ["react-app", "plugin:prettier/recommended"], "rules": { "no-var": "warn", // var 금지 "no-multiple-empty-lines": "warn", // 여러 줄 공백 금지 "no-console": ["warn", { "allow": ["warn", "error"] }], // console.log() 금지 "eqeqeq": "warn", // 일치 연산자 사용 필수 "dot-notation": "warn", // 가능하다면 dot notation 사용 "no-unused-vars": "warn", // 사용하지 않는 변수 금지 "react/destructuring-assignment": "warn", // state, prop 등에 구조분해 할당 적용 "react/jsx-pascal-case": "warn", // 컴포넌트 이름은 PascalCase로 "react/no-direct-mutation-state": "warn", // state 직접 수정 금지 "react/jsx-no-useless-fragment": "warn", // 불필요한 fragment 금지 "react/no-unused-state": "warn", // 사용되지 않는 state "react/jsx-key": "warn", // 반복문으로 생성하는 요소에 key 강제 "react/self-closing-comp": "warn", // 셀프 클로징 태그 가능하면 적용 "react/jsx-curly-brace-presence": "warn" // jsx 내 불필요한 중괄호 금지 } }
```
![[스크린샷 2022-08-03 오전 11.20.39.png]]


### 3-2-2. 팀원 중 윈도우 유저가 있을 경우![[스크린샷 2022-08-03 오전 11.20.55.png]]

##  주의 context.getPhysicalFilename is not a function 에러

eslint-plugin-prettier 설치 후 context.getPhysicalFilename is not a function 에러가 발생하는 경우가 있습니다. ==CRA에 내장된 eslint 버전은 7.28.0 인데, eslint-plugin-prettier, eslint-config-prettier에서 요구되는 eslint 버전은 7.32 이상이라서 발생하는 문제==입니다. 최신 버전의 npm(v8)은 install 시에 이런 문제를 파악하고 자동으로 업데이트 해주기 때문에 문제가 발생하지 않지만 구 버전의 npm(v6~7)의 경우에는 해결해주지 않아서 위와 같은 에러 발생하게 됩니다. 아래와 같이 npm을 업데이트하고 package를 삭제 후 재설치하는 과정을 통해서 해결할 수 있습니다.

1.  `npm install npm@latest -g`
2.  `npm -v`
3.  `npm uninstall -D eslint-config-prettier eslint-plugin-prettier`
4.  `npm install -D eslint-config-prettier eslint-plugin-prettier`