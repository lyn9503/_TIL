# async & await

promise의 then을 chain으로 구현하게 되면 조금 코드가 난잡해진다. 이러한 문제를 해결하기 위해 async와 await을 사용한다.  
기존에 존재하는 것(class, promise)를 감싸서 간편하게 사용할 수 있는 api를 syctactic sugar라고 한다.  

async와 await은 promise를 깔끔하게 사용할 수 있는 api이다.  
promise를 배제하는 것이 아닌 async와 await과 함께 어울려서 사용해야 한다.  

## 1. async
```
function fetchUser() {
    // 사용자의 데이터를 백엔드에서 받아오는 함수
    // do network request in 10 secs...
    return 'ellie';
}

const user = fetchUser();
console.log(user);
```

fetchUser가 호출이 되면 함수가 선언된 곳으로 가서 함수의 코드 블록을 실행한다.   
이후 10초가 지나면 네트워크에서 데이터를 받아오게 되면 ellie가 return 되게 된다.  
그 후 return된 ellie가 user에 할당된 후 ellie가 출력되게 된다.  
이렇게 오래 걸리는 것은 비동기적으로 처리할 수 있게 해줘야 한다.  

```
function fetchUser() {
    return new Promise((resolve, reject) => {
        resolve('ellie');
    });
}
```
promise는 pending 상태가 되어있는 것을 확인할 수 있는데, promise는 resolve나 reject를 사용하지 않아 계속 pending 상태로 남아있게 된다. 이런 경우 블록 안에 resolve를 사용하면 된다.  

```
user.then(console.log);

async function fetchUser() {
    return 'ellie';
}
```
위의 방법처럼 사용해도 되지만 함수 앞에 async를 붙이면 간편하게 비동기적으로 변환된 promise를 return 해 만들어지게 된다.  

## 2. await
```
function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

async function getApple() {
    await delay(3000);
    return '🍎';
}

async function getBanana() {
    await delay(3000);
    return '🍌';
}

function pickFruits() {
    return getApple()
    .then(apple => {
        return getBanana()
        .then(banana => `${apple} + ${banana}`)
    })
}

pickFruits().then(console.log);
```

await란 키워드는 async 함수 안에서만 사용할 수 있다.  
delay라는 함수는 새로운 promise를 생성하는데 임의로 생성한 ms의 정해진 시간이 지나면 resolve를 호출하는 promise를 return 하게 된다.  
getApple 함수에서 3초를 지정했기 때문에 resolve는 3초 뒤 resolve를 호출하는 promise가 전달된다.  
await delay(3000);을 사용하게 되면 3초가 지날 때까지 기다리게 되며, 3초 뒤 🍎을 return 하는 promise가 만들어지게 된다.  
getBanana도 마찬가지로 promise가 만들어지게 된다.  
pickFruits()을 .then을 이용해 만들게 되면 콜백 지옥과 비슷하므로 async로 만드는 것이 좋다.  
```
async function pickFruits() {
    const apple = await getApple();
    const banana = await getBanana();
    return `${apple} + ${banana}`;
}
```
이렇게 async와 await을 사용하게 되면 매우 간단하게 사용할 수 있다.  
만약 에러 처리가 필요할 경우 try catch를 사용해 예외 처리를 해주면 된다.  

## 3. await 병렬처리
```
async function pickFruits() {
    const applePromise = getApple();
    const bananaPromise = getBanana();
    const apple = await applePromise;
    const banana = await bananaPromise;
    return `${apple} + ${banana}`;
}
```
사과와 바나나는 각각 1초씩 기다렸다가 return 되게 되는데 이는 매우 비효율적이다.  
사과와 바나나를 각각 Promise로 생성한 후 await으로 promise를 연동시키면 병렬처리된다.  
사과와 바나나의 promise를 만들었기 때문에 만들자마자 getApple과 getBanana의 코드가 실행되게 되어 병렬적으로 동시에 기다렸다가 출력되게 된다.  
하지만 동시다발적으로 병렬적으로 코드를 작성할 때는 위 코드처럼 작성하지 않는다.  

## 4. useful
useful은 promise에서 제공하는 api이다.  
```
function pickAllFruits() {
    return Promise.all([getApple(), getBanana()])
    .then(fruits => fruits.join(' + '));
}
pickAllFruits().then(console.log);
```
all은 promise의 배열을 전달하게 되면 모든 promise들이 병렬적으로 받을 때까지 모아주는 api이다.  
```
function pickOnlyOne() {
    return Promise.race([getApple(), getBanana()]);
}

pickOnlyOne.then(console.log);
```
race는 만약 사과가 2초고 바나나가 1초일 때 시간이 적은 바나나부터 출력되게 하는 api이다.  
