# 7-6. HOME 구현하기

### React/한입 크기로 잘라 먹는 리액트(React.js)

<br><br><br><br>

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxsbSX%2FbtrJp0CFQdX%2FkZ6pz7bQHczYwxuWMyUGkk%2Fimg.png)

먼저 Home페이지의 상단을 구현해보겠다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fo9yeF%2FbtrJn6p7MNo%2FQlWyMmXFU5kfz8Fv12pjpK%2Fimg.png)

먼저 Home에서 아래와 같이 가운데 날짜를 들고와보자.

```js
import { useState } from "react";

const Home = () => {
  // 날짜를 저장하는 state (기본값 - 현재시간)
  const [curDate, setCurDate] = useState(new Date());
  console.log(curDate);

  return <div></div>;
};

export default Home;
```

그럼 아래와 같이 날짜와 시간이 잘 출력되는 것을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FCXpjI%2FbtrJm7pkGbo%2FEK3MKASeU1TN6Ov8UiGvwK%2Fimg.png)

다음으로는 Header를 만들어보자.

```js
import { useState } from "react";

import MyHeader from "./../components/MyHeader";

const Home = () => {
  // 날짜를 저장하는 state (기본값 - 현재시간)
  const [curDate, setCurDate] = useState(new Date());
  console.log(curDate);
  // 월은 +1씩 해줘야함
  const headText = `${curDate.getFullYear()}년 ${curDate.getMonth() + 1} 월`;

  return (
    <div>
      <MyHeader headText={headText} />
    </div>
  );
};

export default Home;
```

위와 같이 코드를 구성하면 아래와 같이 중앙에 년도와 월이 출력되게 된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxrKZa%2FbtrJpeBy4yM%2Fk2okZT2cQxGBfrRaptCTI1%2Fimg.png)

자 그럼 왼쪽과 오른쪽 버튼도 생성해보자.

```js
import { useState } from "react";

import MyHeader from "./../components/MyHeader";
import MyButton from "./../components/MyButton";

const Home = () => {
  // 날짜를 저장하는 state (기본값 - 현재시간)
  const [curDate, setCurDate] = useState(new Date());
  console.log(curDate);
  // 월은 +1씩 해줘야함
  const headText = `${curDate.getFullYear()}년 ${curDate.getMonth() + 1} 월`;

  return (
    <div>
      <MyHeader
        headText={headText}
        leftChild={<MyButton text={"<"} onClick={() => {}} />}
        rightChild={<MyButton text={">"} onClick={() => {}} />}
      />
    </div>
  );
};

export default Home;
```

자 그럼 각 버튼을 클릭할 시 월과 년도를 변화하도록 만들어보자.

```js
import { useState } from "react";

import MyHeader from "./../components/MyHeader";
import MyButton from "./../components/MyButton";

const Home = () => {
  // 날짜를 저장하는 state (기본값 - 현재시간)
  const [curDate, setCurDate] = useState(new Date());
  // 월은 +1씩 해줘야함
  const headText = `${curDate.getFullYear()}년 ${curDate.getMonth() + 1} 월`;

  const increaseMonth = () => {
    setCurDate(
      new Date(curDate.getFullYear(), curDate.getMonth() + 1, curDate.getDate())
    );
  };

  const decreaseMonth = () => {
    setCurDate(
      new Date(curDate.getFullYear(), curDate.getMonth() - 1, curDate.getDate())
    );
  };

  return (
    <div>
      <MyHeader
        headText={headText}
        leftChild={<MyButton text={"<"} onClick={decreaseMonth} />}
        rightChild={<MyButton text={">"} onClick={increaseMonth} />}
      />
    </div>
  );
};

export default Home;
```

increaseMonth와 decreaseMonth의 getMonth를 이용하여 월과 년도가 변화하도록 제작할 수 있다.

그럼 다음으로 리스트를 구현해 보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbTcvcg%2FbtrJq3yKayN%2FoU6Zd4CwpvM65heBIRIhtk%2Fimg.png)

먼저 사용할 list가 없기 때문에 범위 데이터를 사용해서 작성해 보겠다.

App 컴포넌트에서 data에서 빈데이터가 아닌 dummy data를 이용해 만들어 보자.

