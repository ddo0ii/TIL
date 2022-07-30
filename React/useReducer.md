# 6-14. 복잡한 상태변화 로직분리 (useReducer)

### React/한입 크기로 잘라 먹는 리액트(React.js)

<br><br><br><br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbzMYqJ%2FbtrGJGGJepX%2FpKDxMaOniyW7qT1vIqPSdk%2Fimg.png)

상태변화 로직을 가진 것들은 app component들이었다. 이들은 굉장히 길었었는데 많은 상태변화 처리함수들이 존재했었다.

이들은 컴포넌트 내에만 존재해야 했으며 - 그 이유는 상태를 업데이트 하기 위해서는 상태변화를 참조했어야했기 때문이다. (const에 존재하는 data를 onCreate, onEdit, onRemove에서 써야했기 때문에)

컴포넌트가 길어지고 무거워지는것은 좋지 않다.
그래서 이 복잡한 컴포넌트들을 바깥으로 분리해보는 방법을 한번 알아보자

<br><br>
**useReducer - 컴포넌트에서 상태변화 로직을 분리하자.**

먼저 useSate로 1부터 10000까지 더할 수 있는 Counter를 만들어보았다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUEUHh%2FbtrGHkYOHIr%2FPfkduYIN63x5mgYSl7FVsK%2Fimg.png)

useState를 사용하면 각각 count를 사용하여 다 만들어야했다. 이렇게 하니 component가 길어지고 복잡해지기만 한다.

그래서 useReducer를 사용하게 된다면
reducer라는 함수를 컴포넌트 바깥으로 분리하여 다양한 상태변화로직을 컴포넌트 외부로 분리하여 switch case 문법처럼 편하게 처리할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F1F7yx%2FbtrGKRHjnCT%2FGROMKuxwUh2PVvgmJIVHuk%2Fimg.png)

useReducer는 useSate를 대체할 수 있는 기능

<br><br>

useSate처럼 배열(const [count, dispatch])을 만들어내고 비구조화 할당(const Counter = () => {})을 통해서 사용한다.

```js
const [count, dispatch] = useReducer(reducer, 1);
```

0번째 index(count)는 state이다. 그래서 useState처럼 {count} 이렇게 사용할 수 있다.

1번째 index(dispatch)는 상태를 변화시키는 액션을 발생시키는 함수

useReducer를 사용할때에는 reducer 함수를 꼭 전달해야한다.

dispatch가 상태변화를 일으키는데 이 reducer가 처리해준다고 생각하면 된다.

여기서 두번째로 전달하는 인자는 count state의 초기 값이 된다.

그래서 count의 초기값은 1이며 이를 변화시키고 싶다면 counter의 상태변화함수인 dispatch를 호출하면 상태변화 reducer가 처리하게 된다.

여기서 button을 누르면 type이라는 property를 전달하게 되는데, 이때 dispatch와 같이 전달 되는 이것을 Action(상태변화) 객체라고 칭한다. 그래서 상태변화를 설명할 객체라고 생각하면 된다.

그래서 이 dispatch는 reducer로 나가게 된다.

reducer가 호출되면 상태변화가 일어나고 상태변화에 대한 처리는 reducer가 진행한다.

그래서 add1을 클릭하면

