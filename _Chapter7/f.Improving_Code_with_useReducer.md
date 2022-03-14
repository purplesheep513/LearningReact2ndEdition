# Improving Code with useReducer

## useRecucer
useReducer로 state값을 업데이트해볼 것이다.

예시코드
```javascript
const firstUser = {
  id: "0391-3233-3201",
  firstName: "Bill",
  lastName: "Wilson",
  city: "Missoula",
  state: "Montana",
  email: "bwilson@mtnwilsons.com",
  admin: false
};

function User() {
  const [user, setUser] = useState(firstUser);

  return (
    <div>
      <h1>
        {user.firstName} {user.lastName} - {user.admin ? "Admin" : "User"}
      </h1>
      <p>Email: {user.email}</p>
      <p>
        Location: {user.city}, {user.state}
      </p>
      <button
        onClick={() => {
          setUser({ ...user, admin: true });
        }}
      >
        Make Admin
      </button>
    </div>
  );
}
```
여기서 button쪽을 잘 보면 `setUser({ ...user, admin: true });`으로 되어있는 것을 확인할 수 있다. `setUser({ admin: true });`라고 하면 에러가 나기 때문이다. 항상 spread 연산자를 이용해 기존 object를 concat 해주고 원하는 key,value를 붙여주어야 한다.

>useReducer를 이용해 위의 코드를 다시 짜본다면
```javascript
function User() {
  const [user, setUser] = useReducer(
    (user, newDetails) => ({ ...user, ...newDetails }),
    firstUser
  );
  ...
}
```
useReducer의 첫 번째 인자는 함수형식이고 두 번째 인자는 초기값이다.
여기서 setUser은 기존 user값 안에 newDetails을 추가해주는 함수가 된다.(useReducer의 첫번째 인자라고 봐도 됨)
그렇다면 버튼에는
```javascript
<button
  onClick={() => {
    setUser({ admin: true });
  }}
>
  Make Admin
</button>
```
라고 넣어주면 된다. setUser은 파라미터를 받아서 기존의 정보에 { admin: true }을 붙여주게 된다.

>**요약**: useReducer을 이용하면 setState함수에 다양한 기능을 추가할 수 있음