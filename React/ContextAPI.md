# 6-15. 컴포넌트 트리에 데이터 공급하기 (Context API)

### React/한입 크기로 잘라 먹는 리액트(React.js)

<br><br><br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpGdBf%2FbtrHQoqyQUN%2FigKWA6mpcG5whTTbZfX9D1%2Fimg.png)

DiaryList는 onCreate, onRemove, onEdit의  세개의 props를 받지만

빨간색같이 그냥 거쳐가기만 하는 prop들이 존재한다.(비효율적)

(onDelete라고 했다가, onRemove로 바꾸는데 굉장히 많은 시간이 든다.)

전달만 하는 컴포넌트가 많이 생길 경우에는 props이름도 바꾸기가 어려워 지고 코드 작성과 수정에 악영향을 끼친다.

이런 상황에 props가 드릴처럼 땅을 파고 들어간다고 해서 props drilling이라고도 칭한다고 한다.

이는 부모에서 자식으로 데이터를 전달하는 단방향데이터흐름을 지키는 react를 사용하다보니 발생하는 문제라고 할 수 있다.

 

이를 해결하기 위해 Context를 오늘 배울 것인데, 아이디어는 다음과 같다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FtDm6u%2FbtrHNK3edZh%2FGRQ7meHKigX4pusgLTTh8k%2Fimg.png)

<br>

1. 모든 데이터를 가지고 있는 컴포넌트가 provider라는 공격자 역할을 하는 자식 컴포넌트에게 자신이 가지고있는 모든 데이터를 준다.

2. Provider는 특별해서 자신의 자손에 해당하는 모든 컴포넌트에게 직통으로 데이터를 줄 수 있다.(props drilling이 없어졌다는 뜻)

3. Probider의 모든 자식 component들은 공급자 component에게 직통으로 공급받게 된다.

<br>

이는 번거로움을 많이 없애준다.(쓸데없이 전달만 하는 props들도 필요없고, 코드도 깔끔해지고 가독성도 좋아진다.)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcGB7X9%2FbtrHNGfk99n%2F3CgkKcc3ixec9529ewsf20%2Fimg.png)

이러한 아이디어에서 Provider 컴포넌트의 자식노드로 배치되어 해당 Probider컴포넌트가 공급하는 모든 데이터에 접근할 수 있는 컴포넌트들의 영역을 문맥(Context)이라고 표현한다.

그래서 Provider 컴포넌트 아래에 있는 모든 컴포넌트들은 일기데이터를 조작하고 관리한다는 문맥하에 있다.(이 모든 컴포넌트들이 일기데이터를 조작하고 관리하기위해 문맥속에 있다)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FE1UMK%2FbtrHOsPnL16%2FgePK0tWbNJKFfKwG3s23sK%2Fimg.png)

근데 만약에 이렇게 Counter 컴포넌트처럼 Provider컴포넌트의 자식컴포넌트가 아닌경우, Provider가 제공하는 데이터에 접근할 수 없으며 같은 문맥(Context)이 아니라고 할 수 있다.

 

그래서 우리는 Context를 이용하여 props drilling을 해결할 수 있게 된 것이다.

<br><br>

### 자 그래서 우리는 Context API를 사용할 것이다.
 

#### - Context 생성

```js
const MyContext = React.createContext(defaultValue);
```

#### - Context Provider를 통한 데이터 공급

```js
<MyContext.Provider value = {전역으로 전달하고자 하는 값}>
	{/*이 Context안에 위치할 자식 컴포넌트들*/}
 </MyContext.Provider>
```

자 그럼 이제 본격적으로 context API를 이용하여 props drilling을 제거해 보도록 하겠다!

 

import 파트에서 React가 import되어있는지 확인하고 없다면 추가해주자.

```js
import React, { useCallback, useMemo, useEffect, useRef, useReducer } from "react";
먼저 일기 state를 전역적으로 도와줄 context 만들어보자

export const DiaryStateContext = React.createContext();
```
context도 내보내줘야하기 때문에, export default App;처럼 export해주자!