const [count,~~~ = useReducer(reducer, 1)에의해 state는 1이 되고, action은 type:1이 된다.

reducer함수를 보면, type에 따라 return 값을 내고 있음을 확인할 수 있다.

반환하는 것은 새로운 state가 된다.

그럼이제 복잡한 상태변화로직을 App컴포넌트로부터 독립시켜보자.

일기 데이터 상태변화 로직을 한번 분리시켜보자.

먼저 useState를 주석처리 해주어야한다. (useReducer를 사용할 것이기 때문에)

그렇게 아래와 같이 useReducer를 추가해준다.(import에도 추가해주길 바란다.)

```js
const [data, dispatch] = useReducer();
```

배열의 0번째 인자는 state(data), 1번째는 무조건 dispatch로 지정해야한다.

useReducer는 react의 hooks이기 때문에 import를 해야한다.

```js
import { useCallback, useMemo, useEffect, useRef, useReducer } from "react";
```

여기서 useState는 사용하지 않으니 제거해주면 된다.

useReducer에서는 두개의 인자를 전달해야하는데,

첫번째는 상태변화를 처리하는 함수인 reducer

두번째는 데이터 state의 초기값을 전달해주는 빈배열을 먼저 전달해보겠다.

```js
const [data, dispatch] = useReducer(reducer, []);
```

reducer는 두개의 파라미터를 받는데

첫번째는 상태변화가 일어나기 직전의 state

두번째는 어떤 상태변화들이 일어나야하는지에 대한 정보가 담겨져 있는 action 객체

그래서 여기에서는 action 객체에 담겨있는 type을 통해서 switch문으로 한번 상태변화를 처리해보자.

여기서 기억해야하는 것은 **reducer가 반환하는 값이 새로운 상태의 값**이다!

**(dispatch를 호출하면 reducer가 실행되고, reducer가 return 하는 값이 data의 값이 된다!)**

<br><br>

자 그러면 type별로 case들을 작성해 보겠다.

```js
const reducer = (state, action) => {
  switch(action.type) {
    case 'INIT' :
    case 'CREATE' :
    case 'REMOVE' :
    case 'EDIT' :
    // 상태변화가 일어났는데 상태가 안변하면 안되니까.
    // default로! 상태를 변화시키지 않는다.(그대로 state를 반환)
    default :
    return state;
  }
```

각각 INIT, CREATE, REMOVE, EDIT의 CASE가 있었고,

마지막으로 DEFAULT 조건을 내주었는데 이는 상태변화가 일어났는데 상태가 안변하면 안되니까 DEFAULT로 설정하는 방법이다. 이번에는 그대로 state를 반환하여 그대로 상태를 반환하도록 설정하였다.

우선 initData로 데이터를 초기화해야하니 아래와 같이 코드를 작성하였다.

action의 type은 INIT이고 action에 필요한 데이터는 initData가 되는것이다

```js
//setData는 reducer함수가 하기 때문에 지워도 된다.
// action의 type은 INIT이고 action에 필요한 데이터는 initData가 되는것이다
dispatch({ type: "INIT", data: initData });
```

자 그럼 이제 INIT일때 적절한 state로 변화시켜줄 코드를 작성해 보겠다.

```js
switch(action.type) {
    case 'INIT' : {
      return action.data
    }
```

왜 action.data일까?

방금 위에서 data에 initData를 넣었기 때문에 reducer에서는 action객체는 data프로퍼티를 꺼내어 그 값을 꺼내 주면 이 값이 새로운 state가 되는 것이다.

다음으로 CREATE는 다음과 같이 정의하였다.

```js
case 'CREATE': {
      // created_date는 받지 못했기에 새로 선언해준다
      const created_date = new Date().getTime();
      const newItem = {
        ...action.data,
        created_date
      }
      return [newItem, ...state]
    }

const onCreate = useCallback((author, content, emotion) => {
  // data는 newItem에 있는 것을 그대로 들고와서 쓰면된다
    dispatch({type:'CREATE', data:{author, content, emotion, id: dataId.current}})
    dataId.current += 1;
  }, []);
```

REMOVE는 다음과 같이 정의하였다.

```js
    case 'REMOVE': {
      // targetId가 action.targetId가 아닌 애들만 filter하여 새로운 state를 전달해주면 된다.
      return state.filter((it)=> it.id !== action.targetId)
    }

const onRemove = useCallback((targetId) => {
    dispatch({type: "REMOVE", targetId})
  }, []);
```

EDIT은 다음과 같이 정의하였다.

```js
    case 'EDIT': {
      // state.map((it) => it.id === action.targetId?는 수정하고자 하는 targetId를 만난것이다
      // ...it은 원래 객체 값을 넣어준 다음에 content값만 action.newContent로 넣어주면 된다
      // it은 그렇게 하고 원하는 값이 아니라면 그대로 반환해 주면된다
      return state.map((it) => it.id === action.targetId? {...it, content:action.newContent} : it)
    }

const onEdit = useCallback((targetId, newContent) => {
    dispatch({type:"EDIT", targetId, newContent})
  }, []);
```

<br><br><br><br>

**전체 코드(App.js)**

```js
import { useCallback, useMemo, useEffect, useRef, useReducer } from "react";
import "./App.css";
import DiaryEditor from "./DiaryEditor";
import DiaryList from "./DiaryList";

// useReducer를 사용하는 이유는 복잡한 컴포넌트를 밖으로 내보내기 위해 사용한다.
// 그래서 component 밖에 둔다.
const reducer = (state, action) => {
  // switch를 이용하여 상태변화를 다르게 한다.
  // reducer가 반환하는 값이 data의 값이 된다.
  switch (action.type) {
    case "INIT": {
      return action.data;
    }
    case "CREATE": {
      // created_date는 받지 못했기에 새로 선언해준다
      const created_date = new Date().getTime();
      const newItem = {
        ...action.data,
        created_date,
      };
      return [newItem, ...state];
    }
    case "REMOVE": {
      // targetId가 action.targetId가 아닌 애들만 filter하여 새로운 state를 전달해주면 된다.
      return state.filter((it) => it.id !== action.targetId);
    }
    case "EDIT": {
      // state.map((it) => it.id === action.targetId?는 수정하고자 하는 targetId를 만난것이다
      // ...it은 원래 객체 값을 넣어준 다음에 content값만 action.newContent로 넣어주면 된다
      // it은 그렇게 하고 원하는 값이 아니라면 그대로 반환해 주면된다
      return state.map((it) =>
        it.id === action.targetId ? { ...it, content: action.newContent } : it
      );
    }
    // 상태변화가 일어났는데 상태가 안변하면 안되니까.
    // default로! 상태를 변화시키지 않는다.(그대로 state를 반환)
    default:
      return state;
  }
};

const App = () => {
  // 전역적으로 Data 관리할 state
  // const [data, setData] = useState([]);

  const [data, dispatch] = useReducer(reducer, []);

  const dataId = useRef(0);
  // data 호출
  const getData = async () => {
    const res = await fetch(
      "https://jsonplaceholder.typicode.com/comments"
    ).then((res) => res.json());

    const initData = res.slice(0, 20).map((it) => {
      return {
        author: it.email,
        content: it.body,
        emotion: Math.floor(Math.random() * 5) + 1,
        created_date: new Date().getTime(),
        id: dataId.current++,
      };
    });
    //setData는 reducer함수가 하기 때문에 지워도 된다.
    // action의 type은 INIT이고 action에 필요한 데이터는 initData가 되는것이다
    dispatch({ type: "INIT", data: initData });
  };

  // App component가 mount 되자마자 호출해보자
  // 빈배열 함수를 전달하면 바로 콜백함수를 마운트 되는 시점에 실행되게 된다.
  // getData()로 API 호출
  useEffect(() => {
    getData();
  }, []);

  // useCallback사용
  const onCreate = useCallback((author, content, emotion) => {
    // data는 newItem에 있는 것을 그대로 들고와서 쓰면된다
    dispatch({
      type: "CREATE",
      data: { author, content, emotion, id: dataId.current },
    });
    dataId.current += 1;
  }, []);

  const onRemove = useCallback((targetId) => {
    dispatch({ type: "REMOVE", targetId });
  }, []);

  const onEdit = useCallback((targetId, newContent) => {
    dispatch({ type: "EDIT", targetId, newContent });
  }, []);

  // Memoization
  const getDiaryAnalysis = useMemo(() => {
    if (data.length === 0) {
      return { goodcount: 0, badCount: 0, goodRatio: 0 };
    }

    const goodCount = data.filter((it) => it.emotion >= 3).length;
    const badCount = data.length - goodCount;
    const goodRatio = (goodCount / data.length) * 100;
    return { goodCount, badCount, goodRatio };
  }, [data.length]);

  const { goodCount, badCount, goodRatio } = getDiaryAnalysis;

  return (
    <div className="App">
      <DiaryEditor onCreate={onCreate} />
      <div>전체 일기 : {data.length}</div>
      <div>기분 좋은 일기 개수 : {goodCount}</div>
      <div>기분 나쁜 일기 개수 : {badCount}</div>
      <div>기분 좋은 일기 비율 : {goodRatio}</div>
      <DiaryList onEdit={onEdit} onRemove={onRemove} diaryList={data} />
    </div>
  );
};

export default App;
```

이렇게 하여 모든 INIT, CREATE, REMOVE, EDIT (띄우기, 새로운 글 작성, 지우기, 수정하기)가 useReducer로 모두 잘 작동되는 것을 확인할 수 있다.

여기서 잠깐!

dispatch(상태변화 발생시키는 함수)는 함수형 업데이트 필요 없이, 호출하면 현재 state를 reducer함수가 참조하여 자동으로 변경시켜 useCallback을 사용하여도 dependency array( ' [ ] ' 과 같은 것들)를 걱정하지 않아도 된다.

자 그럼 복잡한 상태 관리 로직을 component로부터 분할시켜 보았다.
