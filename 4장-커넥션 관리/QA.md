# 질의응답
## (찬규) keep alive속성을 잘못사용하면 어떻게 될까?
- 적절한 타임아웃을 설정하지 않으면 유휴 연결이 많아진다.
- 서버자원이 고갈된다
- 로드 밸런싱에 문제가 생긴다

<br/>

## (민지) Keep-alive 를 쓰는 곳이 많아서 계속 지원해야 한다면 왜 제외됐을까? 
- keep-alive 란?
  <br/>http 와 tcp 에서 지속 커넥션을 유지하기 위헤 제공되는 옵션 

- keep-alive 도입 배경
  <br/>http/1.0에서는 한번의 request에 대한 하나의 response 을 보내고 http 커넥션 종료
  <br/>전송할 데이터가 많아지면서 비효율적이라고 인지됨
  <br/>http/1.0+ 부터 keep-alive 옵션 추가 

- http/1.1 표준으로 선택 받지 못한 이유
<br/>네트워크 중간중간에 위치한 http/1.0+ 를 지원하지 않는 멍청한 프록시(dumb proxy) 때문
<br/>멍청한 프록시는 keep-alive의 의미를 이해하지못하고 클라이언트와 서버에게 요청/응답을 전달함. 따라서 프록시는 서버가 연결을 끊을 것을 대기하다가 클라이언트의 요청을 무시하는 상황이 생길 수 있음.
<br/> 이럴 경우 서버나 클라이언트에서 타임아웃으로 인해 커넥션이 끊기길 기다려야함 

- 단, keep-alive 가 표준이 되지 않는다는 것이 지속 커넥션을 제공하지 않는다는 의미가 아님.
<br/>http/1.1 부턴 keep-alive 를 포함하지 않아도 모든 커넥션이 하나의 tcp 연결 위에서 이루어지는 keep-alive 상태임
<br/>단 하위 호환성을 보장해주기 위해 http/1.0 이 request를 keep-alive 로 보내는 경우 response에 keep-alive 를 사용해 보내주시도 하는 등 지원이 필요함

### 🧐 병렬커넥션은 언제부터 적용되었는가?
- HTTP/1.1부터라고 보면 좋을듯.

<br/>

## (연진) HTTP에서 헤더가 누락되면 어떻게 처리될까?
브라우저의 헤더 Content-Type 유추 기능(MIME sniffing)
브라우저가 자동으로 이러한 헤더를 유추할 수 있기 때문에, 별도의 헤더 설정이 없어도 제대로 동작한다.
하지만, 모든 브라우저에서 동작하지 않을 수 있으며, 예측하지 못하는 결과를 가져올 수도 있기 때문에 명시해주는 것이 안전하다.

<br/>

## (해찬) '우아하게 커넥션 끊기'는 오역?
- 커넥션이 갑작스럽게 끊김으로서 종료된 커넥션에 데이터를 전송하는 경우를 방지하는 목적.<br/>
- graceful close가 우아한 종료가 아니라 유예된, 깔끔한 종료(abortive close의 반대 개념)를 오역한 것이라는 [지적](https://sunyzero.tistory.com/269)이 있다.<br/><br/>
