# 원티드 프리온보딩 프론트엔드 - Week 3-1

원티드 프리온보딩 **프론트엔드 8팀**의 ```팔팔한 형제들```입니다.<br>

## 📅 프로젝트 기간

기간 : 2022년 11월 9일 ~ 2022년 11월 12일

## 팔팔한 형제들 팀 소개
### FE
<table>
  <tr>
    <td>
        <a href="https://github.com/CodyMan0">            
	    <img src="https://avatars.githubusercontent.com/u/93697790?v=4" width="100px" />
        </a>
    </td>
    <td>
        <a href="https://github.com/shimeeuisuk">
            <img src="https://avatars.githubusercontent.com/u/104304569?v=4" width="100px" />
        </a>
    </td>
    <td>
        <a href="https://github.com/jangth0655"> 
            <img src="https://avatars.githubusercontent.com/u/83333409?v=4" width="100px" />
        </a>
    </td>
    <td>
        <a href="https://github.com/choi2021">
	    <img src="https://avatars.githubusercontent.com/u/80830981?v=4" width="100px" />
        </a>
    </td>
    <td>
        <a href="https://github.com/strongsongky">
	    <img src="https://avatars.githubusercontent.com/u/102295416?v=4" width="100px" />
        </a>
    </td>
    <td>
        <a href="https://github.com/gywn9708">
	    <img src="https://avatars.githubusercontent.com/u/107469939?v=4" width="100px" />
        </a>
    </td>
    <td>
        <a href="https://github.com/YongHyunKwon">
	    <img src="https://avatars.githubusercontent.com/u/13326980?v=4" width="100px" />
        </a>
    </td>
  </tr>
  <tr>
    <td><b>이주영(팀장)</b></td>
    <td><b>심의석(부팀장)</b></td>
    <td><b>장태희</b></td>
    <td><b>최영준</b></td>
    <td><b>송경용(공지)</b></td>
    <td><b>강효주</b></td>
    <td><b>권용현</b></td>
  </tr>
  <tr>
    <td><b>Front-End</b></td>
    <td><b>Front-End</b></td>
    <td><b>Front-End</b></td>
    <td><b>Front-End</b></td>
    <td><b>Front-End</b></td>
    <td><b>Front-End</b></td>
    <td><b>Front-End</b></td>
  </tr>
</table>


## 🛠 기술 스택

<div align=left> 
  <img src="https://img.shields.io/badge/html5-E34F26?style=for-the-badge&logo=html5&logoColor=white"> 
  <img src="https://img.shields.io/badge/css-1572B6?style=for-the-badge&logo=css3&logoColor=white"> 
  <img src="https://img.shields.io/badge/typescript-1572B6?style=for-the-badge&logo=typescript&logoColor=white">
  <img src="https://img.shields.io/badge/react-61DAFB?style=for-the-badge&logo=react&logoColor=black"> 
  <img src="https://img.shields.io/badge/styled_components-DB7093?style=for-the-badge&logo=styled-components&logoColor=white"> 
  <br>
  
  <img src="https://img.shields.io/badge/vs_code-007ACC?style=for-the-badge&logo=visualstudiocode&logoColor=white">
  <img src="https://img.shields.io/badge/react_router_dom-CA4245?style=for-the-badge&logo=reactrouter&logoColor=white">
  <br>
 
  <img src="https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white">
  <img src="https://img.shields.io/badge/git-F05032?style=for-the-badge&logo=git&logoColor=white">
  <img src="https://img.shields.io/badge/slack-4A154B?style=for-the-badge&logo=slack&logoColor=white">
  <br>
</div>




## 🏁 프로젝트 실행 방법


1. 의존성 패키지를 설치합니다.
```zsh
$ npm install
```
2. 리눅스와 윈도우 husky 충돌 방지 후 사용을 위해 설치합니다. 
```zsh
$ chmod ug+x .husky/* 
```
3. 프로젝트를 실행합니다.
```zsh
$ npm start
```


## 👍 Best Practice 선정 이유

- API 호출별로 로컬 캐싱 구현
  - **코드** :
  ```tsx
  export default class CacheService {
    static setData = (query: string, words: SearchType[]) => {
      const stringifyWord = JSON.stringify(words);
      sessionStorage.setItem(query, stringifyWord);
     };

    static getData = (query: string) => {
      const data = sessionStorage.getItem(query);
      const parsedData: SearchType[] = JSON.parse(data || JSON.stringify([]));
      return parsedData;
    };
   }

  ```
  - **이 기술을 사용한 이유** : 
    로컬 캐싱을 할 수 있는 방법으로는 **HTTP cache-control**, **local Storage**, **Session Storage** 세가지에 대해서 고려했고,
    저희 팀이 선택한 방법은 **Session Storage**입니다. HTTP cache-control은 api호출 후에 받아온 데이터를 저장한 후에 이후 같은 데이터의 경우 새로 api를 호출하는 것이 아니라,
    cache되어 있는 데이터를 가져올 수 있는 방법으로, 서버 데이터의 변화를 알 수 있지만, 서버의 응답이 모두 동일하게 200 OK로 들어와 cache된 데이터인지 확인하기 어려웠습니다.
    local storage와 session storage를 이용한 방식은 모두 브라우저의 storage로 api 호출로 받아온 데이터를 브라우저에 저장하는 방식입니다. 
    서버의 데이터를 브라우저로 가져와서 저장하다보니 **서버의 데이터 변화를 알 수 없는 단점**이 있습니다. 그렇기 때문에 브라우저에 닫아도 계속해서 저장하는 local storage가 아니라
    브라우저를 닫으면 저장된 데이터를 초기화하고, 새로운 api 호출을 하는 *session storage*를 이용해 서버 데이터의 변화를 어느정도 반영하면서 로컬에 데이터를 저장했습니다.

