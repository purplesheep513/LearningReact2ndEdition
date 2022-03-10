# 화살표 함수

ES6이후로 들어오게 된 함수.

이전에는 함수정의를
```javascript
const example = function(firstName, lastName){
  return `Hello ${firstName} ${lastName}`
}
```
같은 형식으로 하였다면 화살표함수는
```javascript
const example = (firstName, lastName) => `Hello ${firstName} ${lastName}`
```
와 같은 형식으로 정의하는 것이다. (파라미터가 하나라면 파라미터 부분의 괄호는 생략할 수도 있다.)

화살표 이후의 로직을 {}로 감싸주어도 된다.
```javascript
const example = (firstName, lastName) => {
`Hello ${firstName} ${lastName}`
}
```


> 그렇다면 예전버전으로 정의하던 함수와 무엇이 다를까?
- this의 scope가 다르다. 화살표 함수 안의 this는 항상 상위 스코프의 this를 가리킨다.
   일반 함수 안의 this 함수로 선언된 경우, 메서드로 선언된 경우가 다른데 
    함수로 선언된 경우는 '전역객체'를 가리키고 메서드로 선언된 경우 '해당 메소드를 소유하고 있는 객체'를 가리킨다.
   하지만 ※ 일반 함수 안의 함수(내부함수, 콜백함수) 의 this는 전역객체 window를 가리킨다.


```javascript
const tahoe = {
  mountains: ["Freel", "Rose", "Tallac", "Rubicon", "Silver"],
  print: function(delay = 1000) {
    setTimeout(function() {
      console.log(this.mountains.join(", "));
    }, delay);
  }
};

tahoe.print();
```
위와 같은 로직을 실행하면 `Uncaught TypeError: Cannot read property 'join' of undefined` 라는 에러가 뜨게 된다.<br/>
이 에러는 print함수 안의 this.mountains에게 join이라는 메서드를 사용하려고 하여 나는 에러다.(join : 배열을 문자열로 만들어주는 메서드)<br/>
이 함수에서 this는 전역 객체인 window{}를 가리킨다. 함수 안의 함수(내부함수, 콜백함수) 내부의 this는 전역객체를 가리키기 때문이다.<br/>
window scope에는 mountains라는 변수가 없으므로 에러가 난다.


이를 해결하기 위해
```javascript
const tahoe = {
  mountains: ["Freel", "Rose", "Tallac", "Rubicon", "Silver"],
  print: function(delay = 1000) {
    setTimeout(() => {
      console.log(this.mountains.join(", "));
    }, delay);
  }
};

tahoe.print(); 
```
와 같이 써준다. 이렇게 작성했을 때 예상되는 출력값은 Freel, Rose, Tallac, Rubicon, Silver 가 된다.<br/>
setTimeout 안의 함수를 화살표 함수로 작성하게되면 setTimeout 안의 this는 상위 scope의 this를 가리킨다.<br/>

하지만 setTimeout바깥의 함수까지 화살표 함수를 사용하면 어떤 일이 일어날까?

```javascript
const tahoe = {
  mountains: ["Freel", "Rose", "Tallac", "Rubicon", "Silver"],
  print: (delay = 1000) => {
    setTimeout(() => {
      console.log(this.mountains.join(", "));
    }, delay);
  }
};

tahoe.print();
```
위와 같은 로직을 실행하면 `Uncaught TypeError: Cannot read property 'join' of undefined` 라는 에러가 뜨게된다.</br>
arrow함수의 상위 scope가 전역객체가 되므로 this가 가리키는 것이 window가 된다는 뜻..
