# 리액트 컴포넌트 역사여행

이전 섹션에서 리액트 컴포넌트를 함수형으로 생성하는 법을 알아봤다.
그러나 이전에는 컴포넌트를 생성하기 위해 다른 방법들이 존재했다.

1. createClass
2013년 리액트가 처음 만들어 졌을 당시, 리액트 컴포넌트를 만들기 위한 유일한 방법은 createClass함수를 사용하는 것이었다.
React.createClass 메서드를 이용하면 됐다
```javascript
  const IngredientsList = React.createClass({
    displayName: "IngredientsList",
    render() {
      return React.createElement(
        "ul",
        { className: "ingredients" },
        this.props.items.map((ingredient, i) =>
          React.createElement("li", { key: i }, ingredient)
        )
      );
    }
  });
```
s컴포넌트를 만드는 createClass함수는 render()메서드를 가지고 있어야 한다.
버전 15.5 이후로는 createClass를 사용하면 경고가 뜬다.

2. class components : 클래스 형태로 컴포넌트를 쓰는 방식이다.
```javascript
  class IngredientsList extends React.Component {
    render() {
      return React.createElement(
        "ul",
        { className: "ingredients" },
        this.props.items.map((ingredient, i) =>
          React.createElement("li", { key: i }, ingredient)
        )
      );
    }
  }
```
