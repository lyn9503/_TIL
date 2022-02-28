# Function
## Function(함수)
함수란 Input(parameters) 을 받아서 Output(return)을 하는 것 이며,  
서브 프로그램이라고도 불리고, 여러번 재사용이 가능하다.  
또한 함수는 한가지의 일이나 어떤 값을 계산하기 위해 사용되고 있다.  
하나의 함수는 한가지의 일만 하도록 만들어야 하며 자바스크립트에서 함수는 object의 일종이다.  

### 함수의 기본적인 문법
function name(param1, param2) { body... return; }  


## Function Declaration (함수 선언)
### 1. Function (함수)
```
function printHello() {
    console.log('hello');
}

printHello();
```
위의 함수는 hello만 출력되게 하므로 아래의 함수로 작성하는 것이 좋다.  
```
function log(message) {
    console.log(message);
}
```
parameter로 message를 전달하면 전달된 message를 화면에 출력한다.
```
log('Hello@');
```
console에 Hello@를 출력

### 2. Parameters (매개변수)
premitive 타입은 메모리에 value가 저장되어 있어 value를 전달한다.  
object 타입은 메모리에 reference가 저장되어 있어 reference를 전달한다.  
```
function changeName(obj) {
    obj.name = 'coder';
}
```
changeName 함수는 전달된 오브젝트에 이름을 coder로 변경한다.  
```
const ellie = { name: 'ellie' };
changeName(ellie);
console.log(ellie);
```
const로 ellie를 지정하면 메모리에 object가 만들어진 reference가 들어가고 reference는 메모리에서 object를 가르킨다.  
changeName(ellie);을 전달하게 되면 obj.name가 가르키고 있는 ellie를 coder로 변경하게 된다.  

### 3. default parameters (기본값 매개변수)
default parameters는 ES6에서 추가되었다.  
```
function showMessage(message, from) {
    console.log(`${message} by ${from}`);
}
showMessage('Hi!');
```
showMessage는 message와 from parameter를 받아온다.  
하지만 위 함수는 Hi!란 하나의 parameter를 받아와 console에는 Hi!와 undefined만 출력하게 된다.  
예전에는 이렇게 parameter를 받아오지 못하는것을 대비해 아래의 코드처럼 사용했다.
```
function showMessage(message, from) {
    if(from === undefined) {
        from = 'unknown';
    }
    console.log(`${message} by ${from}`);
}
```
from이 undefined이면 unknown으로 출력하게 했지만 아래 코드처럼 현재는 parameter 이름의 옆에 작성하면 해결이 된다.  
```
function showMessage(message, from = 'unknown') {
    console.log(`${message} by ${from}`);
}
showMessage('Hi!');
```

### 4. Rest parameters (Rest 매개변수)
Rest parameters는 ES6에서 추가되었다.  
```
function printAll(...args) {
    for (let i = 0; i < args.length; i++) {
        console.log(args[i]);
    }
}
printAll('dream', 'coding', 'ellie');
```
parameter에 ...을 적으면 Rest parameters로 불리게 되는데 이는 배열형태로 전달되게 된다.  
그러므로 ...args는 'dream', 'coding', 'ellie' 3개의 parameter가 담겨진 배열형태이다.  
위처럼 length를 이용해 출력해도 되지만 아래 코드처럼 문법을 사용해 간편하게 출력할 수도 있다.
```
function printAll(...args) {
    for (const arg of args) {
        console.log(arg);
    }
}
```
```
function printAll(...args) {
    args.forEach((arg) => console.log(arg));
}
```
아니면 위처럼 함수형 언어을 이용해 더욱 간편하게 출력할 수도 있다.

### 5. Local scope
```
let globalMessage = 'global'; // global variable
function printMessage() {
    let message = 'hello';
    console.log(message); // local variable
    console.log(globalMessage);
    function printAnother() {
        console.log(message);
        let childMessage = 'hello';
    }
}
printMessage();
```
함수나 { } 안에서 변수를 선언하게 되면 지역변수이다.  
지역변수는 안에서만 접근 가능하며 함수나 { } 밖에서 사용시 오류가 발생한다.  
함수 안에는 또다른 함수를 정의할 수 있는데 printMessage의 함수안에 정의된 printAnother는
자식으로 취급되어 부모인 printMessage의 지역변수를 사용할 수 있다.
이러한 전역변수나 지역변수를 scope라고 한다.  
자바스크립트에서 scope란 유리창에 틴트가 처리된 거랑 똑같으며
밖에서는 안이 보이지 않고 안에서만 밖을 볼 수 있다. 라고 생각하면 이해하기 쉽다.  

