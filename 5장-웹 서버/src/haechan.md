## 5장 웹 서버
- HTTP 트랜잭션을 처리하는 방법<br/><br/>

### 커넥션 입력/출력 처리 아키텍처
- 고성능 웹 서버는 수천 개의 커넥션을 동시에 처리.<br/>
- 멀티 프로세스, 멀티 스레드, 멀티 플렉싱 등을 사용한다.<br/><br/>

### 멀티 플렉싱은 어떻게 진행될까?
- [큐를 순회하며 제한 시간동안 작업을 처리하는 방식(동시성 프로그래밍).](https://blog.naver.com/n_cloudplatform/222189669084)<br/>
- [Node.js가 싱글 스레드라는 이야기도 멀티 플렉싱을 이용한다는 이야기인 것 같다.](https://akasai.space/node-js/about_node_js_4/)<br/><br/>

### Content-Length 헤더는 왜 필요할까?
- 데이터 전송의 완료 시점을 알 수 있고(효율성), 위변조 여부 파악 및 오류 검출에 사용할 수 있다(안정성).<br/>
- 일반적으로 Content-Length 또는 소켓 종료 신호를 통해서 데이터 전송의 완료를 탐지한다고 한다.<br/>
- [Transfer-Encoding 헤더](https://blog.naver.com/claude17/221904720369)를 Chunked로 설정하면 Content-Length 헤더를 대체할 수 있다. 화면 로딩, 동적 리소스 전송 등의 경우를 위해 추가되었다고 한다.<br/><br/>

### 303(See Other) vs 307(Temporary Redirect)
- 303: 다음 요청이 Get을 통해 이루어지도록 한다. (예시 - [쇼핑몰 주문](https://m.blog.naver.com/fbfbf1/222682991444))<br/>
- 307: 다음 요청의 메서드를 강제하지 않는다.<br/><br/>
