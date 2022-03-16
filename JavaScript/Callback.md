# Callback

자바스크립트는 동기적이며, hoisting된 이후부터 코드가 작성한 순서에 맞춰서 하나하나씩 동기적으로 실행된다.  
hoisting이란 var, function declaration 이런 함수 선언들이 자동적으로 제일 위로 올라가는 것이며, hoisting이 된 이후부터 코드가 나타나는 순서대로 자동적으로 실행된다. 

```
console.log('1');
setTimeout(() => console.log('2'), 1000);
console.log('3');
```
synchronous는 정해진 순서대로 코드가 실행되는 것이며,
asynchronous는 비동기적으로 언제 코드가 실행될지 예측할 수 없는 것이다.
setTimeout()는 브라우저에서 제공되는 api로 지정한 시간이 지나면 전달한 콜백함수를 호출한다.

## Synchronois callbacks
```
function printImmediate(print) {
    print();
}
printImmediate(()=> console.log('hello'));
```

## Asynchronois callbacks
```
function printWithDelay(print, timeout) {
    setTimeout(print, timeout);
}
printWithDelay(()=> console.log('async callback'), 2000);
```

모든 함수의 선언은 hoisting되기 때문에 printImmediate와 printWithDelay는 제일 위로 올라가게 되며,  
1 출력  
2는 비동기(브라우저에 1초뒤에 출력하라는 요청)  
3 출력  
printImmediate 동기  
2 출력  
printWithDelay 출력  
순으로 동기 비동기가 이루어진다.  

![1](https://user-images.githubusercontent.com/73509513/158008559-77adfcf7-5ab3-43d8-a416-2da00ef980e6.PNG)

```
// hoisting
 function printImmediate(print) {
    print();
}

function printWithDelay(print, timeout) {
    setTimeout(print, timeout);
}

console.log('1'); // 동기
setTimeout(() => console.log('2'), 1000); // 비동기
console.log('3'); // 동기
printImmediate(()=> console.log('hello')); // 동기
printWithDelay(()=> console.log('async callback'), 2000); // 비동기
```

동기, 비동기는 위의 순서대로 이루어진다.
