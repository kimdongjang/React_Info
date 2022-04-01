# React_Info
React 라이브러리 및 사용법, 자주 사용하는 코드 정리

# Generator
```
function* Generator() {
}
```

+ Generator함수는 generator.next()를 호출해야 코드가 실행되고, yield를 한 값을 반환하고 코드의 흐름을 멈춘다.
+ 코드의 흐름이 멈추고 나서 다시 generator.next()를 호출한다. 다음 yield까지 코드가 진행된다.

```
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


# Redux-Saga


