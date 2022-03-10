# React Components

UI는 버튼, 목록, 제목 등의 각각의 파트로 나뉘어져 있다. 이러한 파트가 모여 UI를 구성하게 된다.
리액트에서는 이러한 각각의 파트를 컴포넌트라 부른다. 컴포넌트를 생성할 때 함수를 사용하므로 컴포넌트는 재사용이 가능하다.

그러므로 리액트로 UI를 구성할 때에는 각각의 컴포넌트들이 재사용 가능한지를 고려해야 한다.


아래의 예시를 보면
```javascript
  const secretIngredients = [
    "1 cup unsalted butter",
    "1 cup crunchy peanut butter",
    "1 cup brown sugar",
    "1 cup white sugar",
    "2 eggs",
    "2.5 cups all purpose flour",
    "1 teaspoon baking powder",
    "0.5 teaspoon salt"
  ];

  function IngredientsList() {
    return React.createElement(
      "ul",
      { className: "ingredients" },
      items.map((ingredient, i) =>
        React.createElement("li", { key: i }, ingredient)
      )
    );
  }

  // 위와 같이 IngredientsList를 함수로 정의해 놓으면 이것을 가져와 언제든지 render해서 사용할 수 있다.
  ReactDOM.render(
    React.createElement(IngredientsList, { items: secretIngredients }, null),
    document.getElementById("root")
  );
```
