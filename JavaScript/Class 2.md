# 클래스 보충

## 1. 클래스 정의
```
class Counter {
    constructor(runEveryFiveTimes) {
        this.counter = 0;
        this.callback = runEveryFiveTimes;
    }

    increase(/*runIf5Times*/) {
        this.counter++;
        console.log(this.counter);
        if(this.counter % 5 === 0) {
            console.log('yo!');
        }
    }
}

const coolCounter = new Counter();

coolCounter.increase();
coolCounter.increase();
coolCounter.increase();
coolCounter.increase();
coolCounter.increase();
```

Counter라는 클래스는 생성하게 되면 counter라는 변수가 0부터 시작한다(초기화 된다).  
class 안에는 increase라는 함수가 있다(클래스 내부에서 함수 선언시 function을 적을 필요가 없다).  
숫자가 5배수 일때 출력하려면 if문을 사용해서 출력하면 된다.  

문제점은 counter 클래스 내부에서 작동하기 때문에 coolCounter를 쓰는 사람이 출력되는 문장을 조절할 수 없다.  

## 2. 클래스에 콜백 함수 사용

```
class Counter {
    constructor() {
        this.counter = 0;
        this.callback = runEveryFiveTimes;
    }

    increase(runIf5Times) {
        this.counter++;
        console.log(this.counter);
        if(this.counter % 5 === 0) {
            runIf5Times(this.counter);
        }
    }
}

function printSomething(num){
    console.log(`yo! ${num}`);
}

function alertNum(num) {
    alert(`alert! ${num}`);
}

const coolCounter = new Counter();

coolCounter.increase();
coolCounter.increase();
coolCounter.increase();
coolCounter.increase();
coolCounter.increase();

coolCounter.increase();
coolCounter.increase();
coolCounter.increase();
coolCounter.increase();
coolCounter.increase();
```

콜백 함수를 이용해서 외부에서 처리하게 하면 문제를 해결할 수 있다.  
만약 5배수 일때 yo!라는 문자열과 숫자를 같이 출력하고 싶다면 if문의 runIf5Times() 호출시에 counter를 전달하고,  
아래 printSomthing 함수에 num이라는 인자를 받아 console.log에 `${num}`을 추가하면 되며, counter가 10일때 알림을 울리게 할 수도 있다.  

콜백 함수를 사용했을때 장점은 콜백 함수를 전달 함으로써 원하는 기능을 수행할 수 있다.  

## 3. 콜백 함수를 전달하지 않았을때 해결

```
class Counter {
    constructor(runEveryFiveTimes) {
        this.counter = 0;
        this.callback = runEveryFiveTimes;
    }

    increase() {
        this.counter++;
        console.log(this.counter);
        if(this.counter % 5 === 0) {
            this.callback && this.callback(this.counter);
            /*
            if(this.callback) { // true
                this.callback(this.counter);
            }
            */
        }
    }
}

function printSomething(num){
    console.log(`yo! ${num}`);
}

function alertNum(num) {
    alert(`alert! ${num}`);
}

const printCounter = new Counter(printSomething);
const alertCounter = new Counter(alertNum);

printCounter.increase();
printCounter.increase();
printCounter.increase();
printCounter.increase();
printCounter.increase();

alertCounter.increase();
alertCounter.increase();
alertCounter.increase();
alertCounter.increase();
alertCounter.increase();

```
콜백 함수를 전달할때 함수에서 전달하지 않고 constructor에서 받는게 좋다.  
constructor에서 콜백 함수를 사용할 경우 increase 호출될 때 마다 counter가 5배가 되면 callback 함수를 호출한다.  

Counter를 만들때 어떤 콜백 함수도 전달하지 않으면 runEveryFiveTimes은 undefined, 즉 this.callback은 undefined가 된다.  
![캡처](https://user-images.githubusercontent.com/73509513/158921197-49ef5271-a28c-454d-ab03-77e78af70836.PNG)  
이 상태로 실행하면 TypeError가 발생하고 this.callback은 함수가 아니라고 경고메세지를 발생하게 된다.  
this.callback이 데이터가 있는지 없는지, undefined인지를 확인한 후 undefined이 아닐경우 보내야한다.  

이 문제는 if에 if문으로 this.callback이 undefined이 아닐때 호출하게 하면 된다.  
아니면 `this.callback && this.callback(this.counter);` this.callback이 true일경우(undefined이 아닐경우) 호출하게 해도 된다.  

### 출력

![2](https://user-images.githubusercontent.com/73509513/158921253-05efc747-f73f-40d4-9f2f-702e10cebf2e.PNG)  

![1](https://user-images.githubusercontent.com/73509513/158921259-c4eaa2e2-8166-462f-b319-7a3d1bc694fa.PNG)


## 결론
클래스를 하나의 완전히 다 만들어진 완전체로 만들지 말고, 원하는 기능을 끼워 맞춰서 재사용(refactoring)이 가능하도록 작성하는 것이 좋다.  
