# Deep Checking Dependencies

string끼리 비교하면 equal이 나온다.
```javascript
if ("gnar" === "gnar") {
  console.log("gnarly!!");
}
```
하지만 배열이나 object, 함수끼리는 비교하면 false가 나온다
```javascript
if ([1, 2, 3] !== [1, 2, 3]) { // 같지 않음
  console.log("but they are the same");
}
```

이것이 useEffect의 dependency array와 무슨 연관이 있을까

dependency array의 값에 array나 object같은 것들이 들어올 경우 useEffect가 계속 호출된다
예)
```javascript
function WordCount({ children = "" }) {
  useAnyKeyToRender(); //키를 누를때마다 render가 일어나는 함수

  const words = children.split(" ");

  useEffect(() => {
    console.log("fresh render"); // words값이 변하지 않는데도 계속 호출됨
  }, [words]);

  return (
    <>
      <p>{children}</p>
      <p>
        <strong>{words.length} - words</strong>
      </p>
    </>
  );
}


function App() {
  return <WordCount>You are not going to believe this but...</WordCount>;
}
```
>해결책 : useMemo

## useMemo
useMemo는 value를 기억하고 있다가 그 값으로 계산을 하는 함수다. 보통 컴퓨터 과학에서 memoization은 퍼포먼스를 높이기 위한 테크닉이다. memoized 함수에서 이전에 계산된 값은 저장되거나 cached 된다. 그 후 함수를 같은 input값으로 호출하면 저장된 캐시 값이 다시 불러와진다. 리액트에서는 **useMemo**가 cached된 값으로 비교를 함으로써 value가 정말로 변했는지 확인하는 역할을 한다.

```javascript
const words = useMemo(() => {
  const words = children.split(" ");
  return words;
}, []);

useEffect(() => {
  console.log("fresh render");
}, [words]);
```
useMemo가 words 값을 저장하고 있다가 useEffect의 dependency array안의 words와 비교하게 된다. useMemo도 dependency array를 가지고있다.

useMemo에 dependency array를 넣지 않으면 words배열이 매 렌더마다 새로 계산될것이다. 그러므로 dependency array안에 children을 넣어준다.
```javascript
function WordCount({ children = "" }) {
  useAnyKeyToRender();

  const words = useMemo(() => children.split(" "), [children]);

  useEffect(() => {
    console.log("fresh render");
  }, [words]);

  return (...);
}
```

비슷한 것으로 useCallback이 있다.
useMemo는 특정 결과값을 재사용할 때 사용하는 반면, useCallback은 특정 함수를 새로 만들지 않고 재사용 하고싶을 때 사용한다.
```javascript
const fn = () => {
  console.log("hello");
  console.log("world");
};

useEffect(() => {
  console.log("fresh render");
  fn();
}, [fn]);
```
이를 useCallback을 이용해 재 작성한다면
```javascript
const fn = useCallback(() => {
  console.log("hello");
  console.log("world");
}, []);

useEffect(() => {
  console.log("fresh render");
  fn();
}, [fn]);
```
useCallback은 fn의 값을 저장해두며, UseMemo나 useEffect처럼 dependency array를 가지고있다. 위의 경우는 dependency array가 빈 배열인 경우다.

※ 그러나 useMemo는 “컴포넌트가 무겁지 않고 자주 다른 props로 렌더된다면 그다지 필요하지는 않다.”