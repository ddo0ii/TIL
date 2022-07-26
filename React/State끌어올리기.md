# ⚡️ State 끌어올리기 (Lifting State Up)

- 단방향 데이터 흐름이라는 원칙에 따라, 하위 컴포넌트는 상위 컴포넌트로부터 전달받은 데이터의 형태 혹은 타입이 무엇인지만 알 수 있다.
- 데이터가 state로부터 왔는지, 하드코딩으로 입력한 내용인지는 알지 못한다.
- 그러므로 하위 컴포넌트에서의 어떤 이벤트로 인해 상위 컴포넌트의 상태가 바뀌는 것은 마치 “역방향 - 데이터 흐름”과 같이 조금 이상하게 들릴 수 있다.
- React가 제시하는 해결책은 다음과 같습니다.

### 상위 컴포넌트의 “상태를 변경하는 함수” 그 자체를 하위 컴포넌트로 전달하고,

### 이 함수를 하위 컴포넌트가 실행한다.

- 여전히 단방향 데이터 흐름에 원칙에 부합하는 해결방법이다.
- 바로 이것이 “상태 끌어올리기”이다.

[참고 : State 끌어올리기 – React](https://ko.reactjs.org/docs/lifting-state-up.html)

[출처](https://hanamon.kr/codestates-til-%ED%95%AD%ED%95%B4%EC%9D%BC%EC%A7%80-35%EC%9D%BC%EC%B0%A8/)
https://hanamon.kr/codestates-til-%ED%95%AD%ED%95%B4%EC%9D%BC%EC%A7%80-35%EC%9D%BC%EC%B0%A8/