- 입력마다 API 호출하지 않도록 API 호출 횟수를 줄이는 전략 수립 및 실행 (디바운스)

  - 코드 :
  ```tsx
  const debounce = setTimeout(() => {
      getResponse();
      }, DELAY_TIME);
    return () => clearTimeout(debounce);
  ```
  - **이 기술을 사용한 이유** : 사용자가 키보드를 연속적으로 입력한다면, 이는 자신의 검색할 단어를 아직 다 입력하지 않았다는 뜻입니다. 따라서, 사용자가 의도한 단어 입력을 완료하지 않은 상태에서 굳이 자동완성의 결과를 매번 보여줄 필요가 없습니다. 이를 고려하지 않는다면, 사용자가 특정 문자열을 입력할 때마다 매번 api 호출이 이루어지기 때문에 이는 리소스 낭비가 될 수 있습니다.
따라서 저희 팀은 사용자가 입력을 마쳤을 때 api호출이 되도록 제어하는 debounce 함수를 만들어 이를 해결하였습니다.
debounce 함수는 callback함수와 delayTime을 인자로 전달 받는데, delayTime만큼 지연되지 않았을 경우 전에 등록했던 setTimeout을 지우고 새로 setTimeout을 등록함으로서 callback함수의 실행을 지연시키는 함수를 반환합니다. 이를 이용하여, 최종 입력이 완료될때까지 자동완성이 보이지 않고, 모든 입력이 완료된 이후에 자동완성 결과를 보여줌으로서 매번 api호출을 하지 않아 **리소스를 절약**할 수 있었습니다.
 

- 키보드만으로 추천 검색어들로 이동 가능하도록 구현
  - 코드 : 
  ```tsx
  import { useState, useEffect } from 'react';

  type KeyType = 'ArrowDown' | 'ArrowUp' | 'Enter';

  const useKeyPress = (targetKey: KeyType) => {
  
  const [keyPressed, setKeyPressed] = useState(false);

  const downHandler = (event: KeyboardEvent) => {
    const { key } = event;
    if (key === targetKey) {
      setKeyPressed(true);
      }
    };

  const upHandler = (event: KeyboardEvent) => {
    const { key } = event;
    if (key === targetKey) {
      setKeyPressed(false);
      }
    };
    
  useEffect(() => {
    window.addEventListener('keydown', downHandler);
    window.addEventListener('keyup', upHandler);

    return () => {
      window.removeEventListener('keydown', downHandler);
      window.removeEventListener('keyup', upHandler);
     };
   });

  return keyPressed;
  };

  export { useKeyPress };
  ```
  - **이 기술을 사용한 이유** : 키보드만으로 추천검색어들로 이동하기 위해 저희 팀은 추천 검색어 리스트 배열의 index와 keydown, keyup event를 이용했습니다. window의 keydown,keyup Event를 사용해 화면에서 방향키를 눌러 바로 추천검색어 리스트로 이동이 가능합니다. 변화된 index에 따라 해당 searchItem 컴포넌트의 배경색을 변화시켜 현재 위치를 UI로 알 수 있게 했고, 추천 검색어 리스트 배열의 자료 양이 많아지면 scroll이 생기고 container 크기 밖의  item이 보이지 않을 수 있어 element.scrollIntoView 메소드를 이용해 해당 아이템의 위치로 자동으로 스크롤이 될 수 있게 했습니다.

- **URL의 쿼리스트링을 활용한 전역 상태 관리**
  - **코드** 
  ```tsx
  import { useSearchParams } from 'react-router-dom';

  const useQueryString = () => {
  const [params] = useSearchParams();
  const query = params.get('q') || '';
    return query;
  };

  export { useQueryString };
  ```
  - **이 기술을 사용한 이유** : url의 쿼리스트링과 인풋의 value를 동기화하여 전역상태관리를 했습니다. 
  


## ✏️ 개선 부분

- onMouseMove를 onMouseEnter이라는 속성으로 변경하여 불필요한 렌더링을 막아주었습니다.
  - **코드**
  ```tsx
  
  <Link to={`/search?q=${text}`}>
     <S.Wrapper ref={itemRef} active={active} onMouseEnter={handleMouseEnter}>
       <BsSearch />
       <span>
       {textArray?.map((item, idx) => {
         if (idx === KEYWORD_INDEX) {
           return <b key={item}>{item}</b>;
         }
         return item;
        })}
       </span>
     /S.Wrapper>
  </Link>
  ```
- **API 호출 endPoint 변경**
  - **코드**
  ```tsx
  async getSearch(keyword: string) {
    try {
      const { data } = await this.httpClient.get<SearchResponse>(
        `?sickNm_like=${keyword}`
      );
      console.info('calling api');
      return await data;
    } catch (error) {
      if (error instanceof AxiosError) {
        const { response } = error;
        if (response) {
          throw new HTTPError(response?.status, response?.statusText);
        }
      }
      throw new Error('Server Error');
      }
    }
  }
  ```


 


