date는 아래와 같이 밀리세컨즈 값을 임의로 콘솔로 출력하여 사용해라.

```js
console.log(new Date().getTime());
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdaWzHj%2FbtrJq5j75Ht%2Fa4UxiHx1eDkNXqWMiL1ax0%2Fimg.png)

그래서 Home 컴포넌트에 DiaryStateContext를 추가해주면 더미데이터를 가지고 있는것을 찾을 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FA75op%2FbtrJvcbhMo9%2FmcYslse4weLDfBSLFiMEe0%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FYxwXm%2FbtrJvkAlVzP%2FC43HCIF3MoKV91wftk4epK%2Fimg.png)

자 그럼 그 날짜에 맞게 데이터들이 나타나도록 한번 설정해보자.

먼저 useEffect를 이용하여 curDate가 변화할때만 일기데이터를 뽑아올 것인데, 여기서 console로 firstDay를 뽑아오면 이달의 첫째날을 불러온다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcWv6oC%2FbtrJvQy39K4%2FTpxX04aBQnzNukQIaGgOu1%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fmm7bB%2FbtrJsOCwrJF%2F6teemegPOxu9mlRnLq5071%2Fimg.png)

그래서 lastDay도 동일하게 아래와 같이 출력된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbl29Fq%2FbtrJuDgaBMT%2FCKg1JOh4DGBU9CLrHkpV21%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FKrvNR%2FbtrJu03eR3l%2FFcZ6fp0EbC3VBceKG7YD51%2Fimg.png)

그래서 우리는 firstDay와 lastDay사이에 있는 diary들만 들고오면 되는 것이다.

그래서 아래와 같이 범위를 지정해주면 된다.

```js
setData(diaryList.filter((it) => firstDay <= it.data && it.data <= lastDay));
```

근데 여기서 diaryList를 전달해줘야한다.

diaryList를 전달하는 것은 이에대해 CRUD가 작동했다는 것인데 그때 list도 변경되어야 하기때문에 depth에 diaryList를 넣으면 된다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbKpcZx%2FbtrJq40abGv%2Fk9KlgJvcfQJEIKK2zavKw1%2Fimg.png)

자 그럼 useEffect로 정상적으로 작동하는지 확인해보자.

```js
useEffect(() => {
  console.log(data);
}, [data]);
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FwCmMC%2FbtrJvaSjSFN%2FnnPV1xPJznaklZpiRLh16k%2Fimg.png)

dummy에 한참 차이나는 date를 넣으면 그것은 뜨지 않음으로 날짜에 맞게 데이터 전달이 잘 된것을 확인할 수 있다.

그리고 firstDay와 lastDay 계산하는 작업이 오래걸리는 작업이기 때문에, diaryList 가 1 이상일때만 실행할 수 있도록 하면 시간절약을 할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FEWlCO%2FbtrJwZCBHDU%2FD94P3Oj1wG6kcdg7tki8PK%2Fimg.png)

자 그럼 다이어리의 리스트를 별도의 컴포넌트로 분할해서 작성해보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FscrTr%2FbtrJt4FpmdC%2FsYtZ335aNW37uFW2wvkfok%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcgyJE2%2FbtrJuR6RA66%2FsC9kfJ6L44nt1shQ9ZcJAk%2Fimg.png)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcMogPU%2FbtrJvQMWIjE%2Fte9sgmgEUWkEmP6qdRqKv1%2Fimg.png)

그러면 위와 같이 정상적으로 출력이 된다.

근데 여기서 prop이 정상적으로 전달이 안될 수 있으니 defaultProp을 사용하자!(빈배열)

```js
const DiaryList = ({ diaryList }) => {
  return (
    <div>
      {diaryList.map((it) => (
        <div key={it.id}>{it.content}</div>
      ))}
    </div>
  );
};

DiaryList.defaultProps = {
  diaryList: [],
};

export default DiaryList;
```

<br><br>

자 그럼 이제는 필터를 한번 구현해 보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdIIeWc%2FbtrJsPV5lRC%2F6PS3OFeGtuEKyDKKT1y8W1%2Fimg.png)

자 먼저 정렬을 위한 함수를 하나 만들어보자.

이 함수에서 전달하는 props들을 먼저 살펴보자면

