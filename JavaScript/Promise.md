# Promise
Promise는 자바스크립트에서 제공하는 비동기를 간편하게 처리할 수 있게 도와주는 object이다.  
정해진 장시간의 기능을 수행하고 나서 정상적으로 기능이 수행되었다면 메세지와 함께 처리된 결괏값을 전해주고,  
기능을 수행하다가 예상치 못한 문제가 발생하면 에러를 발생시킨다.  
새로운 promise가 만들어질 때는 전달한 executor라는 콜백 함수가 바로 실행이 된다.   
state(상태), producer, consumer의 이해가 중요하다.  

state: pending -> fulfilled or rejected  
producer vs consumer

## 1. Producer
```
const promise = new Promise((resolve, reject) => {
    setTimeout(() =>{
        resolve('ellie');
    }, 2000);
    // 데이터를 받아왔을 때 ellie가 맞으면 resolve라는 콜백 함수로 전달
    setTimeout(() =>{
        reject(new Error('no network'));
    }, 2000);
});
```
executor라는 콜백 함수를 전달해주어야 하는데 executor에는 두 가지의 콜백 함수가 있다.  
기능을 정상적으로 수행해서 마지막에 최종 데이터를 전달하는 resolve와,  
기능을 수행하다가 중간에 문제가 생기면 호출하게 될 reject 두 가지로 나누어져 있다.  

## 2. Consumers: then, catch, finally
```
promise
    .then(value => {
        console.log(value);
    })
    .catch(error => {
        console.log(error);
    })
    .finally(() => {
        console.log('finally');
    });
```
then은 promise가 정상적으로 수행이 되어서 마지막에 최종적으로 resolve에서 전달한 값이 value의 parameter로 전달되어 들어온다.  
then을 이용해서 reject를 수행시키면 Uncaught(잡히지 않은 오류)가 나타나게 되는데, 이는 성공적인 case만 다루어서이다.  
에러를 catch 함수로 에러 발생 시 어떻게 처리할 것인지를 작성하면 된다.  
최근에 추가된 finally는 성공, 실패 유무와 상관없이 무조건 마지막에 호출되는 함수이다.  

## 3. Promise chaining
```
const fetchNumber = new promise((resolve, reject) => {
    setTimeout(() => resolve(1), 1000);
});
// resolve 값은 1
fetchNumber
.then(num => num * 2) // 값 2
.then(num => num * 3) // 값 6
.then(num => {
    return new Promise((resolve, reject) => {
        setTimeout(() =>resolve(num - 1), 1000);
    }); // 새로운 promise 생성 후 6의 값을 호출해 1을 빼므로 값은 5
})
.then(num => console.log(num)); // 5 출력
```
then은 값을 바로 전달해도 되고, 아니면 또 다른 비동기인 promise를 전달해도 된다.  

## 4. Error Handling
```
// 총 3가지의 함수를 return 하는 예제
const getHen = () => 
    new Promise((resolve, reject) => {
        setTimeout(() => resolve('hen'), 1000);
    });
// getHen는 닭을 받아오는데, 1초 이후 hen을 return 한다.

const getEgg = hen =>
    new Promise((resolve, reject) => {
        setTimeout(() => resolve(`${hen} => egg`), 1000);
        setTimeout(() => reject(new Error(`error! ${hen} => egg`)), 1000);
    });
// getEgg는 hen을 받아와서 egg를 받아오는 promise를 return
// egg를 받아오는 과정에 오류가 생긴다면 error 발생
const cook = egg =>
    new Promise((resolve, reject) => {
        setTimeout(() => resolve(`${egg} => fried egg`), 1000);
    });
// cook은 egg를 받아와서 fried egg를 만드는 함수
```
```
/**
getHen()
    .then(hen => getEgg(hen))
    .then(egg => cook(egg))
    .then(meal => console.log(meal))
**/
```
콜백 함수를 전달할 때 받아오는 value를 다음 함수 하나를 호출할 때 hen => 를 생략할 수 있다.  

```
getHen() //
    .then(getEgg)
    .catch(error => {
        return 'bread';
    })
    .then(cook)
    .then(console.log)
    .catch(console.log);
```
만약 egg를 받아올 때 문제가 생기지 않도록 에러 발생 시 bread로 대체해 문제를 해결할 수 있다.  
