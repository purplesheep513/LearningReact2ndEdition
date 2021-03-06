> ES2016 이후로 객체와 배열을 사용할때 다양한 방법의 문법을 이용할 수 있게되었다.</br>
객체와 배열의 경우를 따로 살펴보겠다.
1. Destructuring Objects
2. Destructuring Arrays


◎객체의 경우 

```javascript
const sandwich = {
  bread: "dutch crunch",
  meat: "tuna",
  cheese: "swiss",
  toppings: ["lettuce", "tomato", "mustard"]
};

const { bread, meat } = sandwich; // 이런식으로 정의해줄 수도 있다.

console.log(bread, meat); // 예상되는 출력 값 : dutch crunch tuna
```


이것을 그대로 함수의 파라미터에 정의할 수도 있다.
```javascript
const lordify = ({ firstname }) => {
  console.log(`${firstname} of Canterbury`);
};

const regularPerson = {
  firstname: "Bill",
  lastname: "Wilson"
};

lordify(regularPerson); // 예상되는 출력값 : Bill of Canterbury
```
lordify에 바로 regularPerson객체를 넣어주어도 애초에 lordify에서 받을 파라미터를 firstname로 정의하였으므로 firstname을 읽어온다.

</br>

◎배열의 경우

```javascript
const [firstAnimal] = ["Horse", "Mouse", "Cat"];

console.log(firstAnimal); // 예상되는 출력 값 : Horse
```
firstAnimal을 출력하면 첫번째 것만출력된다. 이유: 배열을 가리킬 때 가장 첫번째 값을 가리키고 있음
첫 번째 값 이후의 값을 가져오길 원한다면 아래와 같이 써줄 수 있다.

```javascript
const [, , thirdAnimal] = ["Horse", "Mouse", "Cat"];

console.log(thirdAnimal); // 예상되는 출력 값 : Cat
```

</br>

◎ Object Literal Enhancement
위와 반대경우를 말한다. 변수 또는 상수를 따로 선언해 묶으면 객체가 된다.

```javascript
const name = "Tallac";
const elevation = 9738;

const funHike = { name, elevation }; // 합쳐준다.

console.log(funHike); // 예상되는 출력 값 : {name: "Tallac", elevation: 9738}
```
