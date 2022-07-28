# 7-2. 페이지 라우팅 1 (CSR)

### React/한입 크기로 잘라 먹는 리액트(React.js)

우선 새로 React Application을 하나 생성하였다.

## 우리는 이번에 React router라는 라이브러리를 사용할 것이다.
React router 공식페이지에 접속해보자.
[React router 공식페이지](https://reactrouter.com/)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkIxVS%2FbtrItu5eHD4%2FI8ZdwM5T4PpGdZOqrsxPok%2Fimg.png)

우선 설치를 해보자. Read the Docs를 통해 Installation으로 접속해보자.

[Installation](https://reactrouter.com/docs/en/v6/getting-started/installation)

그리고 아래의 명령어로 라이브러리를 설치해보자.

```sh
npm install react-router-dom@6
```

그러면 package.json파일에 아래와 같이 설치가 잘 되어있음을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbK4ZHb%2FbtrIuYSh2Mp%2FOY3lc0mMciGnVexIP8x8Xk%2Fimg.png)

그럼 npm start로 구동시켜 보겠다.

 

그리고 Routing을 하기 위해 pages폴더를 생성하고, 각 3개의 페이지를 생성해보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcRzv1C%2FbtrIuZjnmcc%2F8tBgVF0KgHUspkK70v9MA0%2Fimg.png)

각각 파일별로 페이지 역할을 할 컴포넌트들을 생성해보자.

**Home.js**
```js
const Home = () => {
    return (
        <div>
            <h1>Home</h1>
            <p>이곳은 홈입니다.</p>
        </div>
    )
}

export default Home;
```
**New.js**
```js
const New = () => {
    return (
        <div>
            <h1>New</h1>
            <p>이곳은 일기 작성 페이지입니다.</p>
        </div>
    )
}

export default New;
```
**Edit.js**
```js
const Edit = () => {
    return (
        <div>
            <h1>Edit</h1>
            <p>이곳은 일기 수정 페이지입니다.</p>
        </div>
    )
}

export default Edit;
```
**Diary.js**
```js
const Diary = () => {
    return (
        <div>
            <h1>Diary</h1>
            <p>이곳은 일기 상세 페이지입니다.</p>
        </div>
    )
}

export default Diary;
```

이제는 React Router Dom을 사용해서 방금 만들었던 페이지들을 특정 주소에 연결해서 Routing을 시도해보자. 

 

먼저 react router 컴포넌트로 App.js파일에서 App 컴포넌트가 return하는 부분을 감싸줘보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FuUm6M%2FbtrIn3ukCQn%2FYeIktADxI4px9wFmIlpvNk%2Fimg.png)

이렇게 감싸주면 Browser url과 mapping될 수 있다라고 생각하면 된다.

다음으로는 우리가 생성했던 네개의 파일들을 import해보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbkypbe%2FbtrIptsto2y%2FTOpLp7MOHckNyKViktpx0k%2Fimg.png)

그래서 이동될 부분들을 <Routes>로 감싸줘 보자.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpiT0u%2FbtrIpGSzpec%2FOPhKjYps0UEQhBNxGd2POk%2Fimg.png)

그리고 Route컴포넌트를 사용해보자.

Route컴포넌트는 실제적으로 url경로와 컴포넌트들을 매핑시켜주는 컴포넌트이다. 그래서 다음과 같이 컴포넌트들을 전달해주면된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbIkkKj%2FbtrIt5Ysdwr%2FYyJuTAKFEeaZcU75s8jgEk%2Fimg.png)

이렇게 하면 다음과 같이 웹브라우저에 나타나게 된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fzz8sA%2FbtrIn4zVVWQ%2FAt93NdTwZEOfHwinLdXMvK%2Fimg.png)

다음과 같이 개발자모드로 확인한다면 Route.Provider아래에 Home 컴포넌트가 전달되고 있는것을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbuAHXe%2FbtrIn3A9E0U%2FsWtXJpEs3q8pzfEHv3rJUk%2Fimg.png)

여기에서 path가 index를 가르키면 Home 컴포넌트를 나타내라고 한것인데
```js
<Route path="/" element={<Home />} />
```
Home 컴포넌트를 mapping시켜서 이와 같이 출력된다고 알면된다.

 

근데 mapping되지 않은 /pages와 같은 페이지들은 Routes안으로 매핑되는 컴포넌트들이 없다보니 Routes가 렌더링할 부분이 없어 Routes에 속하지 않은 부분만 렌더링하게 된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcDCmp7%2FbtrIt6iJI4z%2FbLAtUCNgY81HJhnD1DkiDk%2Fimg.png)

이럴때 콘솔을 확인하면 경고가 뜨게 되는데

/pages와 일치하는 routes가 없다고 출력되는 것을 볼 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F0bGcd%2FbtrIuXTpFqg%2FHIhkgvfaapywD9O7r7NJ7K%2Fimg.png)

자 그러면 하나의 Route페이지를 추가해보자.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJUCAV%2FbtrIuZcBOMN%2FL9PflmqFrWib5hc3j4BNR0%2Fimg.png)

new페이지로 이동하게 된다면 아래와 같이 출력이 되는것을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoFtDg%2FbtrInD3mpWQ%2FcGcKD56JXeLco8RukWIxt1%2Fimg.png)

