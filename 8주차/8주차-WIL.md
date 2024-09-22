# 7주차 WIL - [에이블런] [프론트엔드부트캠프]

이번 주차에서는 React의 기초 개념 중에서 스타일링, `useEffect` Hook, 그리고 리스트 UI 렌더링에 대해 다루었다.

## 1. React 스타일링

### 인라인 스타일링

- 인라인 스타일링은 React 컴포넌트에서 직접 `style` 속성을 통해 CSS 스타일을 적용하는 방식이다.
  ```javascript
  <h1 style={{ fontSize: "24px" }}>Heading</h1>
  ```

### 다양한 스타일링 방식

React에서는 다양한 스타일링 방법을 사용할 수 있으며, Create React App(CRA) 또는 Vite가 기본적으로 설정을 지원해 준다.

1. **CSS**: 전통적인 방식으로 CSS 파일을 불러와 스타일을 적용한다.
2. **SCSS**: Sass를 사용해 더욱 강력한 스타일링을 할 수 있다.
3. **CSS Modules**: `[name].module.scss` 형태로 모듈화된 CSS를 사용하여 이름 충돌을 방지한다.
4. **CSS-in-JS**: `styled-components` 같은 라이브러리를 사용해 JavaScript 내에서 CSS를 작성한다.

   ```javascript
   import styled from "styled-components";

   const StyledBox = styled.div`
     background-color: ${(props) =>
       props.type === "danger" ? "red" : "white"};
   `;
   ```

5. **클래스명 기반 라이브러리**: `Tailwind CSS`나 `Bootstrap` 같은 유틸리티 클래스 기반의 CSS 프레임워크를 사용할 수 있다.

## 2. `useEffect` Hook

### `useEffect`란?

- `useEffect`는 함수형 컴포넌트에서 **side effects**(부수 효과)를 처리하기 위한 Hook이다. 컴포넌트가 마운트되거나 값이 변화할 때 실행되며, 데이터 페칭, 이벤트 리스너 설정, DOM 업데이트 등 다양한 작업을 처리할 수 있다.

### `useEffect` 사용 방법

1. **마운트와 업데이트 시 실행**: 의존성 배열을 제공하지 않으면, 컴포넌트가 마운트되거나 업데이트될 때마다 실행된다.

   ```javascript
   useEffect(() => {
     console.log("컴포넌트가 마운트되거나 업데이트될 때마다 실행됩니다.");
   });
   ```

2. **특정 값이 변경될 때만 실행**: 의존성 배열에 변수를 포함하면, 해당 변수가 변경될 때만 실행된다.

   ```javascript
   useEffect(() => {
     console.log("변수가 변경될 때만 실행됩니다.");
   }, [variable]);
   ```

3. **컴포넌트 마운트 시에만 실행**: 의존성 배열을 빈 배열(`[]`)로 제공하면 컴포넌트가 마운트될 때 한 번만 실행된다.

   ```javascript
   useEffect(() => {
     console.log("컴포넌트가 마운트될 때 한 번만 실행됩니다.");
   }, []);
   ```

4. **Cleanup 함수**: 컴포넌트가 언마운트되거나 업데이트되기 전에 필요한 정리 작업을 할 수 있다. 예를 들어, 타이머 제거나 구독 해제 같은 작업이 포함된다.

   ```javascript
   useEffect(() => {
     const timer = setTimeout(() => {
       console.log("타이머가 실행됩니다.");
     }, 1000);

     return () => clearTimeout(timer); // Cleanup 함수
   }, []);
   ```

## 3. 리스트 UI 구현

### 리스트 데이터 준비

- React에서 리스트를 렌더링하기 위해서는 먼저 데이터를 준비해야 한다. 보통 배열 형태의 데이터를 준비하고, `map()` 메서드를 사용해 리스트 아이템을 렌더링한다.

```javascript
const items = ["Apple", "Banana", "Cherry"];

function ItemList() {
  return (
    <ul>
      {items.map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
}
```

리스트를 렌더링할 때는 **key** 속성을 사용해 각 리스트 아이템을 고유하게 구분해 주어야 한다. 이는 React의 효율적인 업데이트를 돕는다.

