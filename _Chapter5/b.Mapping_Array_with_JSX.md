# Mapping Arrays with JSX

JSX는 자바스크립트이므로 JSX element 안에 바로 자바스크립트 함수를 작성할 수 있다.

```javascript
<ul>
  {props.ingredients.map((ingredient, i) => (
    <li key="{i}">{ingredient}</li>
  ))}
</ul>
```
JSX는 HTML과 비슷하게 생겼으나 브라우저에서 해석될 수 없으므로 createElement메서드가 JSX를 변환해주어야 하는 문제가 있는데 다행히 이 일을 대신해주는 툴이 있다.
</br>
</br>

# Babel

많은 소프트웨어 언어들이 컴파일된 코드를 필요로 하지만 자바스크립트는 인터프리터 언어이므로(브라우저가 코드를 text로 해석할 수 있음) 컴파일이 필요없다.
</br>
</br>
그러나 모든 브라우저가 자바스크립트의 최신 문법을 지원하는 것도 아니고 특히 JSX는 지원되는 브라우저가 없기 때문에 개발자가 직접 자신의 코드를 브라우저가 해석할 수 있는 코드로 수정을 해주어야 한다.
</br>
</br>
이 과정을 컴파일이라고 부르고 Babel는 이 과정을 수행할 수 있도록 디자인 되었다.
</br>

> Babel의 역할
- Babel은 ES6문법을 ES5로 변환해주는 역할을 한다.
- JSX를 자바스크립트로 변환시켜준다.
