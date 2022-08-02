# SPA : Single Page Application

최초 한번 페이지 전체를 로딩한 이후 부터는 데이터만 변경하여 사용할 수 있는 웹 어플리케이션
(하나의 html파일로만 동작함, 리액트 프로젝트 파일도 보면 다 html파일 하나로 작업)
SPA는 클라이언트사이드렌더링 방식이다!
<br>

### Rendering이란?

렌더링은 요청받은 내용을 브라우저 화면에 표시하는 것
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FGMo1N%2FbtrInHZhLrX%2FkCxWO3qUfVsvNkdUpGjyak%2Fimg.png)
<br><br>

# Client Side Rendering

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

# Server Side Rendering

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

**참고문헌**

[바로가기](https://velog.io/@haileyself/SPA-Client-Side-Rendering-%EA%B7%B8%EB%A6%AC%EA%B3%A0-Server-Side-Rendering-90k4ar8is1)
