# React Fragments

다음과 같은 리액트 코드가 있다.
```javascript
function Cat({ name }) {
  return <h1>The cat's name is {name}</h1>;
}

ReactDOM.render(<Cat name="Jungle" />, document.getElementById("root"));
```

해당 코드는 ReactDOM에 의해 다음과 같이 렌더링될것이다.
```javascript
<div id="root">
  <h1>The cat's name is Jungle</h1>
</div>
```

> Cat컴포넌트에 다른 문구를 추가하고 싶다면?
>>직관적으로 생각해 아래와 같은 컴포넌트 형태를 만들어본다.
```javascript
function Cat({ name }) {
  return (
    <h1>The cat's name is {name}</h1>
    <p>He's good.</p>
  );
}
```
그러나 위의 코드는 `Adjacent JSX elements must be wrapped in an enclosing tag`라는 에러를 출력하며 fragment를 이용하라고 할것이다.

#### **이유** : 리액트는 한 번에 두 태그를 렌더링하지 못한다. 그러므고 여러 태그를 추가하고싶다면 div태그 등을 이용해 태그들을 감싸주어야한다.

```javascript
function Cat({ name }) {
  return (
    <div>
      <h1>The cat's name is {name}</h1>
      <p>He's good.</p>
    </div>
  );
}
```
그러나 이는 필요없는 태그를 생성한다. 개발자 도구를 열어서 element탭을 확인해보면
```javascript
<div>
  <h1>The cat's name is {name}</h1>
  <p>He's good.</p>
</div>
```
와 같이 필요없는 div태그가 들어가있는 것을 볼 수 있다. <React.Fragment> 태그를 쓴다면 쓸모없는 태그를 생성하지 않으면서 여러 태그를 감싸는 역할을 수행할 수 있다.
```javascript
function Cat({ name }) {
  return (
    <React.Fragment>
      <h1>The cat's name is {name}</h1>
      <p>He's good.</p>
    </React.Fragment>
  );
}
```
위의 코드를 개발자 도구를 열어서 element탭을 확인하면

```javascript
<h1>The cat's name is {name}</h1>
<p>He's good.</p>
```

 <React.Fragment> 태그 말고 빈 태그 <></>를 사용해도 된다.

 ```javascript
function Cat({ name }) {
  return (
    <>
      <h1>The cat's name is {name}</h1>
      <p>He's good.</p>
    </>
  );
}
```