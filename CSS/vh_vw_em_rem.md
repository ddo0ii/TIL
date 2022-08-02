# vh, vw, em, rem

해당 글에 사용될 HTML 코드 -

```html
<body>
  <div class="parent">
    <div class="child"></div>
  </div>
</body>
```

%

```css
.parent {
    position: flex;
    height: 600px;
    width: 600px;
    margin: 0px 0px;
    background: rgb(201, 179, 125);
}

.child {
height: ???
width: 60%;
margin: 0 auto;
background: rgb(92, 170, 206);
}
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbPTFJ4%2FbtrIA2bhLOI%2FMkWUbOjTbWuwwqEiKcGu40%2Fimg.png)

height: 50%

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb2U0uG%2FbtrIH5RSWVb%2FwTD8uF28F3n1LoRvocRIr0%2Fimg.png)

height: 100%

부모 엘리먼트(.parent) 크기에 따라 %가 차지하는 모습을 볼 수가 있다.

<br><br>

## vh

vh는 Viewport height의 축약어 이며, Viewport는 웹사이트에서

보여지는 영역을 뜻한다.

만일 1vh로 속성값을 설정할 경우 뷰포트 너비의 1% 만큼 계산이 된다.

#### 1vh = 1%

```css
.child {
  height: 20vh;
  width: 100%;
  margin: 0 auto;
  background: rgb(92, 170, 206);
}
```

![](https://blog.kakaocdn.net/dn/bWUZF5/btrIBTE719E/JWCiRq8khNNvmfvT5EECv1/img.gif)

해당 vh는 웹페이지 사이즈를 수정할 경우 20vh이므로 높이가 20% 만큼 계산되는 셈이다.

<br><br>

## vw

vh는 Viewport weigth의 축약어이다.

1vw로 속성값을 설정할 경우 뷰포트 너비의 1% 만큼 계산이 된다.

#### 1vw = 1%

```css
.child {
  height: 100%;
  width: 20vw;
  margin: 0 auto;
  background: rgb(92, 170, 206);
}
```

![](https://blog.kakaocdn.net/dn/pa62g/btrIJWAbiwW/VWO2u0BuIKiKcQ3rkNydCK/img.gif)

해당 vw는 웹페이지 사이즈를 수정할 경우 20vw이므로 너비가 20% 만큼 계산되는 셈이다.

<br><br>

## em

em 은 부모 엘리먼트의 폰트 사이즈를 기준으로 한 단위이다.

#### 1em = font size (부모 엘리먼트)

```css
.parent {
  font-size: 20px;
}

.child {
  font-size: 2em;
}
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FLpiKy%2FbtrIEcEeWXM%2FqjW6W0z33ql36A3wnVKBkk%2Fimg.png)

.child를 2em 속성값을 지정했으므로, 부모 엘리먼트 폰트 사이즈 기준으로 40px이다.

<br><br>

## rem

rem은 최상위 엘리먼트의 폰트 사이즈를 기준으로 한 단위이다.

#### 1rem = font size (최상위 엘리먼트)

```css
html {
  font-size: 50px;
}

.parent {
  font-size: 20px;
}

.child {
  font-size: 2rem;
}
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbDFXto%2FbtrIJW7ZFsR%2FEHKWYBRlKDrNkXTdnB1zF0%2Fimg.png)

.child를 2rem 속성값을 지정했으므로, 최상위 엘리먼트(html) 폰트 사이즈 기준으로 100px이다.

### rem 과 em 둘 중 누가 더 접근성에 선호되는가?

<br>

비교하자면 rem이 더 접근성이 편리하다.

왜냐하면 em의 경우 부모 엘리먼트를 기준으로 상대적인 크기가 변경되므로 제한적인 특징이 있지만,

rem은 최상위 엘리먼트에 상대적인 크기가 변경되므로 광범위한 특징이 있어 접근성이 편리하다.

[출처](https://velog.io/@milkyway/CSS-%EB%8B%A8%EC%9C%84-%EB%B9%84%EA%B5%90-vh-vw-em-rem)