<br><br>

#### 왜 export일까?
export default는 파일당 한번밖에 못쓰고, export는 여러번 쓸 수 있는데
```js
import React, { useCallback, useMemo, useEffect, useRef, useReducer } from "react";
```

여기서 React는 그냥 import하지만, 

나머지는 {}를 통해 비구조화 할당을 통해 import한다.

근데 여기서 React는 이름을 바꿔서 import가 가능하지만, 그 외에는 이름을 바꿔서 import할 수가 없다.

왜냐하면 react파트에서 바로 import React할 수 있는 것은 export default부분만 바로 이와같이 바로 import가 가능하고

export const와 같이 내보내기가 된 부분은 비구조화 할당을 통해서만 import가 가능하다.

 

**그래서 App.js에서는 App 컴포넌트를 내보내고 있고,  부가적으로는 DiaryStateContext를 내보내고 있는것을 확인할 수 있다.**

 

자 그럼 다시 본론으로 다시 들어가서 **DiaryStateContext** 에 공급자를 만들고 데이터를 공급해보겠다.

<br><br><br>

## 1. Data 공급
component가 return 하는 부분의 최상위 컴포넌트를 다음과 같이 바꿔준다.(<DiaryStateContext.Provider>로 감싸주기)

```js
  return (
    <DiaryStateContext.Provider>
      <div className="App">
        <DiaryEditor onCreate={onCreate} />
        <div>전체 일기 : {data.length}</div>
        <div>기분 좋은 일기 개수 : {goodCount}</div>
        <div>기분 나쁜 일기 개수 : {badCount}</div>
        <div>기분 좋은 일기 비율 : {goodRatio}</div>
        <DiaryList onEdit={onEdit} onRemove={onRemove} diaryList={data} />
      </div>
    </DiaryStateContext.Provider>
  );
```

이렇게 하면 개발자모드에서

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FszYFY%2FbtrHTW9B8mU%2FkuPxHEDuTlCDJ5bDS1lSs0%2Fimg.png)

**DiaryStateContext.Provider가 컴포넌트들을 감싸고 있다는 것을 알 수 있다.**

**그래서 이 부분으로 감싸져 있는 컴포넌트들은 어디에서든지 사용가능하다는 뜻을 지니고 있다.**

<br><br>

그럼 데이터를 한번 공급을 해보자.

value라는 데이터로 공급을 해주어야한다.

```js
return (
    // value라는 데이터로 공급을 해주어야한다.
    <DiaryStateContext.Provider value={123}>
```
그래서 아래와 같이 value로 전달되는 것을 확인할 수 있다. (이는 언제든지 사용할 수 있는 값이라고 할 수 있다.)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdj21Wh%2FbtrHVIbuCOZ%2FKkSAKzd373khS3pETl3xdK%2Fimg.png)


DiaryStateContext가 공급하고 싶은 값은 App 컴포넌트가 가진 data state이기 때문에 value에 data state를 넣어주면 된다.

```js
return (
    // value라는 데이터로 공급을 해주어야한다.
    <DiaryStateContext.Provider value={data}>
```
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbwQvsD%2FbtrHUMrSNf7%2F4t6BsxrqLaVVMFZArkciM1%2Fimg.png)

그래서 위와 같이 value를 data로 가져오는 것을 확인할 수 있다.

 

이렇게 데이터를 공급하는 과정은 끝이 났다.

<br><br><br>

##### App.js 최종 코드

