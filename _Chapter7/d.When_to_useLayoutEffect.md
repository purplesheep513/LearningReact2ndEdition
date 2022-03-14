# When to useLayoutEffect
render는 useEffect이전에 일어난다. 덕분에 useEffect 안의 함수는 component의 모든 values에 접근할 수 있다. 다른 effect hook으로 useLayoutEffect가 있다.

useLayoutEffect는 렌더 사이클에 있어 특정한 순간에 불려진다.
이벤트는 다음의 순서로 이루어진다.
1. 렌더
2. useLayoutEffect 호출
3. 컴포넌트의 요소가 실제로 Dom에 붙여짐
4. useEffect 호출

이것은 다음 예제로 설명할 수 있다.
```javascript
import React, { useEffect, useLayoutEffect } from "react";

function App() {
  useEffect(() => console.log("useEffect"));
  useLayoutEffect(() => console.log("useLayoutEffect"));
  return <div>ready</div>;
}
```
App컴포넌트에서 useEffect가 첫 번째 hook이고 그 다음이 useLayoutEffect다. 그러나 렌더를 실행하면 useLayoutEffect가 useEffect보다 먼저 불러와지는 것을 확인할 수 있다.
```javascript
//App 실행 결과
useLayoutEffect
useEffect
```
useLayoutEffect는 render가 이루어고 DOM에 컴포넌트 요소가 붙여지는 사이에 호출된다. 대부분 useEffect를 사용하지만 원하는 effect가 브라우저 paint가 일어나기 전 호출되길 바란다면 useLayoutEffect를 사용하면 될 것이다.