value - select가 어떤것을 선택하고 있는지

onChange - select가 선택한것을 바꿀때 사용하는 함수

optionList - select안에 들어갈 option

```js
const ControlMenu = ({ value, onChange, optionList }) => {
  return <select></select>;
};
```

자 그럼 정렬부터 만들어보자.

먼저 value 중

최신순과 오래된 순의 select박스를 만들고,

```js
import { useState } from "react";

const sortOptionList = [
  { value: "latest", name: "최신순" },
  { value: "oldest", name: "오래된순" },
];
// value - select가 어떤것을 선택하고 있는지
// onChange - select가 변경했을 때 바꿀 함수
// optionList - select 안에 들어갈 option
const ControlMenu = ({ value, onChange, optionList }) => {
  return (
    <select value={value} onChange={(e) => onChange(e.target.value)}>
      {optionList.map((it, idx) => (
        <option key={idx} value={it.value}>
          {it.name}
        </option>
      ))}
    </select>
  );
};

const DiaryList = ({ diaryList }) => {
  // 정렬 (초기값 - lastest)
  const [sortType, setSortType] = useState("lastest");

  return (
    <div>
      <ControlMenu
        value={sortType}
        onChange={setSortType}
        optionList={sortOptionList}
      />
      {diaryList.map((it) => (
        <div key={it.id}>{it.content}</div>
      ))}
    </div>
  );
};

DiaryList.defaultProps = {
  diaryList: [],
};

export default DiaryList;
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcGxVfT%2FbtrJrP9M7kp%2FSOHQG3bwUylJOc1x25b5o0%2Fimg.png);

onChange함수에 따라 정렬을 해보자

근데 sort를 사용하면 원본 데이터가 정렬을 당함으로

배열을 copy해보자! (깊은 복사)

```js
const copyList = JSON.parse(JSON.stringify(diaryList));
```

이는 diaryList를 JSON화 시켜서 문자화 시켜버린다!

그래서 다시 parse를 하면 다시 복호화 시켜준다!

이렇게 하고 copyList에 넣어주는 것이다.

그래서 값만 건드리고 원본은 건드리지 않고 수행했음을 알 수 있다.

자 이제 진짜 정렬을 해보자. 우선 정렬을 위해 비교함수를 만들어보자.

```js
const getProcessedDiaryList = () => {
  const compare = (a, b) => {
    if (sortType === "latest") {
      return parseInt(b.date) - parseInt(a.date);
    } else {
      return parseInt(a.date) - parseInt(b.date);
    }
  };
  // 이는 diaryList를 JSON화 시켜서 문자화 시켜버린다!
  // 그래서 다시 parse를 하면 다시 복호화 시켜준다!
  // 이렇게 하고 copyList에 넣어주는 것이다
  // 그래서 값만 건드리고 원본은 건드리지 않고 수행했음을 알 수 있다
  const copyList = JSON.parse(JSON.stringify(diaryList));
  const sortedList = copyList.sort(compare);
  return sortedList;
};
```

그래서 getProcessedDiaryList를 mapping하는 함수를 만들어야 한다.

```js
import { useState } from "react";

const sortOptionList = [
  { value: "latest", name: "최신순" },
  { value: "oldest", name: "오래된순" },
];
// value - select가 어떤것을 선택하고 있는지
// onChange - select가 변경했을 때 바꿀 함수
// optionList - select 안에 들어갈 option
const ControlMenu = ({ value, onChange, optionList }) => {
  return (
    <select value={value} onChange={(e) => onChange(e.target.value)}>
      {optionList.map((it, idx) => (
        <option key={idx} value={it.value}>
          {it.name}
        </option>
      ))}
    </select>
  );
};

const DiaryList = ({ diaryList }) => {
  // 정렬 (초기값 - latest)
  const [sortType, setSortType] = useState("latest");

  const getProcessedDiaryList = () => {
    const compare = (a, b) => {
      if (sortType === "latest") {
        return parseInt(b.date) - parseInt(a.date);
      } else {
        return parseInt(a.date) - parseInt(b.date);
      }
    };
    // 이는 diaryList를 JSON화 시켜서 문자화 시켜버린다!
    // 그래서 다시 parse를 하면 다시 복호화 시켜준다!
    // 이렇게 하고 copyList에 넣어주는 것이다
    // 그래서 값만 건드리고 원본은 건드리지 않고 수행했음을 알 수 있다
    const copyList = JSON.parse(JSON.stringify(diaryList));
    const sortedList = copyList.sort(compare);
    return sortedList;
  };

  return (
    <div>
      <ControlMenu
        value={sortType}
        onChange={setSortType}
        optionList={sortOptionList}
      />
      {getProcessedDiaryList().map((it) => (
        <div key={it.id}>{it.content}</div>
      ))}
    </div>
  );
};

