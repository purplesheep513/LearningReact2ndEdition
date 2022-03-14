# Introducing useEffect

컴포넌트는 사용자 인터페이스에 렌더되는 간단한 함수다.
렌더는 앱이 처음으로 로드되거나, props/state가 변할 때 이루어진다.
그렇다면 render가 되고난 후 작업을 해야할 때에는 어떻게 해야할까?
</br>
</br>


체크박스 컴포넌트를 예로 들어보자. useState를 이용해 유저가 체크박스에 체크하거나 체크를 해제하며 컴포넌트의 value를 관리할 수 있다. 그렇다면 체크박스 체크하는 이벤트가 일어난 다음에 사용자에게 일어난 이벤트에 대해 알릴 방법은 무엇일까?

> alert메서드를 이용해 예를 들어보겠다.

```javascript
import React, { useState } from "react";

function Checkbox() {
  const [checked, setChecked] = useState(false);

  alert(`checked: ${checked.toString()}`);

  return (
    <>
      <input
        type="checkbox"
        value={checked}
        onChange={() => setChecked(checked => !checked)}
      />
      {checked ? "checked" : "not checked"}
    </>
  );
};
```

위의 예시는 return이 일어나기 전에 alert를 정의했다. return 이하의 컴포넌트는 유저가 alert의 ok버튼을 누르기 이전에는 렌더링되지 않는다. alert함수가 렌더링을 막고있기 때문에 ok버튼을 누를 때 까지 렌더링 된 체크박스의 다음 상태를 볼 수 없는 것이다.

이것은 의도했던 바가 아니므로, 다음과 같이 return이후에 alert 메서드를 위치시켜야 하는지 생각해보게 된다.

```javascript
function Checkbox {
  const [checked, setChecked] = useState(false);

  return (
    <>
      <input
        type="checkbox"
        value={checked}
        onChange={() => setChecked(checked => !checked)}
      />
      {checked ? "checked" : "not checked"}
    </>
  );

  // return 후에 alert 위치
  alert(`checked: ${checked.toString()}`);
};
```
그러나 return이 일어난 후에는 메서드를 호출할 수 없다. return후에는 코드실행이 되지 않기 때문이다.

그러므로 우리가 원하는 방향대로 alert함수가 호출되게 하려면 useEffect를 사용해야한다.</br>
useEffect 안에 alert메서드를 위치시킨다면 render가 모두 일어난 후에 alert함수를 실행시키라는 뜻이 된다.

```javascript
function Checkbox {
  const [checked, setChecked] = useState(false);

  useEffect(() => {
    alert(`checked: ${checked.toString()}`);
  });

  return (
    <>
      <input
        type="checkbox"
        value={checked}
        onChange={() => setChecked(checked => !checked)}
      />
      {checked ? "checked" : "not checked"}
    </>
  );
};
```

alert, console.log, Native API 등은 render의 일부분이 아니다. 그러므로 리액트 엡에서는 렌더가(return안의 것) 이러한 이벤트 이후에 일어나게 된다. useEffect를 사용하게 된다면 render이후에 이벤트가 일어나게 해 컴포넌트의 변경된 값을 이벤트에 전달할 수 있게된다.
