# Template String

템플릿 스트링이란 ``<- 이것을 말한다.

우리가 이전에 String을 표현하는 약속으로 '나 "를 사용했을 때 변수를 중간에 넣고싶은 경우 var1 + "," + var2 이런식으로 해주어야 했다.
그러나 `를 이용하면 중간에 + 연산자를 이용하는 번거로움을 줄일 수 있다.

그러므로
var1 + "," + var2 는 \`\${var1}, ${var2}\`와 같다.

※ 템플릿 스트링안의 변수는 ${}안에 넣어주기로 약속되어있다.


```javascript
document.body.innerHTML = `
<section>
  <header>
      <h1>The React Blog</h1>
  </header>
  <article>
      <h2>${article.title}</h2>
      ${article.body}
  </article>
  <footer>
      <p>copyright ${new Date().getYear()} | The React Blog</p>
  </footer>
</section>
`
```
해주면 원하는 태그와 문자와 변수를 바로 넣을 수 있다.