DiaryList.defaultProps = {
  diaryList: [],
};

export default DiaryList;
```

그러면 정렬이 잘 되는 것을 확인할 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F2NyzP%2FbtrJwqtF3Py%2FP5lq1sXVR8U2981q3dW77k%2Fimg.png);

그럼 우리 두번째 감정 필터를 만들어보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FOJfUQ%2FbtrJvbwXsbe%2FBdTKfwafMUjAwf4D6ngThK%2Fimg.png);

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqccwT%2FbtrJt4eoYeb%2FQOmiPPiF3EnNd6z4DaxhY1%2Fimg.png);

```js
import { useState } from "react";

const sortOptionList = [
  { value: "latest", name: "최신순" },
  { value: "oldest", name: "오래된순" },
];

const filterOptionList = [
  { value: "all", name: "전부 다" },
  { value: "good", name: "좋은 감정만" },
  { value: "bad", name: "안 좋은 감정만" },
];

// value - select가 어떤것을 선택하고 있는지
// onChange - select가 변경했을 때 바꿀 함수
// optionList - select 안에 들어갈 option
const ControlMenu = ({ value, onChange, optionList }) => {
  return (
    <select value={value} onChange={(e) => onChange(e.target.value)}>
      {optionList.map((it, idx) => (
        <option key={idx} value={it.value}>
          {it.name}
        </option>
      ))}
    </select>
  );
};

const DiaryList = ({ diaryList }) => {
  // 정렬 (초기값 - latest)
  const [sortType, setSortType] = useState("latest");
  const [filter, setFilter] = useState("all");

  const getProcessedDiaryList = () => {
    const compare = (a, b) => {
      if (sortType === "latest") {
        return parseInt(b.date) - parseInt(a.date);
      } else {
        return parseInt(a.date) - parseInt(b.date);
      }
    };
    // 이는 diaryList를 JSON화 시켜서 문자화 시켜버린다!
    // 그래서 다시 parse를 하면 다시 복호화 시켜준다!
    // 이렇게 하고 copyList에 넣어주는 것이다
    // 그래서 값만 건드리고 원본은 건드리지 않고 수행했음을 알 수 있다
    const copyList = JSON.parse(JSON.stringify(diaryList));
    const sortedList = copyList.sort(compare);
    return sortedList;
  };

  return (
    <div>
      <ControlMenu
        value={sortType}
        onChange={setSortType}
        optionList={sortOptionList}
      />
      <ControlMenu
        value={filter}
        onChange={setFilter}
        optionList={filterOptionList}
      />
      {getProcessedDiaryList().map((it) => (
        <div key={it.id}>
          {it.content} {it.emotion}
        </div>
      ))}
    </div>
  );
};

DiaryList.defaultProps = {
  diaryList: [],
};

export default DiaryList;
```

자 그럼 이제 필터를 씌워보겠다.

우선 감정이 수치로 나타내어져있기 때문에 3이하는 좋은 감정, 3이상은 나쁜감정으로 취급하는 함수를 생성하고

```js
const filterCallBack = (item) => {
  if (filter === "good") {
    return parseInt(item.emotion) <= 3;
  } else {
    return parseInt(item.emotion) > 3;
  }
};
```

다음과 같이 한번 더 필터링을 하여 화면에 출력하도록 생성하면된다.

```js
const copyList = JSON.parse(JSON.stringify(diaryList));
const filterLists =
  filter === "all" ? copyList : copyList.filter((it) => filterCallBack(it));
const sortedList = filterLists.sort(compare);
return sortedList;
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbu1V80%2FbtrJxoClZB4%2FoCS9ArurXGZTAQ9sKEK0J0%2Fimg.png);

