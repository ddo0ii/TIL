# PAGE ROUTING (/home -> /product?id=1)

### React/한입 크기로 잘라 먹는 리액트(React.js)

우선 페이지가 한 페이지로 구성되면 서비스하기도 힘들고 구성하기도 힘들다.
그래서 이번에는 3 페이지로 구성된 웹 어플리케이션을 만들어 볼 것이다.

그래서 먼저 웹 사이트 페이징에 먼저 알아보자.
<br><br>

## PAGE ROUTING
### Routing이란?
어떤 네트워크 내에서 통신 데이터를 보낼 경로를 선택하는 일련의 과정

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbMp24w%2FbtrInFmeDBy%2FG7uJKkl8VrJOokCGdkA8a1%2Fimg.png)
이와 같이 데이터가 직통으로 가지않고

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FXKYAy%2FbtrItl7SjSP%2FwIzOW2cjsZHmzvDkSPjqm1%2Fimg.png)
네트워크를 통해 메세지가 전송이 된다.(이 네트워크 장치들을 지하철 역이라고 생각하면 좋다.)
<br>
여기서도 데이터들이 어디로 가야할지 알려준다. 그래서 이 네트워크들도 실시간으로 최단거리를 계산해서 갈 수 있도록 한다.

이 경로(route)를 정해주는 장치를 ROUTER라고 칭한다.

 

#### ROUTER : 데이터의 경로를 실시간으로 지정해주는 역할을 하는 무언가

#### ROUTE + ING : 경로를 정해주는 행위 자체와 그런 과정들을 다 포함하여 일컫는 말

<br><br>

### PAGE ROUTING이란?
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FyNV1E%2FbtrItuYqnqq%2FKKh8HTgZPJ18HCTnlN7FUk%2Fimg.png)
웹페이지에 접속하는 것 : 브라우저를 통해 웹서버에 경로의 요청을 날리고 웹 문서를 받아보는 과정


![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxxJWg%2FbtrIuYkpcwb%2F6iJfSt1DccNjlLl7rdJ98K%2Fimg.png)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDZ5hB%2FbtrIoBxsXqT%2FWOJiNk6FD1KH3mqUVgAFRk%2Fimg.png)
#### Page routing : 웹서버가 요청에 명시되어있는 경로에 따라 알맞은 페이지를 선택하고 페이지를 반환하여 사용자가 그 페이지에 접속하는 과정
<br><br>

#### Multipage Application(MPA)  : 여러개의 페이지를 준비해 놓고 요청이 들어오면 그에 맞게 알맞은 페이지를 반환해주는 것

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FclNVfm%2FbtrInDvr1sA%2FMK7EGf6bQixSULpba2jg3k%2Fimg.png)

전통적으로는 각 페이지 이동마다 페이지를 요청하는 방식을 사용한다.(그래서 새로고침하듯이 깜빡이면서 페이지 이동을 하게 된다.)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcflw6U%2FbtrIoBxtc8R%2FchyQk1xi8G1jl3eyJldrE1%2Fimg.png)

사진과 같이 페이지 이동할때마다 새로고침 되어 페이지가 깜빡이며 이동하게 된다.

 
<br><br>
그런데 REACT는!!!

#### Single Page Application(SPA) : 페이지가 하나뿐인 어플리케이션 (Mypage를 요청해도 index.html, 상세페이지를 요청해도 index.html을 반환), 깜빡이지 않는다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FUVhXM%2FbtrIt4SJS29%2FloVLO4GPng8P5V62MUkJMk%2Fimg.png)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc3w4VN%2FbtrIq5x2OJr%2FMNz214v7gbrOBXCJQMpXHk%2Fimg.png)
요청 시 어떠한 상황이어도 index.html을 반환하게 되고, REACT APP을 통째로 던져주게 된다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FslShG%2FbtrInDPJsj9%2FxB8SeeaNNHJz9ydTb3LUAk%2Fimg.png)

근데 post라는 페이지로 이동하고 싶어 어떤 버튼을 클릭하게 된다면, REACT APP이 페이지를 업데이트 시켜버린다.

원래 페이지 이동은 서버와 통신을 해서 이루어져야하는데, 브라우저가 알아서 처리해버리면 되니까 서버 대기시간이 필요없게 되며 바로 업데이트가 되어버린다.

그래서 서버와 통신하는 시간이 없어져버리니 페이지 전환 자체가 굉장히 빨라지게 된다.

 

