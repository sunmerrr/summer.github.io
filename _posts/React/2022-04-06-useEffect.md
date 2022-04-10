---
title: "useEffect"
excerpt: "react function 컴포넌트에서 side effect를 다루는 법"

categories:
  - React
tags:
  - [react, javascript, library, hook, useEffect, side effect]

toc: true
toc_sticky: true
 
date: 2022-04-06
last_modified_at: 2022-04-10
---

- 리엑트 hook을 모른다면? [What is a Hook 👉🏻](https://ko.reactjs.org/docs/hooks-overview.html#but-what-is-a-hook)

## Effect Hook
- `useEffect`는 react의 함수형 컴포넌트에서 side effect를 다룰 수 있게 해주는 hook 이다.
  *- side effect : 렌더링 시에 실행되지 않고 그 이후에 비동기로 실행되는 부수적인 일들* 
  즉, UI로 보여주는 요소를 제외하고 그 안을 채워주는 데이터를 불러오는 것, 데이터를 변경하는 것, DOM을 수정하는 것 등을 useEffect 안에서 처리해줄 수 있다는 말이다.
- react class 컴포넌트와 비교하여 useEffect는 `componetDidMount`, `componentDidUpdate`, `componentWillUnmount`를 대신 하는 역할을 한다.

### 특징
- 첫 rendering 이 완료 된 후에는 항상 실행된다.
- 의존성 배열안의 값이 변경 시 실행된다.
- 기존의 class 컴포넌트와는 달리 비슷한 성격을 가진 로직끼리 묶어줄 수 있다.

### 사용
- 함수형 컴포넌트를 return하기 전에 사용한다.

  - 형태
    ```jsx
    import React, {useEffect} from 'react';

    function Example() {
      useEffect(() => {
        ...실행할 로직...
      })

      return (
        <div>
          예시
        </div>
      )
    }
    ```

  - 의존성 배열
    - 의존성 배열이란 useEffect가 옵션으로 가지고있는 배열로, 로직을 포함하는 중괄호({ })뒤에 쉼표(,)를 써준 후 배열을 넣는다.
    - 의존성 배열안에 값을 넣어둘 경우 그 값이 변경될때마다 해당 useEffect가 실행된다.
    - 의존성 배열안의 값이 업데이트 되지 않는다면 리렌더링시에는 해당 useEffect는 건너뛸 수 있다.
    - 의존성 배열안에 아무값도 넣지 않은 빈배열([ ])을 넣는다면 첫번째 랜더링시에만 useEffect가 실행된다.
    
    ```jsx
    import React, {useEffect, useState} from 'react';

    function Example() {
      const [date, setData] = useState();

      useEffect(() => {
        ...실행할 로직...
      }, []) // 해당 useEffect는 리렌더링 시에는 실행되지 않는다.

      useEffect(() => {
        ...실행할 로직...
      }, [data]) // 해당 useEffect는 data값이 업데이트 될때마다 실행된다.

      return (
        <div>
          예시
        </div>
      )
    }
    ```