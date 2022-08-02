# Flex 컨테이너에 적용하는 속성들

### display: flex;

Flex 컨테이너에 display: flex;를 적용하는게 시작이에요.
이 한 줄의 CSS만으로 아이템들은 기본적으로 아래 그림과 같이 배치됩니다.

```css
.container {
  display: flex;
  /* display: inline-flex; */
}
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbASG5E%2FbtrIGymdCv3%2FMfz29xYgy9yCFj3Lax87a0%2Fimg.jpg)

Block 예시

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FciiXjP%2FbtrIJVAZxaa%2FDZ75djPfQSZCxkj8DW8Nf0%2Fimg.png)

Flex 예시

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbNm82I%2FbtrIA1Dbug4%2FGDKUhsBa5sco4aRqgTDMok%2Fimg.png)

Flex 아이템들은 가로 방향으로 배치되고, 자신이 가진 내용물의 width 만큼만 차지하게 되지요. 마치 inline 요소들 처럼요. height는 컨테이너의 높이만큼 늘어납니다.
height가 알아서 늘어나는 특징은 컬럼 레이아웃을 만들 때 아주 편리하겠네요~
(물론 나중에 정렬 속성을 통해 height를 어떻게 처리할지도 조정할 수 있습니다.)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FPVSx5%2FbtrIFHpDclr%2Fj6z6h73rXPYgldEtZqplt1%2Fimg.jpg)

컬럼의 높이가 자동으로 쫙- 맞는다

inline-flex도 있는데, 이건 block과 inline-block의 관계를 생각하시면 돼요.
아이템의 배치와 관련이 있다기 보다는, 컨테이너가 주변 요소들과 어떻게 어우러질지 결정하는 값입니다. inline-flex는 inline-block처럼 동작해요.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fv1TCm%2FbtrIxwDaexY%2FBom0DXPfEPYJLqGjkTkZr1%2Fimg.jpg)

아이템들이 배치된 방향의 축을 **메인축(Main Axis)**,
메인축과 수직인 축을 수직축 또는 **교차축(Cross Axis)**이라고 불러요.
좀 뜬금 없지만, 앞으로 **메인축**을 **“오뎅꼬치”**라고 생각하세요.
?????
나중에 정렬을 배울 때 헷갈리지 않으려고 하는 건데요,
오뎅(Flex 아이템)들이 꼬치(메인축)을 따라 쭉 꽂혀서 정렬된 상태를 생각하고 계시면 됩니다.
바로 이렇게요↓

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fs4qxg%2FbtrIvoFm9J2%2Fw7qJrI5ahaFiXD5EyEw0Pk%2Fimg.jpg)

<br><br><br>

### 배치 방향 설정

### flex-direction

아이템들이 배치되는 축의 방향을 결정하는 속성입니다. 즉 “메인축(오뎅꼬치)의 방향을 가로로 할거냐 세로로 할거냐”를 정해주는 거예요

```css
.container {
  flex-direction: row;
  /* flex-direction: column; */
  /* flex-direction: row-reverse; */
  /* flex-direction: column-reverse; */
}
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FVi1XI%2FbtrIBURm4H8%2FuLt4KXaBHhnGZTNkife6rk%2Fimg.jpg)

row (기본값)
아이템들이 행(가로) 방향으로 배치됩니다.

row-reverse
아이템들이 역순으로 가로 배치됩니다.

column
아이템들이 열(세로) 방향으로 배치됩니다.
그냥 block 요소들을 쌓아 놓은 것처럼 보이죠?

column-reverse
아이템들이 역순으로 세로 배치 됩니다.

크기가 작은 모바일 기기에서 column으로 배치하다가 일정 폭 이상이 되면 row로 바꿔주는 식으로 반응형 레이아웃을 구현할 수도 있겠네요~

<br><br><br>

### 줄넘김 처리 설정

### flex-wrap