## 1. 불변성 관리

### 불변성이란?

- **불변성(immutability)**은 데이터가 한 번 생성되면 수정되지 않는 성질을 말한다. React에서 상태 관리는 이 불변성을 유지해야 한다.
- React는 상태의 변경을 감지할 때 이전 상태와 새로운 상태를 비교하는 "얕은 비교" 방식을 사용하므로, 불변성을 유지하는 것이 매우 중요하다.

### 배열 상태의 불변성 관리

- **추가**: 배열에 새로운 요소를 추가할 때 스프레드 연산자를 사용해 기존 배열을 복사하고 새 요소를 추가한다.

  ```javascript
  const addItem = (item) => setItems([...items, item]);
  ```

- **제거**: 배열에서 특정 요소를 제거할 때 `filter()` 메서드를 사용해 해당 요소를 제외한 새 배열을 생성한다.

  ```javascript
  const removeItem = (targetItem) =>
    setItems(items.filter((item) => item !== targetItem));
  ```

- **수정**: 배열의 특정 요소를 수정할 때는 `map()` 함수를 사용해 해당 요소만 업데이트된 새 배열을 생성한다.
  ```javascript
  const updateItem = (targetItem, newItem) =>
    setItems(items.map((item) => (item === targetItem ? newItem : item)));
  ```

### 객체 상태의 불변성 관리

- 객체의 속성을 업데이트할 때 객체 전개 연산자(`{...}`)를 사용해 기존 객체를 복사하고, 특정 필드를 업데이트한다.
  ```javascript
  const updateUser = (newValues) => setUser({ ...user, ...newValues });
  ```

## 2. Axios를 사용한 API 통신

### Axios 설치

- Axios는 JavaScript에서 HTTP 요청을 쉽게 할 수 있게 도와주는 클라이언트 라이브러리이다. React 프로젝트에 설치하려면 다음 명령어를 사용한다.
  ```bash
  npm install axios
  ```

### Axios 사용법

1. **GET 요청**: 데이터를 가져오는 방식으로, 서버로부터 데이터를 불러올 때 사용한다.

   ```javascript
   axios
     .get("https://jsonplaceholder.typicode.com/posts")
     .then((response) => console.log(response.data))
     .catch((error) => console.error("Error fetching data", error));
   ```

2. **POST 요청**: 서버에 데이터를 전송하는 방식으로, 주로 폼 데이터를 전송하거나 새로운 데이터를 생성할 때 사용한다.
   ```javascript
   const postData = {
     title: "새 글",
     body: "이것은 새로운 글의 내용입니다.",
     userId: 1,
   };
   axios
     .post("https://jsonplaceholder.typicode.com/posts", postData)
     .then((response) => console.log(response.data))
     .catch((error) => console.error("Error posting data", error));
   ```

### GET 요청을 활용한 데이터 페칭 UI

- `useEffect`와 Axios를 결합하여 컴포넌트가 마운트될 때 데이터를 불러와 화면에 렌더링할 수 있다.
  ```javascript
  useEffect(() => {
    axios
      .get("https://jsonplaceholder.typicode.com/photos")
      .then((response) => setPhotos(response.data))
      .catch((error) => console.error("Error fetching data", error));
  }, []);
  ```

### POST 요청을 활용한 데이터 뮤테이팅 UI

- 사용자가 폼에 입력한 데이터를 서버로 전송하는 방식이다.
  ```javascript
  const handleSubmit = (event) => {
    event.preventDefault();
    const postData = { title, body };
    axios
      .post("https://jsonplaceholder.typicode.com/posts", postData)
      .then((response) => console.log(response.data))
      .catch((error) => console.error("Error posting data", error));
  };
  ```

## React 기초 - 코드 작성법과 React Router

### 1. 코드 작성법 기초

#### 이름 짓기

- **변수명은 명사로**, **함수명은 동사로** 짓는다.

  ```javascript
  const handleInputChange = () => {};
  ```

