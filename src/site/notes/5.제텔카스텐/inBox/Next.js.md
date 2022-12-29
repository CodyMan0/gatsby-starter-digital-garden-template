---
aliases: []
tags : 
---
Up : [[HOME 🌎]]

출처 :
저자 :
URL : https://www.youtube.com/watch?v=ECMB4kUCKWQ&t=448s
인용 : 

react + express.js + react-router-dome + serverSide-rendering

-> 모든 애들의 개념을 내재화해서 쉽게 사용할 수 있다.

### Code splitting and prefetching을 자동으로 해준다는데? 




8번쨰 세션
```js
const pages: Record<string, { default: React.ElementType }> = import.meta.glob( "./pages/*.tsx", { eager: true } ); 

const routes = Object.keys(pages).map((path) => {
const name = path.match(/\.\/pages\/(.*)\.tsx/)?.[1] ?? ""; return { 
name,
path: `/${name === "index" ? "" : name}`,
component: pages[path].default, 
	};
 }); 
 
 const container = document.getElementById("root") as HTMLElement;
 
ReactDOM.createRoot(container).render(
<Router> {routes.map(({ path, component: Component }) => ( <Route key={path} path={path} component={<Component />} /> ))} </Router> 
);
```


넥스트는 자동으로 번들 사이즈를 GGB로 압축해준다.

[[next.Image 전격 해부]]




### 생각의 연결고리
분야 : [[프레임워크와 라이브러리의 차이]]

키워드 :

관련있는 메모 :
