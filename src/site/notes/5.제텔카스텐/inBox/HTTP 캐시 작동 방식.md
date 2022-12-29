브라우저가 제공하는 모든 HTTP 요청은 먼저 브라우저 캐시로 라우팅되어 요청을 수행하는 데 사용할 수 있는 유효한 캐시 응답이 있는지 확인합니다. 일치하는 항목이 있으면 캐시에서 응답을 읽어 네트워크 대기 시간과 전송으로 인해 발생하는 데이터 비용을 모두 제거합니다.

HTTP 캐시의 동작은 [요청 헤더](https://developer.mozilla.org/docs/Glossary/Request_header)와 [응답 헤더](https://developer.mozilla.org/docs/Glossary/Response_header)의 조합에 의해 제어됩니다. 

이상적인 시나리오에서는 웹 애플리케이션의 코드(요청 헤더를 결정함)와 웹 서버의 구성(응답 헤더를 결정함)을 모두 제어할 수 있습니다.

보다 심층적인 개념 개요는 MDN의 [HTTP 캐싱](https://developer.mozilla.org/docs/Web/HTTP/Caching) 기사를 확인하십시오.