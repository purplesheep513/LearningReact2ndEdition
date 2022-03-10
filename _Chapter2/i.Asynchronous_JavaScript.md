동기/비동기에 대한 내용
동기를 사용하면 어떤 작업이 끝날 때 까지 다른 작업을 진행할 수 없지만
비동기를 이용한다면 다른 작업이 끝날 때 까지 기다릴 필요가 없다.
이를 위해 JavaScript는 다음 몇 가지 함수를 제공한다.
1. Simple Promises with Fetch
2. Async/Await
3. Building Promises

◎ Simple Promises with Fetch
  과거 request를 REST API로 만드는 작업은 복잡했다. 그러나 fetch()함수가 등장하면서 단순해졌다.
  그렇다면 fetch()란 무엇인가

  /************** fetch() Example1 **************/
    console.log(fetch("https://api.randomuser.me/?nat=US&results=1"));
  /************** fetch() Example1 **************/
  => 위의 예시 fetch안의 url은 랜덤한 사람들의 이름과 이메일 정보를 담고있는 API다. (당연히 가상의 인물들임)
  fetch는 url을 마치 파라미터처럼 가져가게 된다.

  위 console을 실행하면 Promise{<pending>} 이라는 객체가 출력된다.
  ★ Promise의 의미
    : instruction이 비동기로 진행될 때 JavaScript의 상태를 나타낸다.
      pending, completed, failed 세가지의 상태가 있으며 데이터를 가져오면서 동시에 어떤 상태인지를 알려주는 역할을 한다.
  
  그리하여 다시 fetch("https://api.randomuser.me/?nat=US&results=1")의 결과로 돌아가본다면, Promise{<pending>}은 데이터를 불러오기 전 상태를 말한다.
  데이터를 가져오기 위해 .then()함수를 붙이는 작업이 필요하다.

  그리하여

  /************** fetch() Example2 **************/
    fetch("https://api.randomuser.me/?nat=US&results=1").then(res =>
      console.log(res.json())
    );
  /************** fetch() Example2 **************/
  라고 .then()함수를 붙여보았다. then함수는 Promise가 해결됐을 경우 실행되는 함수다. 
  아래와 같이 여러개를 붙일 수도 있다. 그럴 경우 연쇄적으로 then 안의 내용이 실행된다.


  /************** fetch() Example3 **************/
    fetch("https://api.randomuser.me/?nat=US&results=1")
    .then(res => res.json())
    .then(json => json.results)
    .then(console.log)
    .catch(console.error);
  /************** fetch() Example3 **************/
  먼저 fetch함수가 url안의 데이터를 가져오라는 요청을 보내게 된다. 요청이 성공적으로 이루어지면 response body가 JSON이 된다.
  그 다음, JSON데이터를 결과값으로 return한다.
  그리고 그 결과값을 console.log 함수로 보내게 된다.
  마지막으로, catch함수가 fetch함수가 제대로 실행되지 않았을 경우를 감지해 error를 출력한다.



◎ Async/Await
  Promise를 다루기 위해 자주 사용되는 함수 중에 Async/Await 함수가 있다.
  이 함수에서는 Promise상태가 도출되면 then함수를 사용하는 대신 await라는 함수를 사용한다.

  /************** Async/Await Example1 **************/
    const getFakePerson = async () => {
      let res = await fetch("https://api.randomuser.me/?nat=US&results=1");
      let { results } = res.json();
      console.log(results);
    };
    
    getFakePerson();
  /************** Async/Await Example1 **************/
  async 함수를 이용해 getFakePerson를 한 뒤 fetch를 실행하고 promise로 요청 상태가 도출되면 res에 값을 세팅해준다.
  error로그가 필요하다면 아래와 같이 try catch구문을 사용한다.


  /************** Async/Await Example2 **************/
    const getFakePerson = async () => {
      try {
        let res = await fetch("https://api.randomuser.me/?nat=US&results=1");
        let { results } = res.json();
        console.log(results);
      } catch (error) {
        console.error(error);
      }
    };

    getFakePerson();
  /************** Async/Await Example2 **************/