컨테이너가 더 이상 아이템들을 한 줄에 담을 여유 공간이 없을 때
아이템 줄바꿈을 어떻게 할지 결정하는 속성입니다.

```css
.container {
  flex-wrap: nowrap;
  /* flex-wrap: wrap; */
  /* flex-wrap: wrap-reverse; */
}
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FYqYvp%2FbtrIH5RClHl%2FzMlDYzkXQolrEd8ApDBjF0%2Fimg.jpg)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F6f5Bn%2FbtrIJVBarPD%2F3p7iJaiXEBdaMKPTLi1b51%2Fimg.png)

nowrap (기본값)
줄바꿈을 하지 않습니다. 넘치면 그냥 삐져 나가요.

wrap
줄바꿈을 합니다. float이나 inline-block으로 배치한 요소들과 비슷하게 동작해요.

wrap-reverse
줄바꿈을 하는데, 아이템을 역순으로 배치해요. 그림을 보면 이해하실 수 있을 거예요.

<br><br><br>

### flex-flow

**flex-direction과 flex-wrap을 한꺼번에 지정할 수 있는 단축 속성**이에요.
flex-direction, flex-wrap의 순으로 한 칸 떼고 써주시면 됩니다.

```css
.container {
  flex-flow: row wrap;
  /* 아래의 두 줄을 줄여 쓴 것 */
  /* flex-direction: row; */
  /* flex-wrap: wrap; */
}
```

<br><br><br>

자, 이제 “정렬”을 할건데요. 시작하기 전에 기억해 두실게 있어요.
이건 나중에 Grid까지 이어지니까 지금 알아 두세요~

**“justify”는 메인축(오뎅꼬치) 방향으로 정렬**
**“align”은 수직축(오뎅을 뜯어내는) 방향으로 정렬**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FB8YTp%2FbtrIxS0hNhZ%2FDtzllQW1eSE3kM0jxwKPTk%2Fimg.jpg)

한 번만 나올게 아니니까 이건↑ 지금 꼭 머리에 넣어 두세요!

<br><br><br>

### 메인 축 방향 정렬

### justify-content

justify 키워드가 나왔죠? **메인축** 방향으로 아이템을들 정렬하는 속성이에요.

```css
.container {
  justify-content: flex-start;
  /* justify-content: flex-end; */
  /* justify-content: center; */
  /* justify-content: space-between; */
  /* justify-content: space-around; */
  /* justify-content: space-evenly; */
}
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxBStG%2FbtrII1IpQfi%2F7TPsKGMahVg6wiRrZs14lK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcECtEe%2FbtrIJV82T6S%2FFpaJVfxnNJK7Y1XLnBxhM0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FOHX7m%2FbtrIA2be6Xs%2FAitM0GLUmI5XdCJlIWVaBk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbwbffo%2FbtrII1uSzv0%2FrZJSCmueYUg56aXGFPJF0K%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdx9dwf%2FbtrIJVnDZ2z%2FSQi8g4w4Nw1n45SvGJviLk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcqnwH8%2FbtrIBVwahEY%2FHLDRbKCMsD7ebl1wsIg4s0%2Fimg.png)

flex-start (기본값)

아이템들을 시작점으로 정렬합니다.
flex-direction이 row(가로 배치)일 때는 왼쪽, column(세로 배치)일 때는 위예요.

flex-end
아이템들을 끝점으로 정렬합니다.
flex-direction이 row(가로 배치)일 때는 오른쪽, column(세로 배치)일 때는 아래예요.

center
아이템들을 가운데로 정렬합니다.

space-between
아이템들의 “사이(between)”에 균일한 간격을 만들어 줍니다.

space-around
아이템들의 “둘레(around)”에 균일한 간격을 만들어 줍니다.