- 배열(리스트)을 담는 변수는 **복수형**으로 작성한다.

  ```javascript
  const todos = todos.map((todo) => <li>{todo.title}</li>);
  ```

- Boolean 값을 담는 변수명은 **is**로 시작한다.
  ```javascript
  const isCompleted = true;
  ```

#### Naming Convention

- **camelCase**: 변수명, 함수명
- **SCREAMING_SNAKE_CASE**: 상수명
- **PascalCase**: 클래스명, 함수형 컴포넌트명

### 2. React Router

#### React Router란?

- **React Router**는 SPA(Single Page Application)에서 페이지 라우팅을 구현하기 위한 표준 라이브러리이다.
- **라우팅**은 URL 경로에 대해 특정 컴포넌트를 렌더링하는 작업을 말하며, 클라이언트 사이드에서 페이지 간 이동을 구현할 수 있다.

#### BrowserRouter

- Web 환경에서는 React Router의 **BrowserRouter**를 사용해 라우팅 시스템을 구현한다.

#### Link 컴포넌트

- 페이지 이동을 구현할 때 `<a>` 태그 대신 **`<Link>`** 컴포넌트를 사용해야 한다.

```javascript
import { Link } from "react-router-dom";

<Link to="/about">About</Link>;
```

### 3. 정적 및 동적 라우팅

#### 정적 라우팅

- URL 경로에 따라 특정 컴포넌트를 렌더링한다.

  ```javascript
  import { Route } from "react-router-dom";

  <Route path="/about" component={About} />;
  ```

#### 동적 라우팅

- URL 경로에 변수를 포함시키면 동적 라우팅을 구현할 수 있다. **useParams** 훅을 통해 URL 파라미터에 접근할 수 있다.

  ```javascript
  import { useParams } from "react-router-dom";

  function PostDetailPage() {
    const { postId } = useParams();
    // postId에 따라 데이터를 가져와 렌더링
  }
  ```

### 4. RESTful API

- API 요청을 HTTP 메서드와 경로(path)의 조합으로 표현하는 방법이다. 각 메서드는 특정 작업을 수행한다.

  - **GET**: 데이터를 조회한다.
  - **POST**: 새로운 데이터를 생성한다.
  - **PUT**: 기존 데이터를 수정한다.
  - **PATCH**: 부분적으로 데이터를 수정한다.
  - **DELETE**: 데이터를 삭제한다.

  ```plaintext
  GET /movies → 전체 영화 정보를 가져온다.
  GET /movies/1 → ID가 1인 영화 정보를 가져온다.
  POST /movies → 새로운 영화 데이터를 생성한다.
  PUT /movies/1 → ID가 1인 영화 데이터를 수정한다.
  DELETE /movies/1 → ID가 1인 영화 데이터를 삭제한다.
  ```

## React 기초 - 스타일링(2)

### 1. CSS in JS

- **CSS in JS**는 자바스크립트 코드 안에서 CSS를 작성할 수 있는 기법이다. 이를 통해 더욱 동적인 스타일링이 가능해진다.
- 대표적으로 `styled-components` 라이브러리가 있으며, 이를 사용하면 컴포넌트 단위로 스타일을 적용할 수 있다.

  ```javascript
  import styled from "styled-components";

  const StyledButton = styled.button`
    background-color: ${(props) => (props.primary ? "blue" : "gray")};
    color: white;
    padding: 10px;
  `;
  ```

- **실습**: `ColorChanger` 예제를 통해 동적으로 색상을 변경하는 컴포넌트를 구현해 보았다.

### 2. Tailwind CSS

- **Tailwind CSS**는 유틸리티 클래스 기반의 CSS 프레임워크로, 미리 정의된 클래스들을 조합하여 스타일링을 적용할 수 있다.

  - HTML에서 바로 스타일을 적용할 수 있어, 빠르게 디자인을 구현할 수 있는 장점이 있다.

  ```html
  <button class="bg-blue-500 text-white p-2 rounded">Click me</button>
  ```

- **실습**: 계산기 UI를 Tailwind CSS를 사용하여 구현하며, Tailwind의 유용성을 체험해 보았다.
