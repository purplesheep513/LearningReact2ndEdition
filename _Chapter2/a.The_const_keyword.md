# The const Keyword

ES2015이전에는 var로 모든 변수를 정의했으나 이후 const와 let이 등장함

## const 키워드

상수는 overwritten될 수 없는 값을 뜻한다. (=한 번 정의하면 바꿀 수 없음)
그러므로 overwritten되면 안 되는 값을 const로 정의하도록 한다.

```javascript
var pizza = true;
pizza = false;
console.log(pizza); // 예상되는 출력값: false
```

그러나 아래와 같은 코드를 작성하면
```javascript
const pizza = true;
pizza = false;
```


>개발자도구 콘솔에 Uncaught TypeError : Assignment to constant variable. 라는 에러가 뜨게된다.(상수에 새로운 값을 할당해 에러가남)