space-evenly
아이템들의 사이와 양 끝에 균일한 간격을 만들어 줍니다.
주의! IE와 엣지(Edge)에서는 지원되지 않습니다👎
이 웹사이트의 메뉴 부분은 브라우저 폭이 1024px 이상일 때 space-evenly가 적용되도록 했는데요, IE와 엣지에서만 space-around로 적용이 되도록 처리해 두었어요.

space-between, space-around, space-evenly는 비슷한듯 하면서 살짝 다른데요, 아래 그림을 봐보세요~

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdEgVll%2FbtrIy89mPfy%2F2vdswuHTvPEM0wSIv2Sf80%2Fimg.jpg)

<br><br><br>

### 수직축 방향 정렬

### align-items

align 키워드가 나왔죠? **수직축** 방향으로 아이템을들 정렬하는 속성이에요.
justify-content와 수직 방향의 정렬이라고 생각하시면 됩니다.

```css
.container {
  align-items: stretch;
  /* align-items: flex-start; */
  /* align-items: flex-end; */
  /* align-items: center; */
  /* align-items: baseline; */
}
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FeDOaMS%2FbtrIC0cTn77%2FJnotps7moGrxVPMGKMm8qK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbGWAgS%2FbtrIEbLZZfU%2FiPuUMTAIQsXLQpKBZywnnk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FvcAvK%2FbtrIJVBbcuM%2FPfAAbM5IAHBPk4CnWwcRY0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbJLa2M%2FbtrIA2vsSfz%2FO6yBM9hV20eVKONcgJE89k%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpVTyL%2FbtrIEZdyMTq%2FGlHPTbdiwOv7EsYzeJVJ40%2Fimg.png)

stretch (기본값)
아이템들이 수직축 방향으로 끝까지 쭈욱 늘어납니다.

flex-start
아이템들을 시작점으로 정렬합니다.
flex-direction이 row(가로 배치)일 때는 위, column(세로 배치)일 때는 왼쪽이에요.

flex-end
아이템들을 끝으로 정렬합니다.
flex-direction이 row(가로 배치)일 때는 아래, column(세로 배치)일 때는 오른쪽이에요.

center
아이템들을 가운데로 정렬합니다.

baseline
아이템들을 텍스트 베이스라인 기준으로 정렬합니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F3dPCR%2FbtrIISxCuFj%2FsFysS2nsBPgNryudmikutk%2Fimg.jpg)

justify-content: center;
align-item: center;
를 해주면, 아이템을 이렇게↓ 한 가운데에 놓는 것도 매우 쉽습니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxlCcN%2FbtrIEXmijP1%2FjT91P6Nqg7wdDtQ3q0JUyk%2Fimg.jpg)

<br><br><br>

### 여러 행 정렬

### align-content

flex-wrap: wrap;이 설정된 상태에서, 아이템들의 행이 2줄 이상 되었을 때의 수직축 방향 정렬을 결정하는 속성입니다.

```css
.container {
  flex-wrap: wrap;
  align-content: stretch;
  /* align-content: flex-start; */
  /* align-content: flex-end; */
  /* align-content: center; */
  /* align-content: space-between; */
  /* align-content: space-around; */
  /* align-content: space-evenly; */
}
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FRaxoY%2FbtrIGyzZj9s%2Fla5TMtPV5DEE767tkNyYkK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F1gIvc%2FbtrIA1wDe2w%2F1cIAoEy9RcwKZ8AMEAnzwk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbbSq34%2FbtrIC0RwLVC%2FmeDZvHhQMlf41pKP8Sin5k%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FB8HTJ%2FbtrIJ7OX36v%2FKMKzSOGaZF7af8WwpmTxDk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FzApM0%2FbtrIKl7tCbX%2FuHk9KBFNZejk1HptlZl1f1%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcVHvUL%2FbtrIGzyTbtD%2F2y8dMi5oq3rPmOT2AsF8W0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FPMOTQ%2FbtrIJW7WOZU%2F8FCQd6HW1ty6SbUNYH5TUk%2Fimg.png)