```js
import React, { useCallback, useMemo, useEffect, useRef, useReducer } from "react";
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

// 먼저 일기 state를 전역적으로 도와줄 context 만들어보자
// React가 import되어있는지 확인하고 없다면 추가해준다.
// context도 내보내줘야하기 때문에, export default App;처럼 export해준다
// export default는 파일당 한번밖에 못쓰고, export는 여러번 쓸 수 있는데

export const DiaryStateContext = React.createContext();

const App = () => {
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
    // value라는 데이터로 공급을 해주어야한다.
    <DiaryStateContext.Provider value={data}>
      <div className="App">
        <DiaryEditor onCreate={onCreate} />
        <div>전체 일기 : {data.length}</div>
        <div>기분 좋은 일기 개수 : {goodCount}</div>
        <div>기분 나쁜 일기 개수 : {badCount}</div>
        <div>기분 좋은 일기 비율 : {goodRatio}</div>
        <DiaryList onEdit={onEdit} onRemove={onRemove} diaryList={data} />
      </div>
    </DiaryStateContext.Provider>
  );
};

export default App;
```
 

 

자 그럼 이번에는 context 밑에 있는 자식요소가 data를 사용해보자.

<br><br><br><br>

## 2. Context 밑 컴포넌트들의 Data 사용
DiaryList.컴포넌트!

먼저 App컴포넌트에서 data state를 prop으로 받아서 map함수를 통해 렌더링을 하고 있었지

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc5q5gv%2FbtrHUhyVl1c%2FKiuat8gfXXoncbJ8i7Pklk%2Fimg.png)

근데 이제는 data state에서 받을 필요가 없다. 왜냐하면 context로 받으면 되는거니까! 그래서 porp을 지우면 된다!

```js
import DiaryItem from "./DiaryItem";

const DiaryList = ({ onEdit, onRemove }) => {
그렇게 하고 useContext라는 hook을 사용해야하기때문에 import로 받아서 아래와 같이 사용한다.

import { useContext } from "react";
import DiaryItem from "./DiaryItem";

const DiaryList = ({ onEdit, onRemove }) => {
  // context에서 받아와야하기 때문에 useContext라는 hook을 사용해야한다(import받아야한다.)
  const diaryList = useContext
```
이렇게 하고 useContext는 context를 전달해야하는데 값을 꺼내고 싶은 데이터를 전달하면 된다.

DiaryStateContext를 사용하려니 이는 App.js로부터 export const로 내보냈기에 iport로 가져와주고 아래와 같이 사용하면된다.

```js
import { useContext } from "react";
import DiaryItem from "./DiaryItem";
import { DiaryStateContext } from "./App";

const DiaryList = ({ onEdit, onRemove }) => {
  // context에서 받아와야하기 때문에 useContext라는 hook을 사용해야한다(import받아야한다.)
  // DiaryStateContext는 App.js에서 export const로 내보낸적이 있기에 import로 가져와주고 아래와 같이사용하면된다.
  const diaryList = useContext(DiaryStateContext)
```
그래서 아래와 같이 components에서 hooks로부터 Data사용을해야한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbp0lgt%2FbtrHVgsLOHT%2Fz5KIACpxgWVhjF24BZiMoK%2Fimg.png)

그래서 App 컴포넌트로부터 diaryList={data}는 없어져도 되게 된다.

```js
<DiaryList onEdit={onEdit} onRemove={onRemove} diaryList={data} />
<DiaryStateContext.Provider value={data}>
      <div className="App">
        <DiaryEditor onCreate={onCreate} />
        <div>전체 일기 : {data.length}</div>
        <div>기분 좋은 일기 개수 : {goodCount}</div>
        <div>기분 나쁜 일기 개수 : {badCount}</div>
        <div>기분 좋은 일기 비율 : {goodRatio}</div>
        <DiaryList onEdit={onEdit} onRemove={onRemove} />
      </div>
    </DiaryStateContext.Provider>
```
그래서 우리는 data state를 성공적으로 공급하였다.

하지만 data state는 context가 적용되기 이전에도 props drilling이 일어나지 않았다. (App에서 DiaryList로 한 단만 내려왔으면 되기에) 

 

