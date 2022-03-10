ReactDOM

ReacDOM은 React Element를 브라우저에 랜더링하기 위해 필요한 도구들을 포함하고있다.
React Elements와 그의 자식을 ReacDOM.render 메서드로 랜더링 할 수 있다.
파라미터는 두 가지를 받는데, 첫 번째는 만들고싶은 요소이고 두 번째는 타겟 노드다.
따라서 
/************** Example1 **************/
  const dish = React.createElement("h1", {id="menu"}}, "Baked Salmon");

  ReactDOM.render(dish, document.getElementById("root"));
/************** Example1 **************/
와 같이 사용할 수 있다.

위의 코드를 실행시키면 아래와 같은 결과가 나온다.

/************** Result **************/
<body>
  <div id="root">
    <h1 id="menu">Baked Salmon</h1>
  </div>
</body>
/************** Result **************/



ReacDOM.render의 첫 번째 파라미터에는 다음과 같이 배열이 들어갈 수도 있다.

/************** Example2 **************/
const dish = React.createElement("h1", null, "Baked Salmon");
const dessert = React.createElement("h2", null, "Coconut Cream Pie");

ReactDOM.render([dish, dessert], document.getElementById("root"));
/************** Example2 **************/