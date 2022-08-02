# white-space 속성

white-space 속성은 pre 요소처럼 요소의 공백을 어떻게 처리할 지를 정의합니다. 또한 td 요소의 nowrap 속성을 사용하지 않고 CSS에 일률적으로 배치 금지를 지정할 수 있습니다.

white-space의 속성 값
normal, nowrap, pre, pre-wrap, pre-line

- 연속된 공백과 줄 바꿈은 메꾸어져서 하나의 공백으로 표시됩니다. 소스(Source)내의 줄 바꿈 문자도 공백 문자로써 처리됩니다. 필요하다면 긴 줄을 줄바꿈 합니다.
- normal과 같이 공백을 채우지만 가로로 긴 줄에서도 줄 바꿈을 하지 않고 표시합니다.
- 연속된 공백을 그대로 표시합니다. 또한 긴 줄도 줄 바꿈하지 않고 표시합니다.
- 연속 공백은 그대로 유지됩니다. 행(行)의 줄 바꿈은 행의 박스를 채우기 위해 필요한 경우에 실행합니다.
- 연속 공백은 메꾸어져 하나의 공백이 됩니다. 행의 줄 바꿈은 행의 박스를 메꾸기 위해 필요한 때에 실행됩니다.

<br><br>
선택자 { white-space : 속성 값; }

```html
<style>
  　.normal {white-space:normal;}
  　.nowarp{white-space:nowrap;}
  　.pre{white-space:pre;}
  　.prewrap{white-space:pre-wrap;}
  　.preline{white-space:pre-line;}
  　　　}
</style>
<p class=" ">요소의 공백문자 를 어 떻게처리할 지를 정의합니다.</p>
```

▼ 　위의 공백이 들어간 문장은, white-space의 속성 값에 따라서, 아래와 같이 표시됩니다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDQd1P%2FbtrIJVVRXT5%2FjpDk5yxJDx0rCIBWM9gsjK%2Fimg.png)

[출처](https://www.tabmode.com/homepage/white-space.html)