자 그럼 새 일기쓰기 버튼을 만들어보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbbsk2n%2FbtrJvRkPtbZ%2FtkRiPuaaquymrkDXQfvM70%2Fimg.png);

```js
import { useState } from "react";
import { useNavigate } from "react-router-dom";
import MyButton from "./MyButton";

const sortOptionList = [
  { value: "latest", name: "최신순" },
  { value: "oldest", name: "오래된순" },
];

const filterOptionList = [
  { value: "all", name: "전부 다" },
  { value: "good", name: "좋은 감정만" },
  { value: "bad", name: "안 좋은 감정만" },
];

// value - select가 어떤것을 선택하고 있는지
// onChange - select가 변경했을 때 바꿀 함수
// optionList - select 안에 들어갈 option
const ControlMenu = ({ value, onChange, optionList }) => {
  return (
    <select value={value} onChange={(e) => onChange(e.target.value)}>
      {optionList.map((it, idx) => (
        <option key={idx} value={it.value}>
          {it.name}
        </option>
      ))}
    </select>
  );
};

const DiaryList = ({ diaryList }) => {
  const navigate = useNavigate();
  // 정렬 (초기값 - latest)
  const [sortType, setSortType] = useState("latest");
  const [filter, setFilter] = useState("all");

  const getProcessedDiaryList = () => {
    const filterCallBack = (item) => {
      if (filter === "good") {
        return parseInt(item.emotion) <= 3;
      } else {
        return parseInt(item.emotion) > 3;
      }
    };

    const compare = (a, b) => {
      if (sortType === "latest") {
        return parseInt(b.date) - parseInt(a.date);
      } else {
        return parseInt(a.date) - parseInt(b.date);
      }
    };
    // 이는 diaryList를 JSON화 시켜서 문자화 시켜버린다!
    // 그래서 다시 parse를 하면 다시 복호화 시켜준다!
    // 이렇게 하고 copyList에 넣어주는 것이다
    // 그래서 값만 건드리고 원본은 건드리지 않고 수행했음을 알 수 있다
    const copyList = JSON.parse(JSON.stringify(diaryList));
    const filterLists =
      filter === "all" ? copyList : copyList.filter((it) => filterCallBack(it));
    const sortedList = filterLists.sort(compare);
    return sortedList;
  };

  return (
    <div>
      <ControlMenu
        value={sortType}
        onChange={setSortType}
        optionList={sortOptionList}
      />
      <ControlMenu
        value={filter}
        onChange={setFilter}
        optionList={filterOptionList}
      />
      <MyButton
        type={"positive"}
        text={"새 일기쓰기"}
        onClick={() => navigate("/new")}
      />
      {getProcessedDiaryList().map((it) => (
        <div key={it.id}>
          {it.content} {it.emotion}
        </div>
      ))}
    </div>
  );
};

DiaryList.defaultProps = {
  diaryList: [],
};

export default DiaryList;
```

Navigate기능도 탑재하여 new페이지로 이동도 가능하게 제작하였다.

그럼 이제 스타일링 작업을 해보도록 하겠다.

```css
/* DiaryList */

.DiaryList .menu_wrapper {
  margin-top: 20px;
  margin-bottom: 30px;

  display: flex;
  justify-content: space-between;
}

.DiaryList .menu_wrapper .right_col {
  flex-grow: 1;
}

.DiaryList .menu_wrapper .right_col button {
  width: 100%;
}

.DiaryList .ControlMenu {
  margin-right: 10px;
  border: none;
  border-radius: 5px;
  background-color: #ececec;

  padding-top: 10px;
  padding-bottom: 10px;
  padding-left: 20px;
  padding-right: 20px;

  cursor: pointer;
  font-family: "Nanum Pen Script";
  font-size: 18px;
}
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbuGYMM%2FbtrJsPV9wBB%2Fv2pMqUTtXT3gRjEcOpo3ok%2Fimg.png);

자 그럼 우리 이제 일기 컴포넌트를 만들어보자.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FXRqhq%2FbtrJvRZrc6G%2FqsUJmr3AltJ54yspkwrSL0%2Fimg.png);

그럼 DiaryItem으로 새로운 컴포넌트를 만들자.

##### DiaryList.js

```js
import { useState } from "react";
import { useNavigate } from "react-router-dom";
import MyButton from "./MyButton";
import DiaryItem from "./DiaryItem";

