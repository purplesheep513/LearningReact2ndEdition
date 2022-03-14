# Improving Component Performance

```javascript
const Cat = ({ name }) => {
  console.log(`rendering ${name}`);
  return <p>{name}</p>;
};

function App() {
  const [cats, setCats] = useState(["Biscuit", "Jungle", "Outlaw"]);
  return (
    <>
      {cats.map((name, i) => (
        <Cat key={i} name={name} />
      ))}
      <button onClick={() => setCats([...cats, prompt("Name a cat")])}>
        Add a Cat
      </button>
    </>
  );
}
```
=> 이 컴포넌트를 사용했을 때 console.log의 결과
```javascript
rendering Biscuit
rendering Jungle
rendering Outlaw
```

여기서 cats에 "Ripple"을 추가한다면 모든 Cat 컴포넌트가 렌더될것이다
```javascript
rendering Biscuit
rendering Jungle
rendering Outlaw
rendering Ripple
```

cat에 이름을 추가할때마다 모든 Cat컴포넌트들이 렌더된다. 그러나 Cat컴포넌트는 변화가 없는 pure컴포넌트다. 이때 memo 함수를 쓴다면.. 이 함수는 property에 변화가 있을 때에만 컴포넌트를 렌더해준다.

그리하여 아래와 같이 코드를 작성한다
```javascript
import React, { useState, memo } from "react";

const Cat = ({ name }) => {
  console.log(`rendering ${name}`);
  return (
    <>
      cats.map((name, i) => <PureCat key={i} name={name} />);  
    </>
  );
};

const PureCat = memo(Cat);
```
cat에 "Pancake"이라는 이름을 추가한다면 console.log에는
```javascript
rendering Pancake
```
만 출력된다.