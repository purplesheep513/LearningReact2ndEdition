# Rules to Follow with Hooks
버그가 나지 않도록 유의해야할 점
* Hook은 component의 scope내에서만 가동되어야 한다.
  * Hook은 React 컴포넌트에 의해 호출되어야 한다. Hook은 커스텀된 또 다른 Hook(그리고 결국 다른 컴포넌트에 붙을)에 더해질 수 있다.
* 기능별로 Hook을 나눠서 사용하자
  * 다른 기능을 하는 함수들을 굳이 같은 hook안에 몰아넣을 필요는 없다. 그래야 읽기도 쉽고 dependency array안의 value들을 관리하기에도 편하다
* Hook은 가장 상위 level에서 호출되어야한다.
  * Hook은 조건문이나 반복문 또는 async/await 안에서 불러질 수 없다. (hook안에 조건문을 사용할 것)

  불가
  ```javascript
  if (count > 5) {
    const [checked, toggle] = useState(false);
  }
  ```
  가능
  ```javascript
  useState(
    count => (count < 5) ? undefined : !c,
    (count < 5) ? undefined
  );
  useEffect(() => {
    const fn = async () => {
      await SomePromise();
      };
      fn();
  });
  ```