위의 정렬들, justify-content랑 align-items를 보셨다면 어떤 느낌인지 이거↑ 테스트 해보시면 아실 거예요..(무책임)
정리하려다가 말이 너무 중복되는 느낌이라서요 ㅋㅋㅋ
눌러보시니까 딱 와 닿죠?
역시나 space-evenly는 MS 계열 브라우저(IE, 엣지)에서는 지원되지 않습니다👎👎

자, 이제 컨테이너에 적용하는 속성은 마무리가 되었고
이제 아이템에 적용하는 속성들에 대해 살펴 볼게요.

<br><br><br>

## **Flex 아이템에 적용하는 속성들**

### 유연한 박스의 기본 영역

### flex-basis

flex-basis는 Flex 아이템의 기본 크기를 설정합니다(flex-direction이 row일 때는 너비, column일 때는 높이).

```css
.item {
  flex-basis: auto; /* 기본값 */
  /* flex-basis: 0; */
  /* flex-basis: 50%; */
  /* flex-basis: 300px; */
  /* flex-basis: 10rem; */
  /* flex-basis: content; */
}
```

flex-basis의 값으로는 우리가 width, height 등에 사용하는 각종 단위의 수가 들어갈 수 있고요, 기본값 auto는 해당 아이템의 width값을 사용합니다. width를 따로 설정하지 않으면 컨텐츠의 크기가 되겠지요. content는 컨텐츠의 크기로, width를 따로 설정하지 않은 경우와 같아요. 좀 헷갈리죠? ㅋㅋ 일단 지금은 아이템의 기본 점유 크기를 설정한다고 생각해 주세요. 있다가 나오는 다른 속성들과 결합해서 몇가지 테스트를 하면서 좀 더 익숙해져 보겠습니다.

```css
.item {
  flex-basis: 100px;
}
```

원래의 width가 100px이 안되는 AAA와 CCC는 100px로 늘어났고, 원래 100px이 넘는 BBB는 그대로 유지되죠~

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fl68rw%2FbtrICOW0cEQ%2FkBg0kmNMiNiYaCX3oM1sNk%2Fimg.png)

반면에 width를 설정하면, 원래 100px을 넘는 BBB도 100px로 맞춰집니다.
(아래처럼 BBBBBBBBBBB가 다음 줄로 넘어가도록 하려면, CSS에 word-wrap: break-word;를 적용해주세요. 안그러면 영역만 100px로 줄어들고 BBBBBB는 옆으로 쭉- 삐져나간답니다.)

```css
.item {
  width: 100px;
}
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fby0R0i%2FbtrICY7jmt4%2FERzuEwppiciZTbs5EkV7f0%2Fimg.png)

둘 다 설정하면?

```css
.item {
  flex-basis: 100px;
  width: 100px;
}
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbwZqQH%2FbtrIGyfFR7m%2FPrUxo2MVCTpD8ZfGG6aYUK%2Fimg.png)

<br><br><br>

### 유연하게 늘리기

### flex-grow

flex-grow는 아이템이 flex-basis의 값보다 커질 수 있는지를 결정하는 속성이에요.
flex-grow에는 숫자값이 들어가는데, 몇이든 일단 0보다 큰 값이 세팅이 되면 해당 아이템이 유연한(Flexible) 박스로 변하고 원래의 크기보다 커지며 빈 공간을 메우게 됩니다.
기본값이 0이기 때문에, 따로 적용하기 전까지는 아이템이 늘어나지 않았던 거예요.

