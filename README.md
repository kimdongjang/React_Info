# React_Info
React 라이브러리 및 사용법, 자주 사용하는 코드 정리  


## Redux
+ Action, Store, Reducer, State, Dispatch, Subscribe
#### Action
액션이 호출되면 사전에 정의한 **액션 생성 함수**에서 해당 액션의 객체가 생성되며, 그 객체는 dispatch()함수의 인자로 넘겨지게 된다.  
dispatch()함수는 Reducer()함수를 호출해 새로운 state를 생성한다.
```js
const ADD_TODO = 'ADD_TODO'

// addTodo("오늘 할 일") 과 같이 호출한다.
const addTodo = (text) => {
  return {
    type: ADD_TODO,
    text
  }
}
```

#### Reducer
Reducer는 **이전 상태 정보**(state)와 위의 액션 생성 함수를 통해 발생한 **액션 객체**(action)를 인자로 받는다.  
리듀서 함수가 상태를 업데이트하면 그에 따라 rendering이 된다.  
리듀서는 항상 현재 상태를 '읽기 전용'으로 다룬다.  
불변성을 지켜야하기 때문에 **원본 state 객체를 직접 변경하지 않고 객체에 새 값을 적용**해야 한다. 따라서 Spread 연산자나, concat, Object.assing() 등의 함수를 이용한다.  

#### 리듀서의 상태 업데이트
```js
배열(colors) 최초의 모습
const colors = ['red', 'green']

1) 배열의 요소 추가
colors.push('blue') // colors = ['red', 'green', 'blue'] //Bad(기존 배열의 요소 변경)
[...colors, 'blue'] // colors = ['red', 'green'] // Good(기존 배열의 요소 변경 없음) 

2) 배열의 요소 삭제
colors.pop() // colors = ['red'] // Bad
colors.filter(element => element != 'green') // Good

3)배열의 요소 변경
colors[0] = 'pink' // colors = ['pink', 'green'] // Bad
colors.map((el) => el === 'red' ? 'pink' : el) // Good
```  
  

```js
객체(profile) 최초의 모습
cosnt profile = { name : 'jordan', age : 30 }

1) 객체의 요소 추가
profile.number = 23 // profile = { name: 'jordan', number: 23 } // Bad
{ ...state, number:23 } // Good

2) 객체의 요소 삭제
delete profile.name // profile = undefinded // Bad
{ ...state, age: undefined } // Good
_.omit(state, 'age) // Good, lodash 라이브러리를 사용하는 방법.

3) 객체의 요소 변경
profile.name = 'sam' // profile = { name: 'sam' } // Bad
{ ...state, name : 'Sam' } // Good
```  
  
  
```js
import { SET_USERNAME, SET_DARK_MODE } from '../actions/index'

const initialState = {
  currentUser: { name: 'Hyeonjeong' }, 
  darkMode: false,
}

const settingReducer = (state = initialState, action) => {
  let newState
  switch (action.type) {
    case SET_USERNAME:
      newState = Object.assign({}, state, { currentUser: { name: action.name } })
      break
    case SET_DARK_MODE:
      newState = Object.assign({}, state, { darkMode: action.value })
      break
    default:
      return state
  }
  return newState
}

export default settingReducer
```  
  



## Generator
```js
function* Generator() {
}
```



+ Generator함수는 generator.next()를 호출해야 코드가 실행되고, yield를 한 값을 반환하고 코드의 흐름을 멈춘다.
+ 코드의 흐름이 멈추고 나서 다시 generator.next()를 호출한다. 다음 yield까지 코드가 진행된다.




```js
function* watchGenerator() {
    console.log('모니터링 시작!');
    while(true) {
        const action = yield;
        if (action.type === 'HELLO') {
            console.log('안녕하세요?');
        }
        if (action.type === 'BYE') {
            console.log('안녕히가세요.');
        }
    }
}
```
+ while을 통해 action의 타입에 대해 모니터링을 구현할 수 있다.


## Redux-Saga



# Next.js
1. pages/ 폴더 안에 다른 폴더를 만들면 해당 라우팅의 페이지들은 서버측에서 먼저 로드해줌
  


## ServerSide Cycle
1. Next Server GET 요청을 받음
2. 요청에 맞는 Page를 찾음
3. _app.tsx의 getIniaialProps가 있다면 실행
4. Page Component의 getInitalProps가 있다면 실행, pageProps들을 받아온다.
5. document.tsx의 getInitialProps가 있다면 실행, pageProps들을 받아온다.
6. 모든 props들을 구성하고 _app.js > page Component 순서로 렌더링
7. 모든 Content를 구성하고 _document.js를 실행하여 html 형태로 출력한다.  


#### 공통적인 데이터 패칭이 필요할 경우 _app.tsx에서 미리 데이터 패칭을 해줌