근데 App.js의 h2부분은 그대로 있는 것을 확인할 수 있는데,

Routes안에 있는 부분만 변화하도록 설계하였기 때문에 Routes부분만 변경되고 이외의 부분은 그대로 설계가 된다.

 

그러고 이제 다른 페이지들도 Routing해주자.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcrU18a%2FbtrIoJhHL5T%2FCALk7JvhsT5CJCQLsGIvxk%2Fimg.png)

자 그럼 페이지이동을 시키는 요소를 만들어보자.

우리는 기존에 a tag를 통해 페이지를 이동시켰다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb86RlZ%2FbtrInJJDIg7%2F0JXWXYfKivw14DIE7BwBKk%2Fimg.png)

### 그런데 이 태그를 사용할 경우 계속 페이지가 새로고침되는것을 확인할 수 있다.

### 페이지를 이동하는것은 SPA의 특징이 아니라 MPA의 특징이었다.

### 그래서 a태그를 이용하게 된다면 SPA의 장점을 사용하지 못한다는 것이다.

그래서 우리는 a태그를 사용하지 않을 것이다.

### a 태그는 외부 페이지로 이동할때만 이용하도록 하자

<br>

## 그럼 React Router는 어떻게 페이지를 이동시켜야하나?
자 우선 component하나를 생성해보자.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDMFuV%2FbtrInJpkbjN%2FV3OPtaW4Z5d8VWxwfahGjk%2Fimg.png)

이 RouteTest 컴포넌트를 React Route에서 제공하는 SPA, CSR방법으로 페이지를 이동할 수 있도록 사용해 볼것이다.

이 컴포넌트의 이름은 Link인데 아래와 같이 import해주면 된다.
```js
import { Link } from 'react-router-dom';
```
근데 보통 a태그를 이용할때 경로를 명시할때에는 href를 사용하였지만

Link router를 사용할 때에는 to라는 prop에다 경로를 전달해 주면된다. 

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FWeDga%2FbtrIq5ZjaGR%2FG5sFJna09YdkBhhMFqYOK1%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F1eccC%2FbtrInIcTayt%2FN1gUN2OCtq0FnWv3sXd6yK%2Fimg.png)

그리고 RouteTest를 사용할 수 있도록 App.js에 import해보자

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F27OXQ%2FbtrItuEb4RM%2FLksS6DYcfKmU5bDENXqWvK%2Fimg.png)

그럼 다음과 같이 네개의 링크가 생성된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbleLvJ%2FbtrItvpBDMR%2FAEmdCb4JVvx87hnN3eWcc1%2Fimg.png)

각각 링크를 클릭하면 component가 리렌더링되면서 페이지가 이동되는것을 확인할 수 있다.

그리고 위의 아이콘도 깜빡이지 않으면서 페이지가 이동되는 것을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDKaqM%2FbtrItvJRZpN%2FumwA8jiHlmRPqbmGC67as0%2Fimg.png)

굉장히 빠른 페이지 이동을 CSR방식으로 React router로 구현할 수 있다.

 

이렇게 CSR로 페이지를 이동시키게 되면,

실제로 페이지를 이동시키는것이라고 보기 보다는 페이지 역할을 하는 컴포넌트들을 갈아끼우고 url을 바꿔서 마치 페이지가 이동하는것처럼 보이게 만드는 방식이라고 생각하면 된다.

 

결론적으로 React App이 제공하는  public의 index.html 파일이 딱 하나 뿐이지만
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJciNd%2FbtrIq6X7T0x%2FEwcnf63NxXWkaUEax26z41%2Fimg.png)

App 컴포넌트의 Router들을 통해서 url로 컴포넌트들을 계속 변경하여 마치 페이지가 이동되는 것처럼 만들어주는 방식이라고 알 수 있다.

 

그래서 React는 이러한 방식으로 페이지를 전환시키기 때문에

페이지 이동시 깜빡임이 없고 이동속도가 매우 빨라서 쾌적한 페이지 이동을하는 CRS방법으로 렌더링한다.

 

**최종 코드**

**src/App.js**
```js
import './App.css';
import { BrowserRouter, Route, Routes } from 'react-router-dom';

import RouteTest from './components/RouteTest';

import Home from './pages/Home'
import New from './pages/New'
import Edit from './pages/Edit'
import Diary from './pages/Diary'

function App() {
  return (
    <BrowserRouter>
      <div className="App">
        <h2>App.js</h2>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/new" element={<New />} />
          <Route path="/edit" element={<Edit />} />
          <Route path="/diary" element={<Diary />} />
        </Routes>
        <RouteTest />
      </div>
    </BrowserRouter>
  );
}

export default App;
```
**src/components/RouteTest.js**
```js
import './App.css';
import { BrowserRouter, Route, Routes } from 'react-router-dom';

import RouteTest from './components/RouteTest';

import Home from './pages/Home'
import New from './pages/New'
import Edit from './pages/Edit'
import Diary from './pages/Diary'

function App() {
  return (
    <BrowserRouter>
      <div className="App">
        <h2>App.js</h2>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/new" element={<New />} />
          <Route path="/edit" element={<Edit />} />
          <Route path="/diary" element={<Diary />} />
        </Routes>
        <RouteTest />
      </div>
    </BrowserRouter>
  );
}

export default App;
```