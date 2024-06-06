### Proxy의 Max-forward 동작 원리

- 클라이언트는 HTTP 요청을 프록시 서버에 보낼 때 `Max-Forward` 헤더를 포함.
- 각 프록시 서버는 요청을 받을 때마다 `Max-Forward` 값을 1씩 감소.
- `Max-Forward` 값이 0이 되면, 해당 프록시 서버는 더 이상 요청을 전달하지 않고, 대신 자체적으로 요청에 대한 응답을 생성.