```css
.item {
  flex-grow: 1;
  /* flex-grow: 0; */ /* 기본값 */
}
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FnoQ1r%2FbtrIEZkh5RA%2FgOfZLxja7KX5kMRDwn5weK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Ftadho%2FbtrIBUcWMZ2%2FcMkks4iID4QxZ1cAoF9J1K%2Fimg.png)

flex-grow에 0과 1을 세팅한 경우
flex-grow에 들어가는 숫자의 의미는, 아이템들의 flex-basis를 제외한 **여백** 부분을 **flex-grow에 지정된 숫자의 비율**로 나누어 가진다고 생각하시면 됩니다.
이게 말로 설명하니 좀 애매한데..
아래 실제 코드가 적용된 예시와 그림을 보시면 와 닿을거예요.

```css
/* 1:2:1의 비율로 세팅할 경우 */
.item:nth-child(1) {
  flex-grow: 1;
}
.item:nth-child(2) {
  flex-grow: 2;
}
.item:nth-child(3) {
  flex-grow: 1;
}
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcfUsf5%2FbtrIC0jGRVz%2FMHITlFrXRwekpjtC3anSXK%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fuga32%2FbtrIGxVaoPm%2FNA0ZCT5yuaqG8jmXkLvUGk%2Fimg.jpg)

각 아이템의 컨텐츠가 “AAAAA”, “B”, “CCC”로 원래의 크기가 다르기 때문에 전체 아이템의 크기가 살짝 애매한 비율로 보이지만, 여백의 비로 생각해 보면 정확히 1:2:1이죠!
정수 뿐 아니라 3.141592같은 소수도 가능합니다.

<br><br><br>

### 유연하게 줄이기

### flex-shrink

flex-shrink는 flex-grow와 쌍을 이루는 속성으로, 아이템이 flex-basis의 값보다 작아질 수 있는지를 결정합니다.
flex-shrink에는 숫자값이 들어가는데, 몇이든 일단 0보다 큰 값이 세팅이 되면 해당 아이템이 유연한(Flexible) 박스로 변하고 flex-basis보다 작아집니다.
기본값이 1이기 때문에 따로 세팅하지 않았어도 아이템이 flex-basis보다 작아질 수 있었습니다.

```css
.item {
  flex-basis: 150px;
  flex-shrink: 1; /* 기본값 */
}
```

flex-shrink를 0으로 세팅하면 아이템의 크기가 flex-basis보다 작아지지 않기 때문에 고정폭의 컬럼을 쉽게 만들 수 있어요. 고정 크기는 width로 설정합니다.
아주 자주 쓰는, 이런↓ 레이아웃도 손쉽게!

```css
.container {
  display: flex;
}
.item:nth-child(1) {
  flex-shrink: 0;
  width: 100px;
}
.item:nth-child(2) {
  flex-grow: 1;
}
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F8kXtd%2FbtrIH6QLa9N%2FioSt8pgwZDgpTC3NxNOyw0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcBdhba%2FbtrIISExAiU%2FHohkYLfXGSrcrfcPzTWDb1%2Fimg.png)

컨테이너의 폭을 100%와 250px로 왔다리갔다리. flex-shrink: 0; 덕분에 컨테이너가 아무리 작아져도 첫번째 아이템은 찌그러지지 않고 폭이 100px로 유지된다.

<br><br><br>

### flex

**flex-grow, flex-shrink, flex-basis**를 한 번에 쓸 수 있는 축약형 속성입니다.
이 세 속성들은 서로 관련이 깊기 때문에, 이 축약형을 쓰는 편이 여러모로 편리합니다.

```css
.item {
  flex: 1;
  /* flex-grow: 1; flex-shrink: 1; flex-basis: 0%; */
  flex: 1 1 auto;
  /* flex-grow: 1; flex-shrink: 1; flex-basis: auto; */
  flex: 1 500px;
  /* flex-grow: 1; flex-shrink: 1; flex-basis: 500px; */
}
```

**주의할 점은, flex: 1; 이런 식으로 flex-basis를 생략해서 쓰면 flex-basis의 값은 0이 됩니다.**

축약형 flex로 좀 더 예시를 들어 볼게요.

```css
.item {
  flex: 1 1 0;
}
.item:nth-child(2) {
  flex: 2 1 0;
}
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbN50JJ%2FbtrIKlGpCeX%2FzX3bpIKLHqYKj48dJHWvH0%2Fimg.png)

