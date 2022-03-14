# The Dependency Array
useEffect는 useState나 (지금까지는 언급되지 않았던 useReducer)같이 state를 관리해주는 Hooks와 결합해서 작동하도록 디자인 되었다.

아래의 2가지 state를 가진 예를 살펴보면

```javascript
import React, { useState, useEffect } from "react";
import "./App.css";

function App() {
  const [val, set] = useState("");
  const [phrase, setPhrase] = useState("example phrase");

  const createPhrase = () => {
    setPhrase(val);
    set("");
  };

  useEffect(() => {
    console.log(`typing "${val}"`);
  });

  useEffect(() => {
    console.log(`saved phrase: "${phrase}"`);
  });

  return (
    <>
      <label>Favorite phrase:</label>
      <input
        value={val}
        placeholder={phrase}
        onChange={e => set(e.target.value)}
      />
      <button onClick={createPhrase}>send</button>
    </>
  );
}
```
val은 input박스의 value를 나타낸다. val은 input박스 안의 값이 변할 때마다 변화한다. 그리고 send버튼을 누른다면 input박스의 value가 한 phrase로 저장돼 val은 ""로 리셋된다.

이러한 방법은 개발자가 의도한대로 작동된다. 그러나 위의 코드대로 실행한다면 useEffect hook이 필요 이상으로 매번 호출된다는 문제점이 있다. render가 일어난 이후 위의 코드의 useEffect는 다음과 같이 호출된다.

```javascript
typing ""                             // First Render
saved phrase: "example phrase"        // First Render
typing "S"                            // Second Render
saved phrase: "example phrase"        // Second Render
typing "Sh"                           // Third Render
saved phrase: "example phrase"        // Third Render
typing "Shr"                          // Fourth Render
saved phrase: "example phrase"        // Fourth Render
typing "Shre"                         // Fifth Render
saved phrase: "example phrase"        // Fifth Render
typing "Shred"                        // Sixth Render
saved phrase: "example phrase"        // Sixth Render
```

이와같이 매번 이벤트가 일어나는것은 비효율적이다. useEffect가 특정 데이터가 변화할때만 일어난다면 조금 더 효율적인 코드가 될 것이다. 이러한 문제점을 해결하기 위해 dependency array라는 것을 도입할 수 있다. dependency array는 useEffect등의 함수가 호출되는 것을 통제하기 위해 사용된다.

다음과같은 예를 보자
```javascript
useEffect(() => {
  console.log(`typing "${val}"`);
}, [val]);

useEffect(() => {
  console.log(`saved phrase: "${phrase}"`);
}, [phrase]);
```
위 코드는 useEffect함수 안에 [val]이나 [phrase]배열을 추가했다.
첫 번째 useEffect는 val이 바뀔때마다 실행되고 두 번째 useEffect는 phrase가 바뀌면 실행된다. 따라서 다음과 같은 갱신이 일어날 것으로 예상할 수 있다.

```javascript
typing ""                              // First Render
saved phrase: "example phrase"         // First Render
typing "S"                             // Second Render
typing "Sh"                            // Third Render
typing "Shr"                           // Fourth Render
typing "Shre"                          // Fifth Render
typing "Shred"                         // Sixth Render
typing ""                              // Seventh Render
saved phrase: "Shred"                  // Seventh Render
```
위와 같이 필요한 만큼만 렌더링 되는 것을 확인할 수 있다.
배열 안에는 여러 value를 넣을 수 있다. 배열 안의 value가 변화할 때마다 effect가 일어난다.

* 빈 배열을 넣을 때에는? 최초의 render가 일어났을때만 effect가 일어난다.

예를들면 
```javascript
useEffect(() => {
  welcomeChime.play();
}, []);
```
위의 코드를 사용한다면 render가 일어난 후 welcome song이 실행될 것이다.
만약, 컴포넌트 트리가 제거된 이후 메서드를 실행하려고한다면 아래의 코드를 사용한다.
```javascript
useEffect(() => {
  welcomeChime.play();
  return () => goodbyeChime.play();
}, []);
```
render가 일어난 후 welcome song이 한 번 실행되고 component가 tree에서 사라진 후에는 goodbye song이 실행될 것이다.

이러한 패턴은 여러 방면으로 유용하게 사용될 수 있다.

예)
1. 사용자가 첫번째 렌더이후 news feed를 구독한다
2. 그 후 그 news feed를 구독 취소한다.

좀더 자세히 설명하자면, 사용자는 posts라는 state value를 생성하는 것으로 이벤트를 시작한다. 그리고 그 state value를 변경하기 위한 함수로는 setposts를 이용할 것이다.

그리고나서 addPosts라는 함수를 생성하고 그것은 최신 뉴스 post를 받아와 배열에 추가시킬 것이다. 그 후 useEffect를 사용해 news feed를 구독하고 그 때 welcome song을 듣는다.


* 정리해보자면
  * 최초 렌더(mount)됐을 때 useEffect안의 함수가 실행된다.
  * dependency array안의 prop이나 state가 변경될 때(update) useEffect안의 함수가 실행된다.
  * 컴포넌트가 제거(unmount)되면 useEffect안의 return이 실행된다.

>용어정리

mount : 최초의 렌더링
update : props나 state가 바뀌는 경우
unmount : component 삭제

