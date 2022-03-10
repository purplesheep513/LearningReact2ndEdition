# Children
리액트는 자식요소를 props.children 이라는 메소드를 이용해 랜더링한다. 

```javascript
  <body>
    <div id="root">
      <h1>Baked Salmon</h1>
    </div>
  </body>
```
이전 섹션에서 만든 태그를 살펴보면 h1의 자식요소로 텍스트를 랜더링했고 props.children이 Baked Salmon이라는 단어를 세팅해 준 것이다.
텍스트가 아닌 다른 React Elements도 자식요소로 랜더링이 가능하며 이를 실행하면 Elements의 트리가 생성된다. 이것이 우리가 element tree라는 용어를 쓰는 이유다

> element tree
  : 여러개의 가지를 가진 하나의 root element

예를들면 
```javascript
  <ul>
    <li>2 lb salmon</li>
    <li>5 sprigs fresh rosemary</li>
    <li>2 tablespoons olive oil</li>
    <li>2 small lemons</li>
    <li>1 teaspoon kosher salt</li>
    <li>4 cloves of chopped garlic</li>
  </ul>
```
위의 태그에서 root element는 ul태그이고 6개의 자식을 가진다. 위의 ul태그와 자식을 React.createElement를 이용해 표현하면 아래와 같다.
```javascript
  React.createElement(
    "ul",
    null,
    React.createElement("li", null, "2 lb salmon"),
    React.createElement("li", null, "5 sprigs fresh rosemary"),
    React.createElement("li", null, "2 tablespoons olive oil"),
    React.createElement("li", null, "2 small lemons"),
    React.createElement("li", null, "1 teaspoon kosher salt"),
    React.createElement("li", null, "4 cloves of chopped garlic")
  );
```

createElement로 보내진 추가적인 파라미터는 전부 첫 번째 파라미터의 자식요소가 된다.

이제 createElement가 어떻게 이루어져있는지 확인하기 위해 해당 코드를 const 키워드에 담아 console.log를 찍어본다.
```javascript
const list = React.createElement(
  "ul",
  null,
  React.createElement("li", null, "2 lb salmon"),
  React.createElement("li", null, "5 sprigs fresh rosemary"),
  React.createElement("li", null, "2 tablespoons olive oil"),
  React.createElement("li", null, "2 small lemons"),
  React.createElement("li", null, "1 teaspoon kosher salt"),
  React.createElement("li", null, "4 cloves of chopped garlic")
);

console.log(list);

//>> 결과

{
    "type": "ul",
    "props": {
    "children": [
    { "type": "li", "props": { "children": "2 lb salmon" } … },
    { "type": "li", "props": { "children": "5 sprigs fresh rosemary"} … },
    { "type": "li", "props": { "children": "2 tablespoons olive oil" } … },
    { "type": "li", "props": { "children": "2 small lemons"} … },
    { "type": "li", "props": { "children": "1 teaspoon kosher salt"} … },
    { "type": "li", "props": { "children": "4 cloves of chopped garlic"} … }
    ]
    ...
    }
}
```

children에 각각의 아이템이 들어가있는 것을 확인할 수 있다. 


리액트는 자바스크립트이기 때문에 리액트 컴포넌트 트리를 편하게 구현하기 위해 파라미터에 자바스크립트 코드를 넣을 수 있다.
위의 예제를 자바스크립트 코드를 이용해 구현해본다면
```javascript
  const items = [
    "2 lb salmon",
    "5 sprigs fresh rosemary",
    "2 tablespoons olive oil",
    "2 small lemons",
    "1 teaspoon kosher salt",
    "4 cloves of chopped garlic"
  ];

  React.createElement(
    "ul",
    { className: "ingredients" },
    items.map(ingredient => React.createElement("li", null, ingredient))
  );
```

위와 같이 표현할 수 있겠다. 하지만 이렇게 DOM을 구성할 경우 콘솔창에 아래와 같은 경고가 나타나게 된다.

```javascript
  ▶ Warning: Each child in an array or iterator should have a unique "key" prop. Check the top-level render call using <ul>. ... 이하생략
```

배열의 iterating을 이용해 자식요소를 빌드하는 경우, 리액트는 각각의 요소들이 key값을 갖는것을 권장한다. 
리액트가 DOM을 업데이트 할 때 key값을 유용하게 이용할 수 있기 때문이다.
따라서 위의 경고는 각각의 요소에 key값을 부여함으로서 제거할 수 있다.
아래와 같은 코드를 작성하자.

```javascript
  React.createElement(
    "ul",
    { className: "ingredients" },
    items.map((ingredient, i) =>
      React.createElement("li", { key: i }, ingredient)
    )
  );
```