# React_Info
React 라이브러리 및 사용법, 자주 사용하는 코드 정리  


## Redux
+ Action, Store, Reducer, State, Dispatch, Subscribe
### Action
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

### Reducer
state의 수정 방법을 미리 정의해놓은 함수다.
Reducer는 **이전 상태 정보**(state)와 위의 액션 생성 함수를 통해 발생한 **액션 객체**(action)를 인자로 받는다.  
리듀서 함수가 상태를 업데이트하면 그에 따라 rendering이 된다.  
리듀서는 항상 현재 상태를 '읽기 전용'으로 다룬다.  
불변성을 지켜야하기 때문에 **원본 state 객체를 직접 변경하지 않고 객체에 새 값을 적용**해야 한다. 따라서 Spread 연산자나, concat, Object.assing() 등의 함수를 이용한다.  

#### Object에서의 Spread 연산자 사용 방법
```js
var currentState = { name: '철수', species: 'human'};
currentState = { ...currentState, age: 10}; 

console.log(currentState)// {name: "철수", species: "human", age: 10}

currentState = { ...currentState, name: '영희', age: 11}; 
console.log(currentState); // {name: "영희", species: "human", age: 11}
```

#### 리듀서의 상태 업데이트
  
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


### dispatch
dispatch()를 사용하면 HTML 안에서 reducer를 동작시킬 수 있다.
```dispatch({ type: 'DISPATCH_TYPE' })```과 같은 형태로 사용한다.  
또는 ```dispatch({type: 'DISPATCH_TYPE', payload : { args1, args2, ... } })```과 같은 형태로 데이터를 포함해서 사용할 수 있다.  
리듀서 측에서 ```action.payload```로 받아서 사용할 수 있다.  
  



## Generator
```js
function* Generator() {
}
```



+ Generator함수는 ```generator.next()```를 호출해야 코드가 실행되고, ```yield```를 한 값을 반환하고 코드의 흐름을 멈춘다.
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