### 6. Return a value
```
function sum(a, b) { 
    return a + b;
}
const result = sum(1, 2); // 3
console.log(`sum: ${sum(1, 2)}`);
```
함수는 parameter를 리턴받아서 계산되어 지는데 함수에 return이 없어도 return undefined가 들어가있어 생략이 가능하다.

### 7. Early return, early exit
```
function upgradeUser(user) {
    if(user.point > 10) {
        // 10 이상의 user point가 있으면 로직을 upgrade
    }
}
```
이런 요구일때 if안에 로직을 많이 작성하면 가독성이 떨어진다.

이럴때는 if와 else를 번갈아 쓰는 것보다 아래처럼 작성하는 것이 좋다.
```
function upgradeUser(user) {
    if(user.point <= 10) {
        return;
    }
    // 로직 작성
}
```
위처럼 조건이 맞지 않을경우 빨리 return해 함수를 종료하고 그 뒤에 필요한 로직을 작성하는 것이 좋다.

## Function expression (함수 표현식)
### 1. Function expression (함수 표현식)
함수는 다른 변수와 마찬가지로 변수에 할당되고, 함수에 parameter로 전달되며 return값으로도 return이 되는데  
이를 가능하게 하는 것이 Function expression이다.  
```
const print = function() { // anonymous function
    console.log('print');
}
print(); // print 함수 호출
const printAgain = print;
printAgain(); // printAgain에 담긴 print 함수 호출
const sumAgain = sum; 
console.log(sumAgain(1, 3)); // sumAgain에 위에 작성한 sum 함수가 담긴 sum함수를 호출해 계산
```
함수를 선언함과 동시에 변수에 할당하는 방법이 있는데 이를 anonymous function이라고 부르며,  
함수의 이름을 정하게 되면 named function이 된다.  

**Function Declaration과 Function expression의 차이점**  
Function expression은 할당된 다음부터 호출이 가능한 반면  
Function Declaration은 함수가 호출되기 이전에도 호출이 가능하다.  

### 2. Callback function (Callback 함수)
```
function randomQuiz(answer, printYes, printNo) {
    if(answer === 'love you') {
        printYes();
    } else {
        printNo();
    }
}
// anonymous function
const printYes = function() {
    console.log('Yes');
}

// named function
const printNo = function print() {
    console.log('No');
    // print();
    // recursions function
    // 함수안에서 함수 자신 스스로를 부르는 것을 recursion function라고 한다.
    // 이렇게 함수를 계속 호출하게 되면 call stack 에러가 발생한다.
}
randomQuiz('wrong', printYes, printNo);
randomQuiz('love you', printYes, printNo);
```
위 코드는 정답인 answer와 정답이 맞거나 틀릴경우 호출하는 printYes와 printNo를 전달하게 되는데  
이처럼 상황에 맞는 함수를 호출하는 것을 Callback function이라고 한다.

### Arrow function (화살표 함수)
Arrow function은 항상 anonymous function이다.
```
const simplePrint = function() {
    console.log('simplePrint');
}
// Function expression

const simplePrint = () => console.log('simplePrint');
const add = (a, b) => a + b;
const simpleMultiply = (a, b) => {
    // do something more
    return a * b;
}
// Arrow function
```
Function expression보다 간결하게 작성할 수 있으며, 만약 { }을 사용하게 된다면 return을 사용해주어야 한다.  

### IIFE: Immediately Invoked Function Expression (즉시 실행 함수 표현)
```
function hello() {
    console.log('IIFE');
}
hello();
```
Function expression은 기본적으로 함수를 작성하고 따로 호출해줘야 한다.
```
(function hello() {
    console.log('IIFE');
})();
```
하지만 IIFE는 함수에 ( )로 묶어주고 끝나는 부분에 (); 을 작성해주면 함수를 작성함과 동시에 호출이 가능하다.