flex-basis: 0; 으로, 기본 점유 크기를 0으로 만들어버려 결국 전체 크기를 1:2:1로 나누어 가져서, 영역 자체의 크기가 정확히 1:2:1의 비율로 설정되었습니다.
여백의 비가 아닌, 영역 자체를 원하는 비율로 분할하기를 원한다면 이렇게 flex-basis을 0으로 하면 손쉽게 처리할 수 있어요.

flex-wrap과 flex-basis를 이용해서 2단 컬럼의 사각형 목록을 만들어 볼게요.

```css
.container {
  display: flex;
  flex-wrap: wrap;
}
.item {
  flex: 1 1 40%;
}
```

flex-basis가 40%면, 100%에는 2개까지만 들어가므로 하나의 row에는 2개까지만 남고 다음줄로 넘어가게 되어서 2단 컬럼이 유지가 됩니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbiJgE1%2FbtrIC0jHohr%2FTHKU6sWmZxUnzykmK1PxD0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbnrg0x%2FbtrIEcdaibr%2FHV4NS514glbXDgGorktJbK%2Fimg.png)

flex: 1 1 40%는 2단, flex: 1 1 30%는 3단

<br><br><br>

### 수직축으로 아이템 정렬

### align-self

align이니 수직축 정렬이겠죠~
align-items의 아이템 버전입니다. align-items가 전체 아이템의 수직축 방향 정렬이라면, align-self는 해당 아이템의 수직축 방향 정렬입니다.

```css
.item {
  align-self: auto;
  /* align-self: stretch; */
  /* align-self: flex-start; */
  /* align-self: flex-end; */
  /* align-self: center; */
  /* align-self: baseline; */
}
```

기본값은 auto로, 기본적으로 align-items 설정을 상속 받습니다.
align-self는 align-items보다 우선권이 있어요~ 전체 설정보다 각각의 개별 설정이 우선한다는 것, 외우지 않아도 자연스럽게 다가오죠?
auto외의 나머지 값들은 align-items와 동일합니다.

아래는 align-self 값을 BBB는 center, CCC는 flex-start로 설정한 예시예요.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fn62z0%2FbtrIKmSRZWK%2FOymgwDuKsisgCb9RAXfv50%2Fimg.png)

<br><br><br>

### 배치 순서

### order

각 아이템들의 시각적 나열 순서를 결정하는 속성이에요.
숫자값이 들어가며, 작은 숫자일 수록 먼저 배치됩니다. “시각적” 순서일 뿐, HTML 자체의 구조를 바꾸는 것은 아니므로 접근성 측면에서 사용에 주의하셔야 합니다. 시각 장애인분들이 사용하는 스크린 리더로 화면을 읽을 때, order를 이용해 순서를 바꾼 것은 의미가 없다는 것을 기억해 주세요.

```css
.item:nth-child(1) {
  order: 3;
} /* A */
.item:nth-child(2) {
  order: 1;
} /* B */
.item:nth-child(3) {
  order: 2;
} /* C */
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbk1two%2FbtrIBTylPhV%2FOgK8MgoX5zD8pkDSjFB2Z1%2Fimg.png)

<br><br><br>

### z-index

z-index로 Z축 정렬을 할 수 있어요. 숫자가 클 수록 위로 올라옵니다.
(position에서의 z-index랑 똑같이 생각하시면 됩니다.)

```css
.item:nth-child(2) {
  z-index: 1;
  transform: scale(2);
}
/* z-index를 설정 안하면 0이므로, 1만 설정해도 나머지 아이템을 보다 위로 올라온다 */
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdNj3I6%2FbtrIAD2vUNm%2FdKHE49KRktX2KF4FmXajrk%2Fimg.png)

[출처](https://studiomeal.com/archives/197)