자 그럼 onEdit, onRemove (상태변화를 주도하는 함수) 또한 context를 통해 공급자들을 과정을 가져보자.

 
```js
<DiaryStateContext.Provider value={data}>
      <div className="App">
        <DiaryEditor onCreate={onCreate} />
        <div>전체 일기 : {data.length}</div>
        <div>기분 좋은 일기 개수 : {goodCount}</div>
        <div>기분 나쁜 일기 개수 : {badCount}</div>
        <div>기분 좋은 일기 비율 : {goodRatio}</div>
        <DiaryList onEdit={onEdit} onRemove={onRemove} />
      </div>
    </DiaryStateContext.Provider>
```

data처럼 onCreate, onRemove, onEdit도 전달하면 좋게 보이겠지만 >> 절대 그렇게 해서는 안된다!!

Provider도 또한 컴포넌트이기 때문에(prop이 바뀌면 재생산되어버린다.)

Provider 컴포넌트가 재생산된다면, 자식 컴포넌트들도 자동으로 재생산 된다.

그래서 data, onCreate, onRemove, onEdit에 props를 같이 내려주면 data state가 바뀔때 마다 rerendering되어서 결론적으로 최적화가 다 풀리게 된다.

 

그래서 Context를 중첩으로 사용하면 된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FwGklX%2FbtrH0Pou6WZ%2FVUw2QkW6LKtdJX9LC1mink%2Fimg.png)

진과 같이 data를 DiaryStateContext만을 위해 존재하도록 만들어주고

지금 전달하고자하는 onCreate, onEdit, onRemove와 같은 변화시키는 함수(dispatch 함수)들을 내보내려 하는 것인데

다음과 같이 새로운 context를 생성해 주면 된다.  

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F1kbwh%2FbtrH0vjzuBv%2FYBW95RYVvlK6k2agKouU81%2Fimg.png)

이 DiaryDispatchContext의 Provider는 아래와 같이 배치할 것이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcVlL84%2FbtrH0vcOBlI%2FSicitl9idLFkDu07CbWsQk%2Fimg.png)

그래서 아래와 같이 Context.Provider가 2중으로 감싸져 있는 것을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbZRFoM%2FbtrH1zlaZI2%2FB9HYwd9mvKC75KqfkGPFYK%2Fimg.png)

위는 DiaryStateContext.Provider, 아래는 DiaryDispatchContext.Provider

그래서 dispatch함수들(onCreate, onEdit, onRemove)은 DiaryDispatchContext.Provider로 전달해 주면 되는 것이다.

 

그래서 DiaryDispatchContext.Provider는 다시 렌더링 될 이유가 없다. onCreate, onEdit, onRemove가 재생성되지 않는 함수들로만 이루어졌기 때문에 rerendering되지 않도록 만들면 된다.

 

자 그러면 onCreate, onEdit, onRemove를 하나로 묶어서 전달해보도록 하자. (useMemo 사용)

재생성 되는 일이 없도록, [] 빈 배열을 전달하자.

```js
  const memoizedDispatches = useMemo(() => {
    return {onCreate, onRemove, onEdit}
  }, [])
```

이렇게 하고 memoizedDispatches를 DiaryDispatchContext.Provider의 데이터로 전달해주자
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FvTZFb%2FbtrHZEuQIBT%2Fw16Q27HrlewjV50oaFuPq0%2Fimg.png)

useMemo를 활용해야하는 이유는 무엇이냐면!

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcwlEVR%2FbtrH1ccKoyX%2FgrEMo89R9u4zE7zRO89oPK%2Fimg.png)

이와 같이 만들어서 dispatches들을 전달한다면, App 컴포넌트가 재생성이 될 때 dispatches객체들도 다시 생성이 된다. 그래서 useMemo를 사용하여 재생성되지 않도록 해야한다.(이것이 최적화!)

 

그리하여, DiaryEditor도 DiaryList도 dispatch 함수들을 더이상 전달받지 않아도 되게 된것이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbXlkF2%2FbtrH0Sr5PEe%2FJYc8dPW9R1SFb0kKskhiNK%2Fimg.png)

