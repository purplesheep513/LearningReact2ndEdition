
# let 키워드

let 키워드에는 변수를 할당할 수 있다. var와 다른 점은 scope이다. var는 {}에 상관없이 변수를 지정하고 바꿀 수 있다.
그러나 let으로 선언할 경우 {}바깥으로 영향을 미칠 수 없다.

var로 선언할 경우
```javascript
var topic = "JavaScript";

if (topic) {
  var topic = "React";
  console.log("block", topic); // 예상되는 출력값: block React
}

console.log("global", topic); // 예상되는 출력값: global React
```


let으로 선언할경우
```javascript
var topic = "JavaScript";

if (topic) {
  let topic = "React"; // topic은 새로운 변수 취급
  console.log("block", topic); // 예상되는 출력값: block React
}

console.log("global", topic); // 예상되는 출력값: global JavaScript
```

※ var을쓰면 for문의 {}에서도 scope 차단이 적용되지 않는다.

var로 선언할 경우
```javascript
var div,

for (var i = 0; i < 5; i++) {
  div = document.createElement("div");
  container = document.getElementById("container");
  div.onclick = function() {
    alert("This is box #" + i);
  };
  container.appendChild(div);
}
```

for문을 돌며 생성된 `<div></div>`에는 모두 onclick함수가 할당되어 있다. 이것을 클릭하면 전부 This is box #5 라는 메세지를 받게된다.
왜냐하면 
1. for문의 i가 var로 선언되어있다.
2. for문은 i가 5가 되는 순간 멈춘다.(마지막으로 i에게 할당되는 값이 5)
3. var로 선언된 i는 global변수 취급받으므로 마지막으로 i에게 할당되는 숫자인 5가 i의 최종 값이 된다.

=> 그러므로 onclick에서 출력되는 i가 무조건 5가 됨


그러나 let으로 선언된 변수의 경우를 살펴보자.

let으로 선언할경우
```javascript
const container = document.getElementById("container");
let div;
for (let i = 0; i < 5; i++) {
  div = document.createElement("div");
  div.onclick = function() {
    alert("This is box #: " + i);
  };
  container.appendChild(div);
}
```

for문을 돌며 생성된 `<div></div>`에는 모두 onclick함수가 할당되어 있다.
이것을 클릭하면 순서대로 This is box #0, This is box #1, ..., This is box #4 라는 메세지를 받게된다.
i의 scope가 let에 의해 보호되기 때문이다.