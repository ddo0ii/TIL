# ⚡️ Side Effect

## ❗️Side Effect (부수 효과)

- **함수 내에서 어떤 구현이 함수 외부에 영향을 끼치는 경우 해당 함수는 Side Effect가 있다**고 이야기한다.
- 다음은, 전역 변수 a를 sampleFn라는 함수가 수정하는 예제이다.

```js
let a = "hello";

function sampleFn() {
  a = "world";
}

sampleFn(); // sampleFn는 Side Effect를 발생시킨다.
```

## ❗️Pure Function (순수 함수)

- **순수 함수**란, 오직 **함수의 입력만이 함수의 결과에 영향**을 주는 함수를 의미한다.
- **순수 함수**에는 **네트워크 요청**과 같은 **Side Effect가 없다**.
- **순수 함수**는 **입력으로 전달된 값을 수정하지 않는다.**
- **순수 함수**는 **동일한 전달 인자**가 주어질 경우, **항상 똑같은 값이 리턴됨**을 보장한다.
- 그래서 **예측 가능한 함수**이기도 하다.
- 함수의 입력이 아닌 다른 값이 함수의 결과에 영향을 미치는 경우, 순수 함수라고 부를 수 없다.

```js
function sampleFn(str) {
  // toUpperCase 메소드는 원본을 수정하지 않는다. (Immutable)
  return str.toUpperCase();
}

sampleFn("hanamon"); // 'HANAMON'
```

## ❗️React 컴포넌트에서의 Side Effect

- React 애플리케이션을 작성할 때에는 AJAX 요청이 필요하거나, LocalStorage 또는 타이머와 같은
  React와 상관없는 API를 사용하는 경우가 발생할 수 있다.
- 이는 **React의 입장에서는 전부 Side Effect** 이다.

#### React는 Side Effect를 다루기 위한 Hook인 Effect Hook을 제공한다.

- 타이머 사용 (setTimeout)
- 데이터 가져오기 (fetch API, localStorage)

[출처](https://hanamon.kr/codestates-til-%ED%95%AD%ED%95%B4%EC%9D%BC%EC%A7%80-35%EC%9D%BC%EC%B0%A8/)