const sortOptionList = [
  { value: "latest", name: "최신순" },
  { value: "oldest", name: "오래된순" },
];

const filterOptionList = [
  { value: "all", name: "전부 다" },
  { value: "good", name: "좋은 감정만" },
  { value: "bad", name: "안 좋은 감정만" },
];

// value - select가 어떤것을 선택하고 있는지
// onChange - select가 변경했을 때 바꿀 함수
// optionList - select 안에 들어갈 option
const ControlMenu = ({ value, onChange, optionList }) => {
  return (
    <select
      className="ControlMenu"
      value={value}
      onChange={(e) => onChange(e.target.value)}
    >
      {optionList.map((it, idx) => (
        <option key={idx} value={it.value}>
          {it.name}
        </option>
      ))}
    </select>
  );
};

const DiaryList = ({ diaryList }) => {
  const navigate = useNavigate();
  // 정렬 (초기값 - latest)
  const [sortType, setSortType] = useState("latest");
  const [filter, setFilter] = useState("all");

  const getProcessedDiaryList = () => {
    const filterCallBack = (item) => {
      if (filter === "good") {
        return parseInt(item.emotion) <= 3;
      } else {
        return parseInt(item.emotion) > 3;
      }
    };

    const compare = (a, b) => {
      if (sortType === "latest") {
        return parseInt(b.date) - parseInt(a.date);
      } else {
        return parseInt(a.date) - parseInt(b.date);
      }
    };
    // 이는 diaryList를 JSON화 시켜서 문자화 시켜버린다!
    // 그래서 다시 parse를 하면 다시 복호화 시켜준다!
    // 이렇게 하고 copyList에 넣어주는 것이다
    // 그래서 값만 건드리고 원본은 건드리지 않고 수행했음을 알 수 있다
    const copyList = JSON.parse(JSON.stringify(diaryList));
    const filterLists =
      filter === "all" ? copyList : copyList.filter((it) => filterCallBack(it));
    const sortedList = filterLists.sort(compare);
    return sortedList;
  };

  return (
    <div className="DiaryList">
      <div className="menu_wrapper">
        <div className="left_col">
          <ControlMenu
            value={sortType}
            onChange={setSortType}
            optionList={sortOptionList}
          />
          <ControlMenu
            value={filter}
            onChange={setFilter}
            optionList={filterOptionList}
          />
        </div>
        <div className="right_col">
          <MyButton
            type={"positive"}
            text={"새 일기쓰기"}
            onClick={() => navigate("/new")}
          />
        </div>
      </div>

      {getProcessedDiaryList().map((it) => (
        <DiaryItem key={it.id} {...it} />
      ))}
    </div>
  );
};

DiaryList.defaultProps = {
  diaryList: [],
};

export default DiaryList;
```

##### DiaryItem.js

```js
import { useNavigate } from "react-router-dom";
import MyButton from "./MyButton";

const DiaryItem = ({ id, emotion, content, date }) => {
  const navigate = useNavigate();

  const env = process.env;
  env.PUBLIC_URL = env.PUBLIC_URL || "";

  // 숫자데이터를 년월일로 알아보기 쉽게 변환
  const strDate = new Date(parseInt(date)).toLocaleDateString();
  const goDetail = () => {
    navigate(`/diary/${id}`);
  };
  const goEdit = () => {
    navigate(`/eidt/${id}`);
  };

  return (
    <div className="DiaryItem">
      <div
        onClick={goDetail}
        className={[
          "emotion_img_wrapper",
          `emotion_img_wrapper_${emotion}`,
        ].join(" ")}
      >
        <img src={process.env.PUBLIC_URL + `assets/emotion${emotion}.png`} />
      </div>
      <div onClick={goDetail} className="info_wrapper">
        <div className="diary_date">{strDate}</div>
        <div className="diary_content_preview">{content.slice(0, 25)}</div>
      </div>
      <div className="btn_wrapper">
        <MyButton onClick={goEdit} text={"수정하기"} />
      </div>
    </div>
  );
};

