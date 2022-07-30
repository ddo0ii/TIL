# 7-3. 페이지 라우팅 2 (CSR)

### React/한입 크기로 잘라 먹는 리액트(React.js)

## React Router Dom의 유용한 기능
### REACT ROUTER V6
#### REACT에서 CSR기반의 페이지 라우팅을 할 수 있게 해주는 라이브러리
<br>

### 1. Path Variable (useParams)
### 2. Query String (useSearchParams)
### 3. Page Moving (useNavigate)
 
<br><br><br> 

## 1. Path Variable (useParams)
### Diary 페이지

경로 : /diary

특징 : 어떤 일기를 보여줘야 할 지 전달 받아야 함

예 : /diary/1 -> 1번 일기

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbOGgOC%2FbtrIxvp5L4i%2Fs0FFsyySQZ7JALd5WnzWEK%2Fimg.png)

먼저 diary/1이라 경로를 입력하여보겠다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcMAPQe%2FbtrIyvRcdLe%2F7a8ir4ZyxqdkdTMklyAFHk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fd561dY%2FbtrIA0Qsop6%2FNrDL6bzqJlr56KkSKob691%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FQRdiy%2FbtrIywCyWAR%2FQYfQmbKZFzmkkViHwJnmZK%2Fimg.png)

매칭되는 routes가 없다는 것을 보여준다.

**Path variable**을 사용하려면 routes에서 path설정을 별도로 해주어야한다.

**:id** 를 사용하여 뒤에 있는 인자를 전달하려는 것을 보여주면 된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fd4GPF9%2FbtrIBUbnJ9n%2FSx4kl3K8bRTWQ0BeZDQBxK%2Fimg.png)

그럼 다음과 같이 정상적으로 실행이 된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FD2ZAt%2FbtrIvTerwHQ%2F6cMkpDSlzaYzq2qNmyy3YK%2Fimg.png)

그러나 다음의 /1인 id값을 뺀다면 아래와 같이 경로설정이 되지않아 다음과 같은 결과 값을 내는 것을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDKEA2%2FbtrIyo422Z0%2FfHsgBNyBkQA215qpl5oLK1%2Fimg.png)

그래서 다음과 같이 아래와 같이 두 경우로 코드를 구성한다면 두 경우 모두 정상적으로 출력됨을 알 수 있다.

http://localhost:3000/diary/1
http://localhost:3000/diary

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdondtw%2FbtrItmUYox8%2FPkWwR0sp3rocuLkn8xL24K%2Fimg.png)

그러나 우리는 id가 없는 일기는 유지하지 않을 것이기 때문에 /diary 로 path가 설정되어있는 구문은 삭제할 것이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F5ZG9i%2FbtrICZcrFx6%2FQD0SZeFWKAtscIg9IXkyz0%2Fimg.png)


그럼 우리 1이라는 path variable을 꺼내서 한번 사용해보자.

우선 diary 컴포넌트에서 사용해보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcS4VkC%2FbtrIA1oihP1%2FbuAXNnOioUnrBCkND6Jqek%2Fimg.png)

**useParams**를 이용하여 id를 선언하는데,

여기서 use라는 keyword는 react에서 hooks로 많이 사용하는데

여기에서는 hook은 아니지만 별도의 library에서 기능을 더 편하게 만들어준 사용자 정의 hook을 custom hooks라 칭한다.

<br> 

그래서 여기서 useParams를 사용하면, 전달받아 들어오는 path variable들을 모아서 객체로 가져다 주는데 우리는 이를 여기서는 id라고 부르기로 했다. 그래서 우리는 id로 꺼내오면 되는것이다!

console로 id를 출력해보면 1을 잘 출력하는 것을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpsZJz%2FbtrIx0KEZLE%2FF1UXXCzjfBspkLpcfy36i1%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbb4Eos%2FbtrIBUJdyqe%2F0HnDQSaTd2JkYHcO0aOp5K%2Fimg.png)

<br> <br> <br> 

## 2. Query String (useSearchParams)
### Query : 웹 페이지에 데이터를 전달하는 가장 간단한 방법

/edit?id=10&mode=dark    => Query String
 

http://localhost:3000/edit?id=10&mode=dark 이 경로로 이동하게 되면 아래와 같이 정상적으로 출력되는 것을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcXSaj0%2FbtrIuamqOeO%2FVadGkMIATAwiBEoUQlew41%2Fimg.png)

근데 원래 Path variable사용하면 별도의 처리를 해줘야 잘 처리가 되었는데 **Query String**처리를 하면 별도의 처리를 하지 않아도 되는 점을 확인할 수 있다. 그래서 ? 뒤에있는 인자들은 페이지 경로에 영향을 주지 않는다는 것을 알 수 있다.

 

그럼 우리 **Query String**를 한번 꺼내서 사용해보자.

이번에는 **useSearchParams**를 사용하였다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fmf6g8%2FbtrIsd45CC6%2FlxJxIL56mnKeBCjmmdNWpK%2Fimg.png)

이번에도 아래와 같이 잘 출력되는 것을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbi3XMX%2FbtrIyZLiqAT%2FKxqsRbkqAaZHVaET5mQTQ1%2Fimg.png)

자 그럼 **setSearchParams**를 이용하여 전달되는 query들을 변경시켜보겠다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc5qkRN%2FbtrIuaGNCcG%2Fj9QP5XZHnKkuYbKpC4z3Rk%2Fimg.png)

이렇게 버튼을 하나 만들어 실행시킨다면 아래와 같이 Query String이 변하는것을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FM02Jt%2FbtrICPVaxOH%2FCUC7oTQqUcNyT4OjKQuUZk%2Fimg.png)

<br> <br> <br> 

## 3. Page Moving (useNavigate)
이번에도 Edit페이지에서 한번 실행을 해보자.

버튼을 클릭하면 form으로 이동할 수 있도록 한번 만들어보자.

**useNavigate**라는 hook을 사용해보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F6YyEl%2FbtrIyoRzPw5%2FF0XjqUup6EdNve3rnQCOP0%2Fimg.png)

여기에서 HOME으로 가기를 클릭하게 된다면

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FFgMaC%2FbtrIxBdhZ5E%2FVKfxKkRlBhB3jYUrboKFOk%2Fimg.png)

Home으로 이동하는 것을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc7LAuz%2FbtrIzarZ3k5%2FkGMQtyNnJnBKJH54K12Ilk%2Fimg.png)

이는 로그인되지 않은 사용자가 로그인 페이지로 가려고 할때 로그인 값을 검사해서 로그인하지 않았다면 로그인 페이지로 강제로 보내버리기 위해 이 기능을 사용하게 된다. 그래서 Navigate기능은 페이지 이동을 원치 않아도 그쪽으로 이동시킬 수 있는 기능을 지니고 있다고 생각하면 된다.

 

그럼 뒤로가기는 어떻게 만들까?

뒤로가기는 **-1**을 이용하여 할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fy6s8X%2FbtrIxBxA8FN%2FHfheP9KphxlcgCv4MraQx1%2Fimg.png)