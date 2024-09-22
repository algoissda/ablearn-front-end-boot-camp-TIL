# 10주차 WIL - [에이블런] [프론트엔드부트캠프]

이번 주차에서는 Git과 TypeScript에 대해 학습하였다.

## 1. Git

### Git이란?

- Git은 분산 버전 관리 시스템으로, 코드의 버전을 추적하고 관리할 수 있는 도구다. 코드 변경사항을 기록하여 프로젝트의 상태를 언제든지 되돌리거나 협업할 수 있다.

### 주요 개념

1. **Staging Area**: 커밋하기 전에 변경사항을 검토하고 준비하는 임시 공간.
2. **Branch**: 코드의 독립적인 버전을 관리할 수 있는 기능으로, 여러 작업을 병렬적으로 진행할 수 있다.

### 주요 Git 명령어

- `git init`: 새로운 Git 저장소를 생성.
- `git add`: 변경사항을 Staging Area에 추가.
- `git commit -m "message"`: Staging Area의 변경사항을 하나의 버전으로 커밋.
- `git branch`: 브랜치를 확인하거나 새 브랜치를 생성.
- `git switch`: 다른 브랜치로 전환.
- `git push`: 로컬에서 원격 저장소로 변경사항을 푸시.
- `git pull`: 원격 저장소의 변경사항을 로컬에 가져옴.
- `git merge`: 다른 브랜치의 변경사항을 현재 브랜치에 병합.
- `git stash`: 작업 중인 변경사항을 임시로 저장하고 나중에 다시 적용.

## 2. TypeScript

### TypeScript란?

- TypeScript는 JavaScript의 상위 집합(Superset)으로, JavaScript에 정적 타입을 추가한 언어다. 컴파일 시에 타입 오류를 확인할 수 있어, 대규모 프로젝트에서 유용하다.

### 주요 개념

1. **타입 정의**: 변수와 함수의 타입을 명시할 수 있다.

   ```typescript
   const num: number = 5;
   const name: string = "Alice";
   ```

2. **함수 타입**: 함수의 매개변수와 반환 타입을 정의할 수 있다.

   ```typescript
   function add(a: number, b: number): number {
     return a + b;
   }
   ```

3. **Interface vs Type**:

   - `interface`: 객체의 구조를 정의하는 데 사용.
   - `type`: 객체뿐만 아니라 유니언 타입, 인터섹션 타입 등도 정의할 수 있어 더 유연하다.

   ```typescript
   interface User {
     id: number;
     name: string;
   }

   type ID = number | string;
   ```

4. **Generic Type**: 다양한 타입을 받아 재사용 가능한 함수나 클래스를 작성할 수 있다.

   ```typescript
   function identity<T>(arg: T): T {
     return arg;
   }
   ```

5. **타입 단언 (Type Assertion)**: 타입스크립트가 추론하지 못하는 타입을 명시적으로 지정할 수 있다.
   ```typescript
   const someValue: any = "Hello";
   const strLength: number = (someValue as string).length;
   ```

### TypeScript 설치 및 사용법

- 전역 설치: `npm install -g typescript`
- 프로젝트 내 설치: `npm install -D typescript`

### 마무리

이번 주차에서는 Git을 사용해 프로젝트 버전을 관리하는 방법과 TypeScript를 통해 코드의 안정성을 높이는 방법을 배웠다.

## Next.js 기초

### 1. Next.js란?

Next.js는 React 기반의 프레임워크로, 서버 사이드 렌더링(SSR), 정적 사이트 생성(SSG), 그리고 클라이언트 사이드 렌더링(CSR)을 지원한다. 이를 통해 SEO 최적화와 성능 향상이 가능하며, 다양한 렌더링 방법을 혼합하여 사용할 수 있다.

### 2. 주요 특징

1. **서버 사이드 렌더링 (SSR)**: 서버에서 HTML을 렌더링하여 클라이언트로 전송해 SEO와 초기 로딩 속도 개선에 유리하다.
2. **정적 사이트 생성 (SSG)**: 빌드 타임에 HTML 파일을 미리 생성하여 매우 빠른 페이지 로딩을 제공한다.
3. **파일 기반 라우팅**: 파일의 경로와 이름을 기반으로 페이지를 자동으로 생성할 수 있다. Next.js 13부터는 App Router를 통해 라우팅을 더 유연하게 관리할 수 있다.

### 3. 프로젝트 시작하기

Next.js 프로젝트는 `create-next-app` 명령어를 사용해 빠르게 시작할 수 있다.

```bash
npx create-next-app@latest
```

프로젝트 생성 시 다양한 설정 옵션을 선택할 수 있다:

- TypeScript 사용 여부
- ESLint 사용 여부
- Tailwind CSS 사용 여부 등

### 4. 라우팅 시스템

- **파일 기반 라우팅**: `app` 디렉터리 하위에 있는 파일들이 자동으로 URL 경로가 된다.
  - `app/page.js`: 루트 경로로 매칭되는 페이지가 된다.
  - `app/posts/page.js`: `/posts` 경로로 매칭되는 페이지가 된다.
- **동적 라우팅**: 경로의 일부를 변수로 처리할 수 있다. `app/posts/[postId]` 형태로 디렉터리를 구성하여, `postId`라는 변수를 받아 동적 페이지를 구현할 수 있다.
  ```javascript
  function PostDetailPage({ params }) {
    const { postId } = params;
    return <div>Post {postId}</div>;
  }
  ```

### 5. 클라이언트 사이드 렌더링 (CSR)

Next.js는 서버 사이드 렌더링이 기본이지만, 클라이언트 측에서 데이터를 패칭하는 CSR 방식도 지원한다. 클라이언트에서 `useEffect`와 `useState`를 사용해 데이터를 가져올 수 있다.

```javascript
"use client";
import { useEffect, useState } from "react";

function PostsListPage() {
  const [posts, setPosts] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/posts")
      .then((res) => res.json())
      .then((data) => setPosts(data));
  }, []);

  return (
    <div>
      <h1>Posts List</h1>
      {posts.map((post) => (
        <div key={post.id}>{post.title}</div>
      ))}
    </div>
  );
}

export default PostsListPage;
```

### 6. 서버 사이드 렌더링 (SSR) & 정적 사이트 생성 (SSG)

서버 사이드 렌더링과 정적 사이트 생성은 Next.js에서 데이터를 서버에서 미리 렌더링하거나 빌드 타임에 HTML 파일을 생성해 제공하는 방법이다.