```js
  return (
    // value라는 데이터로 공급을 해주어야한다.
    <DiaryStateContext.Provider value={data}>
      <DiaryDispatchContext.Provider value={memoizedDispatches}>
        <div className="App">
          <DiaryEditor />
          <div>전체 일기 : {data.length}</div>
          <div>기분 좋은 일기 개수 : {goodCount}</div>
          <div>기분 나쁜 일기 개수 : {badCount}</div>
          <div>기분 좋은 일기 비율 : {goodRatio}</div>
          <DiaryList />
        </div>
      </DiaryDispatchContext.Provider>
    </DiaryStateContext.Provider>
  );
```
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcr88DS%2FbtrH0vRrsh0%2FKjQYg3GevsjWdXUGehBY7k%2Fimg.png)

그리하여 DiaryEditor에서 onCreate props를 전달받지 않고, 아래와 같이 들고와야 한다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkBTBB%2FbtrHZDpbnWf%2Fffy4yaoVh7dg37SmCrkFz1%2Fimg.png)

그리고 DiaryList에서도 아래와 같이 삭제해주고

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbdg4nh%2FbtrH0bZZgOT%2FVleabQ5Klr3HbmTfqGqPd0%2Fimg.png)

그리고 DiaryItem에서 onEdit과 onRemove를 더이상 prop으로 받지 않게 지워주면 된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkKM0n%2FbtrHZDW2CMj%2FTYJBFK5Y1Lrn1IByKRpMYk%2Fimg.png)

그리하고 아래와 같이 불러주면 된다.

```js
const { onRemove, onEdit } = useContext(DiaryDispatchContext);
```

그러면 Create, Edit, Remove가 잘 작동되는 것을 볼 수 있다.

 

<br><br><br><br>

#### 최종코드
##### App.js

```js
import React, {
  useCallback,
  useMemo,
  useEffect,
  useRef,
  useReducer,
} from "react";
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

// 먼저 일기 state를 전역적으로 도와줄 context 만들어보자
// React가 import되어있는지 확인하고 없다면 추가해준다.
// context도 내보내줘야하기 때문에, export default App;처럼 export해준다
// export default는 파일당 한번밖에 못쓰고, export는 여러번 쓸 수 있는데

export const DiaryStateContext = React.createContext();
export const DiaryDispatchContext = React.createContext();

const App = () => {
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

  const memoizedDispatches = useMemo(() => {
    return {onCreate, onRemove, onEdit}
  }, [])

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
    // value라는 데이터로 공급을 해주어야한다.
    <DiaryStateContext.Provider value={data}>
      <DiaryDispatchContext.Provider value={memoizedDispatches}>
        <div className="App">
          <DiaryEditor />
          <div>전체 일기 : {data.length}</div>
          <div>기분 좋은 일기 개수 : {goodCount}</div>
          <div>기분 나쁜 일기 개수 : {badCount}</div>
          <div>기분 좋은 일기 비율 : {goodRatio}</div>
          <DiaryList />
        </div>
      </DiaryDispatchContext.Provider>
    </DiaryStateContext.Provider>
  );
};

export default App;
```

