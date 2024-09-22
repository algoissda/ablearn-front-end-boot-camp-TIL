## 9주차 WIL - [에이블런] [프론트엔드부트캠프]

이번 주차에서는 React에서 전역 상태 관리에 대해 학습하였다. 전역 상태 관리는 애플리케이션 전반에서 데이터를 공유하고 관리하는 중요한 개념으로, 특히 상태를 효과적으로 관리하는 방법을 배우는 데 중점을 두었다.

### 1. 전역 상태 관리란?

- **전역 상태 관리**는 앱 전체에 걸쳐 상태를 공유하고 관리하는 것을 의미한다.
- React는 기본적으로 부모에서 자식으로 데이터가 흐르는 **단방향 데이터 흐름**을 따른다. 하지만 상태가 여러 컴포넌트에 걸쳐 사용될 때는 전역 상태 관리가 필요하다.

### 2. 전역 상태 관리 방법

#### Props Drilling

- **Props Drilling**은 부모 컴포넌트에서 자식 컴포넌트로, 그리고 그 아래의 자식에게 계속해서 props를 전달하는 방식이다. 하지만 깊은 컴포넌트 구조에서 props를 전달하는 것은 유지보수와 코드 관리가 어려워질 수 있다.

#### Context API

- **Context API**는 리액트에서 제공하는 전역 상태 관리 도구로, 라이브러리 없이도 상태를 공유할 수 있도록 도와준다. 주로 Props Drilling의 단점을 보완하기 위해 사용된다.

#### Redux와 기타 라이브러리

- **Redux**: 전역 상태 관리를 위해 가장 널리 사용되는 라이브러리이다. 하지만 복잡성과 많은 코드로 인해 Recoil, Zustand, Tanstack Query와 같은 더 간단한 상태 관리 라이브러리들이 등장했다.

### 3. 실습 - Netflex에 프로필과 좋아요 기능 구현

- 이번 실습에서는 `Netflex`에 사용자 프로필 수정과 좋아요 기능을 추가했다.
  1. **프로필 수정**: 마이페이지에서 닉네임을 수정할 수 있으며, 수정된 닉네임은 Header에 반영된다.
  2. **영화 좋아요 기능**: 로그인한 사용자는 영화 목록과 상세 페이지에서 '좋아요' 버튼을 누를 수 있고, 마이페이지에서 좋아요한 영화 목록을 확인할 수 있다.

## Context API

### Context API의 세 가지 기본 단계

1. **Context 생성**: `createContext()`를 사용해 Context를 생성한다.

   ```javascript
   const SomeContext = createContext();
   ```

2. **Context 사용**: `useContext()`를 통해 Context를 사용할 수 있다.

   ```javascript
   const value = useContext(SomeContext);
   ```

3. **Provider로 값을 전달**: `Provider` 컴포넌트를 사용해 특정 범위에 값을 전달한다. 이 범위 내의 모든 컴포넌트에서 Context 값을 사용할 수 있다.

   ```javascript
   function SomeProvider({ children }) {
     const value = {
       /* some value */
     };

     return (
       <SomeContext.Provider value={value}>{children}</SomeContext.Provider>
     );
   }
   ```

- Context API는 React에서 전역 상태를 관리하는 간단한 방법으로, Props Drilling을 대체할 수 있다.

## Redux 및 Redux Toolkit

### Redux의 특징

- **단방향 데이터 흐름**: React에서처럼 상태가 한 방향으로만 흐른다.
- **데이터 변경이 까다로움**: 상태 관리를 예측 가능하고 유지 보수하기 쉽게 설계되어, 상태 변경이 엄격하게 관리된다.

### Redux의 핵심 개념

1. **Store**: 앱 전체에서 전역적으로 접근할 수 있는 상태가 저장되는 공간이다. 일반적으로 앱에서는 하나의 store만 사용한다.
2. **Reducer**: store 내의 상태를 업데이트하는 함수이다. action 객체를 받아 상태를 변경한다.
3. **Action Creator**: action 객체를 생성하는 함수로, 상태 변경 요청을 단순화하고 휴먼 에러를 줄이는 데 도움을 준다.

### Redux 코드 작성 단계

1. **설치**: `@reduxjs/toolkit`과 `react-redux`를 설치한다.

   ```bash
   npm install @reduxjs/toolkit react-redux
   ```

2. **Reducer 만들기**: 상태 변경 로직을 관리하는 함수를 작성한다.

   ```javascript
   const initialState = { value: 0 };

   function counterReducer(state = initialState, action) {
     switch (action.type) {
       case "counter/incremented":
         return { ...state, value: state.value + 1 };
       case "counter/decremented":
         return { ...state, value: state.value - 1 };
       default:
         return state;
     }
   }
   ```

3. **Store 생성**: reducer를 사용해 store를 만든다.

   ```javascript
   const store = createStore(counterReducer);
   ```

4. **App에 Store 주입**: `Provider`를 사용해 React 앱에 store를 주입한다.

   ```javascript
   <Provider store={store}>
     <App />
   </Provider>
   ```

5. **컴포넌트에서 Redux 사용**: `useSelector`와 `useDispatch` 훅을 사용해 상태를 조회하고 업데이트할 수 있다.

6. **Redux Devtools**: 상태 변화를 쉽게 추적할 수 있도록 Chrome 확장 프로그램을 설치해 사용한다.

## Zustand 전역 상태 관리

