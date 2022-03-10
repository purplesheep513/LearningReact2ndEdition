# React Elements as JSX
이전 챕터까지는 리액트 element를 만들기 위해 React.createElement를 이용했으나 이제부터는 JSX로 좀더 쉽게 코드를 작성할 것이다.
JSX에서는 태그를 사용해 element의 타입을 지정한다. (HTML과 흡사한 형식)
```javascript
<ul>
  <li>1 lb Salmon</li>
  <li>1 cup Pine Nuts</li>
  <li>2 cups Butter Lettuce</li>
  <li>1 Yellow Squash</li>
  <li>1/2 cup Olive Oil</li>
  <li>3 Cloves of Garlic</li>
</ul>
```

## JSX Tips
JSX는 HTML과 비슷하게 생겼지만 몇 가지 고려해야할 점이 있다.
### **Nested components**
JSX 태그 안에 자식 태그를 추가할 수 있음. 
```javascript
<IngredientsList>
  <Ingredient />
  <Ingredient />
  <Ingredient />
</IngredientsList>
```
### **className**
HTML태그와 달리 JSX에서는 class 어트리뷰트를 className라고 명명함.

```javascript
<h1 className="fancy">Baked Salmon</h1>
```
### **JavaScript expressions**
{} 를 이용해 변수값을 넣을 수 있다.
```javascript
<h1>{title}</h1>
// 또는
<input type="checkbox" defaultChecked={false} />
```
### **Evaluation**
{}안에 자바스크립트 코드처럼 작성할 수 있다.
```javascript
<h1>{"Hello" + title}</h1>

<h1>{title.toLowerCase().replace}</h1>
```