export default DiaryItem;
```

##### App.css

```css
@import url("https://fonts.googleapis.com/css2?family=Nanum+Pen+Script&family=Yeon+Sung&display=swap");

body {
  background-color: #f6f6f6;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: "Nanum Pen Script";
  min-height: 100vh;
  margin: 0px;
}

/_
  가로가
  650
  미만일때만
  작동됨
  _/
  /_
  min
  또는
  max로
  width
  최대
  최소로
  조건을
  준다
  _/
  @media
  (min-width: 650px) {
  .App {
    width: 640px;
  }
}

@media (max-width: 650px) {
  .App {
    width: 90vw;
  }
}

#root {
  background-color: white;
  box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
}

.App {
  min-height: 100vh;
  padding-left: 20px;
  padding-right: 20px;
}

/_ MyButton _/ .MyButton {
  cursor: pointer;
  border: none;
  border-radius: 5px;

  padding-top: 10px;
  padding-bottom: 10px;
  padding-left: 20px;
  padding-right: 20px;

  font-size: 18px;

  white-space: nowrap;
  font-family: "Nanum Pen Script";
}

.MyButton_default {
  background-color: #ececec;
  color: black;
}

.MyButton_positive {
  background-color: #64c964;
  color: white;
}

.MyButton_negative {
  background-color: #fd565f;
  color: white;
}

/_ HEADER _/ header {
  padding-top: 20px;
  padding-bottom: 20px;

  display: flex;
  align-items: center;
  border-bottom: 1px solid #e2e2ee;
}

header > div {
  display: flex;
}

header .head_text {
  width: 50%;
  font-size: 25px;
  justify-content: center;
}

header .head_btn_left {
  width: 25%;
  justify-content: start;
}

header .head_btn_right {
  width: 25%;
  justify-content: end;
}

header button {
  font-family: "Nanum Pen Script";
}

/_ DiaryList _/ .DiaryList .menu_wrapper {
  margin-top: 20px;
  margin-bottom: 30px;

  display: flex;
  justify-content: space-between;
}

.DiaryList .menu_wrapper .right_col {
  flex-grow: 1;
}

.DiaryList .menu_wrapper .right_col button {
  width: 100%;
}

.DiaryList .ControlMenu {
  margin-right: 10px;
  border: none;
  border-radius: 5px;
  background-color: #ececec;

  padding-top: 10px;
  padding-bottom: 10px;
  padding-left: 20px;
  padding-right: 20px;

  cursor: pointer;
  font-family: "Nanum Pen Script";
  font-size: 18px;
}

/_ DiaryItem _/ .DiaryItem {
  padding-top: 15px;
  padding-bottom: 15px;

  border-bottom: 1px solid #e2e2e2;

  display: flex;
  justify-content: space-between;
}

.DiaryItem .emotion_img_wrapper {
  cursor: pointer;
  min-width: 120px;
  height: 80px;
  border-radius: 5px;
  display: flex;
  justify-content: center;
}

.DiaryItem .emotion_img_wrapper_1 {
  background-color: #64c964;
}

.DiaryItem .emotion_img_wrapper_2 {
  background-color: #9dd772;
}

.DiaryItem .emotion_img_wrapper_3 {
  background-color: #fdce17;
}

.DiaryItem .emotion_img_wrapper_4 {
  background-color: #fd8446;
}

.DiaryItem .emotion_img_wrapper_5 {
  background-color: #fd565f;
}

.DiaryItem .emotion_img_wrapper img {
  width: 50%;
}

.DiaryItem .info_wrapper {
  flex-grow: 1;
  margin: 20px;
  cursor: pointer;
}

.DiaryItem .diary_date {
  font-weight: bold;
  font-size: 25px;
  margin-bottom: 5px;
}

.DiaryItem .diary_content_preview {
  font-size: 18px;
}

.DiaryItem .btn_wrapper {
  min-width: 70px;
}
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbJJTkI%2FbtrJt3zODq0%2FqpCKLkoiBD8ECMFczK6zk0%2Fimg.png);

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FQNBej%2FbtrJuCIDsTn%2FWZRA3aS5WG5x05Jd5uE1g0%2Fimg.png);

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbC49lu%2FbtrJvbjtzry%2Fk5fbClsVDWfXhyFKDgZ761%2Fimg.png);