##### DiaryEditor.js
```js
import React, { useContext, useEffect, useRef, useState } from "react";
import { DiaryDispatchContext } from "./App";

const DiaryEditor = () => {
  const {onCreate} = useContext(DiaryDispatchContext)
  const authorInput = useRef();
  const contentInput = useRef();

  const [state, setState] = useState({
    author: "",
    content: "",
    emotion: 1,
  });

  const handleChangeState = (e) => {
    setState({
      ...state,
      [e.target.name]: e.target.value,
    });
  };

  const handleSubmit = () => {
    if (state.author.length < 1) {
      // focus
      authorInput.current.focus();
      return;
    }
    if (state.content.length < 5) {
      contentInput.current.focus();
      // focus
      return;
    }
    onCreate(state.author, state.content, state.emotion);
    alert("저장 성공");
    setState({
      author: "",
      content: "",
      emotion: 1,
    });
  };

  return (
    <div className="DiaryEditor">
      <h2>✨오늘의 일기✨</h2>
      <div>
        <input
          ref={authorInput}
          name="author"
          value={state.author}
          onChange={handleChangeState}
        />
      </div>
      <div>
        <textarea
          ref={contentInput}
          name="content"
          value={state.content}
          onChange={handleChangeState}
        />
      </div>
      <div>
        <span>오늘의 감정점수 : </span>
        <select
          name="emotion"
          value={state.emotion}
          onChange={handleChangeState}
        >
          <option value={1}>1</option>
          <option value={2}>2</option>
          <option value={3}>3</option>
          <option value={4}>4</option>
          <option value={5}>5</option>
        </select>
      </div>
      <div>
        <button onClick={handleSubmit}>일기 저장하기</button>
      </div>
    </div>
  );
};
export default React.memo(DiaryEditor);
```

##### DiaryItem.js
```js
import React, { useContext, useEffect, useRef, useState } from "react";
import { DiaryDispatchContext } from "./App";
const DiaryItem = ({
  id,
  author,
  content,
  created_date,
  emotion,
}) => {
  const { onRemove, onEdit } = useContext(DiaryDispatchContext);
  const [isEdit, setIsEdit] = useState(false);
  const toggleIsEdit = () => setIsEdit(!isEdit);
  const [localContent, setLocalContent] = useState(content);
  const localContentInput = useRef();

  const handleRemove = () => {
    if (window.confirm(`${id}번째 일기를 정말 삭제하시겠습니까?`)) {
      onRemove(id);
    }
  };

  const handleQuitEdit = () => {
    setIsEdit(false);
    setLocalContent(content);
  };

  const handleEdit = () => {
    if (localContent.length < 5) {
      localContentInput.current.focus();
      return;
    }
    if (window.confirm(`${id}번째 일기를 수정하시겠습니까?`)) {
      onEdit(id, localContent);
      toggleIsEdit();
    }
  };

  return (
    <div className="DiaryItem">
      <div className="info">
        <span className="author_info">
          작성자 : {author} | 감정: {emotion}
        </span>
        <br />
        <span className="date">{new Date(created_date).toLocaleString()}</span>
      </div>
      <div className="content">
        {isEdit ? (
          <>
            <textarea
              ref={localContentInput}
              value={localContent}
              onChange={(e) => setLocalContent(e.target.value)}
            />
          </>
        ) : (
          <>{content}</>
        )}
      </div>
      {isEdit ? (
        <>
          <button onClick={handleQuitEdit}>수정 취소</button>
          <button onClick={handleEdit}>수정완료</button>
        </>
      ) : (
        <>
          <button onClick={handleRemove}>삭제하기</button>
          <button onClick={toggleIsEdit}>수정하기</button>
        </>
      )}
    </div>
  );
};

export default React.memo(DiaryItem);
```

##### DiaryList.js
```js
import { useContext } from "react";
import DiaryItem from "./DiaryItem";
import { DiaryStateContext } from "./App";

const DiaryList = () => {
  // context에서 받아와야하기 때문에 useContext라는 hook을 사용해야한다(import받아야한다.)
  // DiaryStateContext는 App.js에서 export const로 내보낸적이 있기에 import로 가져와주고 아래와 같이사용하면된다.
  const diaryList = useContext(DiaryStateContext)
  return (
    <div className="DiaryList">
      <h2>일기 리스트</h2>
      <h4>{diaryList.length}개의 일기가 있습니다.</h4>
      <div>
        {diaryList.map((it) => (
          <DiaryItem key={it.id} {...it} />
        ))}
      </div>
    </div>
  );
};

// defaultProps는 undefined로 전달 될 수 있는 값을 default로 설정해주는 것
DiaryList.defaultProps = {
  diaryList: [],
};

export default DiaryList;
```