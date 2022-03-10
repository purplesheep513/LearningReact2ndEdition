# 스프레드 오퍼레이터
...<- 이것을 자주 보았을 것이다. 이것을 스프레드 오퍼레이터라 한다.

> 스프레드오퍼레이터의 역할
1. 복수 배열의 내용을 하나로 묶어준다.
2. 나머지 값을 가져올 때 사용한다.

```javascript
const peaks = ["Tallac", "Ralston", "Rose"];
const canyons = ["Ward", "Blackwood"];
const tahoe = [...peaks, ...canyons]; // peaks와 canyons두 배열을 하나로 묶는다.

console.log(tahoe.join(", ")); // 예상되는 출력 값 : Tallac, Ralston, Rose, Ward, Blackwood
```
위의 코드는 두 배열을 하나로 묶는 스프레드 오퍼레이터의 예시다.

```javascript
const lakes = ["Donner", "Marlette", "Fallen Leaf", "Cascade"];

const [first, ...others] = lakes; // others에 첫 번째 값을 제외한 나머지 값들이 들어가게 된다.

console.log(others.join(", ")); // 예상되는 출력 값Marlette, Fallen Leaf, Cascade
```
위의 코드는 배열의 나머지 값을 저장하는 스프레드 오퍼레이터의 예시다.


※ 스프레드 오퍼레이터는 배열 뿐만 아니라 객체에서도 사용할 수 있다.
