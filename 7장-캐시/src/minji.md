# 질문
## max-age=0 과 no-cache 를 이용하는 것의 차이
* 원본 서버에 유효성 검사를 수행하게 만든다는 점에서, 실제 동작 자체는 매우 유사
실제로 대부분의 브라우저에서 동일한 뜻을 가짐([toss tech](https://toss.tech/article/smart-web-service-cache))
* HTTP/1.0에는 no-cache 가 없었기 때문에 max-age=0 을 이용하곤 했었음
* ```Cache-Control: max-age=0, must-revalidate``` == ```Cache-Control: no-cache```([MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control))
max-age=0 은 캐시가 원서버와 연결이 끊겼을 때 stale response 를 발생시킬 수 있음. 따라서 must-revalidate 를 붙여야만 no-cache 와 같아지는 것


## 만약 Cache-Control: only-if-cached 인데 캐시에 사본이 없으면 어떻게 될까?
* 캐시에 사본이 없다면 네트워크 요청을 시도하지 않음 
* 요청이 실패했다고 응답하며 일반적으로는 504 Gateway Timeout 상태 코드가 반환됨
* 네트워크 요청을 시도하지 않으므로 오프라인 모드에서 유용하게 쓰일 수 있음