근데 어떤 웹사이트들은 접속할때마다 보여지는 데이터들이 다르다. 이렇게 데이터가 필요한 경우에는 아래와 같이 서버와 데이터들만 요청하고 전달받으면 된다.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FWMwZr%2FbtrIn4zSCsS%2FrWiwrOMK3WkbZKE0b46M5K%2Fimg.png)

<br>

#### Client Side Rendering(CSR) : 클라이언트측에서 알아서 페이지를 렌더링하는 방식
<br><br><br>
 

그래서 정리를 하자면,

REACT는

### Single Page Application(SPA) 방식을 따르면서

### Client Side Rendering(CSR) 방식으로 페이지를 렌더링한다.

<br><br><br><br>

**참고문헌**

[바로가기](https://velog.io/@haileyself/SPA-Client-Side-Rendering-%EA%B7%B8%EB%A6%AC%EA%B3%A0-Server-Side-Rendering-90k4ar8is1)
<br>

## SPA : Single Page Application
최초 한번 페이지 전체를 로딩한 이후 부터는 데이터만 변경하여 사용할 수 있는 웹 어플리케이션
(하나의 html파일로만 동작함, 리액트 프로젝트 파일도 보면 다 html파일 하나로 작업)
SPA는 클라이언트사이드렌더링 방식이다!
<br>

### Rendering이란?
렌더링은 요청받은 내용을 브라우저 화면에 표시하는 것
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FGMo1N%2FbtrInHZhLrX%2FkCxWO3qUfVsvNkdUpGjyak%2Fimg.png)
<br><br>

## Client Side Rendering
클라이언트 사이드 렌더링은 SPA로, 클라이언트 사이드에서 HTML을 반환한 후에, JS가 동작하면서 데이터만을 주고 받아서 클라이언트에서 렌더링을 진행하는 것
점점 더 복잡해지는 웹페이지를 구현하기 위해서 전통적인 방식의 SSR보다는 CSR로 웹을 구현하는 경우가 많아짐

- 동작과정 : HTML 다운로드-> JS 다운로드 -> JS 실행 -> DATA 서버로부터 받기 -> Content 확인가능
<br>

### CSR의 장점
- 클라이언트 사이드 렌더링은 사용자의 행동에 따라 필요한 부분만 다시 읽어들이기때문에 SSR 보다 조금 더 빠른 인터랙션이 가능
- page 전체를 요청하지 않고 페이지에 필요한 부분만 변경하게 하기 때문에, 모바일 네트워크에서도 빠른 속도로 렌더링이 가능
- lazy loading을 지원해줌
lazy loading이란 ? 페이지 로딩 시 중요하지 않은 리소스의 로딩을 늦추는 기술
(Ex. 스크롤 내려야만 해당 이미지 보이게 하는 것)
- 서버사이드 렌더링이 따로 필요하지 않기때문에 일관성있는 코드를 작성할 수 있음
<br>

### CSR의 단점
- Googlebot과 Searchconsole에 검색 노출이 되지 않음 (브라우저가 없기때문에, html만 가져와서 검색에는 뜨지 않음)
- 페이지를 읽고, 자바스크립트를 읽은 후 화면을 그리는 시간까지 모두 마쳐야 콘텐츠가 사용자에게 보여지기 때문에 초기구동 속도가 느림
<br><br>

## Server Side Rendering
서버에서 렌더링을 작업하는 렌더링 방식, 전통적인 웹 어플리케이션 렌더링 방식으로 사용자가 웹 페이지에 접근할 때, 서버에 각각의 페이지에 대한 요청을 하며 서버에서 html, js 파일 등을 다 다운로드해서 화면에 렌더링하는 방식
<br>

### SSR의 장점
- 사용자가 처음으로 컨텐츠를 볼 수 있는 시점을 앞당길 수 있음
- 검색엔진최적화(SEO) 적용이 용이
<br>

### SSR의 단점
- 모든 요청에 관해 필요한 부분만 수정하는 것이 아닌, 완전히 새페이지를 로딩하고 렌더해줌(새로고침)
- 전체를 로딩하다보니 CSR보다 느리고, bandwitdh를 많이 쓰고, 사용자 경험 좋지 않음
(사용자가 처음으로 컨텐츠를 볼 수는 있으나, 화면단에는 html요소들이 나오나 js파일이 다 다운로드 되지않아서 버튼이 클릭되지않는 등의 현상이 있을 수 있음)