### 1. Getting Started

Zustand는 React에서 전역 상태를 관리하는 간단한 라이브러리이다. 사용법이 직관적이며 Redux보다 설정이 간단하다.

#### 설치

```bash
npm i zustand
```

#### 기본 사용법

1. **Store 생성**: `create` 함수를 사용해 상태를 정의한다.

   ```javascript
   import create from "zustand";

   const useStore = create((set) => ({
     bears: 0,
     increasePopulation: () => set((state) => ({ bears: state.bears + 1 })),
     removeAllBears: () => set({ bears: 0 }),
   }));
   ```

2. **컴포넌트에서 상태 사용**: 상태를 조회하고 변경할 수 있다.

   ```javascript
   function BearCounter() {
     const bears = useStore((state) => state.bears);
     return <h1>{bears} around here ...</h1>;
   }

   function Controls() {
     const increasePopulation = useStore((state) => state.increasePopulation);
     return <button onClick={increasePopulation}>one up</button>;
   }
   ```

### 2. 추가 기능

1. **여러 데이터를 한 번에 가져오기**: 여러 데이터를 가져올 때 불필요한 리렌더링을 방지하려면 `useStore`를 각각 사용하거나, `useShallow`를 사용하여 객체 또는 배열 형태로 데이터를 가져올 수 있다.
2. **비동기 작업 지원**: Redux의 reducer와는 달리, Zustand는 기본적으로 비동기 작업을 지원한다.

3. **Immer.js와 연동**: Zustand는 Immer.js를 미들웨어로 연동해 불변성을 유지하면서 상태를 업데이트할 수 있다.

4. **LocalStorage 연동**: `persist` 미들웨어를 사용해 상태를 `localStorage`에 저장할 수 있다.

## Tanstack Query 및 json-server

### 1. Tanstack Query

Tanstack Query는 비동기 데이터 관리를 위한 도구로, 기존의 Redux 등에서 비동기 통신을 다루는 어려움을 해결하기 위해 등장했다.

#### 설치

```bash
npm i @tanstack/react-query
```

#### 사용법

1. **QueryClient 설정**: 애플리케이션에서 사용할 QueryClient를 설정한다.

   ```javascript
   import {
     QueryClient,
     QueryClientProvider,
     useQuery,
   } from "@tanstack/react-query";

   const queryClient = new QueryClient();

   function App() {
     return (
       <QueryClientProvider client={queryClient}>
         <Example />
       </QueryClientProvider>
     );
   }
   ```

2. **useQuery 훅 사용**: 서버에서 데이터를 가져올 때 `useQuery` 훅을 사용한다.

   ```javascript
   function Example() {
     const { isPending, error, data } = useQuery({
       queryKey: "repoData",
       queryFn: () =>
         fetch("https://api.github.com/repos/TanStack/query").then((res) =>
           res.json()
         ),
     });

     if (isPending) return "Loading...";
     if (error) return `An error has occurred: ${error.message}`;

     return (
       <div>
         <h1>{data.name}</h1>
         <p>{data.description}</p>
       </div>
     );
   }
   ```

#### useQuery와 useMutation

- **useQuery**: 데이터를 조회하는 데 사용된다. (Read)
- **useMutation**: 데이터를 생성, 수정, 삭제할 때 사용된다. (Create, Update, Delete)

#### Devtools

- `@tanstack/react-query-devtools`를 설치하여 Devtools를 통해 상태 변화를 모니터링할 수 있다.

### 2. json-server

- **json-server**는 빠르게 REST API를 만들 수 있는 도구로, 테스트와 개발 과정에서 유용하다.

  ```bash
  npm install -g json-server
  ```

- JSON 파일을 기반으로 서버를 실행하여, 데이터를 조회하거나 조작할 수 있는 완전한 REST API를 제공한다.

## React Hooks 요약

### 1. `useState`

- 상태 관리를 위해 사용되는 기본적인 훅으로, 상태값과 상태를 업데이트하는 함수를 반환한다.
  ```javascript
  const [count, setCount] = useState(0);
  ```

### 2. `useEffect`

- 컴포넌트가 렌더링된 이후 비동기적으로 특정 작업을 수행할 때 사용된다.
  ```javascript
  useEffect(() => {
    // Fetch data or set up a subscription
  }, [dependencies]);
  ```

### 3. `useLayoutEffect`

- `useEffect`와 유사하지만, DOM이 업데이트되기 전에 동기적으로 실행된다. 레이아웃을 조작해야 할 때 유용하다.

### 4. `useMemo`

- 값의 참조값을 메모이제이션하여, 렌더링 시 계산 비용이 큰 값을 재계산하지 않도록 한다.
  ```javascript
  const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
  ```

### 5. `useCallback`

- 함수를 메모이제이션하여, 리렌더링 시 동일한 함수 참조값을 유지하도록 한다. 주로 자식 컴포넌트에 props로 함수를 전달할 때 사용된다.
  ```javascript
  const memoizedCallback = useCallback(() => doSomething(a, b), [a, b]);
  ```

### 6. `useRef`

- 리렌더링에 영향을 받지 않는 참조값을 유지할 때 사용된다. 주로 DOM 요소에 접근하거나 상태를 저장할 때 사용된다.
  ```javascript
  const inputRef = useRef(null);
  ```

React의 다양한 훅을 통해 상태 관리와 성능 최적화를 더욱 효과적으로 할 수 있다.
