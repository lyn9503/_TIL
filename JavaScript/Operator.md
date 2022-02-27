# Operator (연산자)

## 1. String concatenation (문자열 연결)
```
console.log('my' + 'cat');
console.log('1' + 2);
console.log('string literals: 1 + 2 + ${1 + 2}');
```
string literals는 줄바꿈이나 중간에 '' 같은 것도 문자열로 변환해 보여준다.

## 2. Numeric operators (숫자 연산자)
```
console.log(1 + 1); // add
console.log(1 - 1); // substract
console.log(1 / 1); // divide
console.log(1 * 1); // multiply
console.log(1 % 1); // remainder
console.log(1 ** 1); // expontiation
```

## 3. Increment and decrement operators (증감 연산자)
```
let counter = 2;
const preIncrement = ++counter;
// counter = counter + 1;
// preIncrement = counter;
console.log(`preIncremnet: ${preIncrement}, counter: ${counter}`);
```
```
const postIncrement = counter++;
// postIncrement = counter;
// counter = counter + 1;
console.log(`postIncremnet: ${postIncrement}, counter: ${counter}`);
```

## 4. Assignment operators (할당 연산자)
```
let x = 3;
let y = 6;
x += y; // x = x + y;
x -= y;
x *= y;
x /= y;
```

## 5. Comparison operators (비교 연산자)
```
console.log(10 < 6); // less than
console.log(10 <= 6); // less than or equal
console.log(10 > 6); // greater than
console.log(10 >= 6); // greater than or equal
```

## 6. Logical operators (논리 연산자)
### || (or), && (and), ! (not) 
```
const value1 = false;
const value2 = 4 < 2;
```

### || (OR) 
or은 하나라도 true라면 멈춘다.  
```
console.log(`or: ${value1 || value2 || check()}`);
//check는 true를 return
```

### && (AND) 
모두 참이여야 true값을 return  
```
console.log(`or: ${value1 || value2 || check()}`);
// and는 null을 check할때도 많이 쓰인다.
// nullableObject && nullableObject.something
// nullableObject가 null이면 false가 되어 뒷쪽이 실행이 되지 않는다.
// nullableObject null이 아닐때만 nullableObject.something을 받아오게 된다.

if(nullableObject != null) {
    nullableObject.something;
}
```

### ! (NOT) 
값을 반대로 바꿔서 보여준다.  
```
console.log(!value1);

function check() {
    for (let i = 0; i < 10; i++) {
        //wasting time
        console.log('false');
    }
    return true;
}
```

## 7. Equality (동등 연산자)
```
const stringFive = '5';
const numberFive = 5;
```

### == loose equality
타입을 변경해서 검사한다.  
```
console.log(stringFive == numberFive);
console.log(stringFive != numberFive);
```

### === strict equality
타입이 다르다는 것을 검사한다.  
```
console.log(stringFive === numberFive);
console.log(stringFive !== numberFive);
```

만약 검사를 한다면 **strict equality**를 사용하는 것이 더 좋다.

### object equality by reference
```
const ellie1 = {name: 'ellie'};
const ellie2 = {name: 'ellie'};
const ellie3 = ellie1;
console.log(ellie1 == ellie2); // 각각 다른 reference를 가지고 있기 때문에 false
console.log(ellie1 === ellie2); // 타입의 여부와 상관없이 다른 reference를 가지기 때문에 false
console.log(ellie1 === ellie3); // ellie3은 ellie1의 reference값을 가지고 있기 때문에 true
```

### equality = puzzler
```
console.log(0 == false); // 0은 false로 간주되어 true
console.log(0 === false); // 0은 boolean 타입이 아니기 떄문에 false
console.log('' == false); // ture
console.log('' === false); // false
console.log(null == undefined); // null과 undefined은 같은것으로 간주해 true
console.log(null === undefined); // null과 undefined은 다른 타입이므로 false
```

## 8. Conditional operators (조건문)
### if, else if, else
```
const name = 'ellie';
if (name === 'ellie') {
    console.log('Welcome, Ellie!');
} else if (name === 'coder') {
    console.log('You are amazing coder')
} else {
    console.log('unkwnon')
}
```
name이 ellie라면 Welcome, Ellie! 출력  
name이 ellie가 아니고 coder라면 You are amazing coder 출력  
name이 ellie, coder도 아니라면 unkwnon 출력  

## 9. Ternary operators (삼항 조건 연산자)
### ?
### condition ? value1 : value2;  
```
console.log(name === 'ellie' ? 'yes' : 'no');
```
ellie가 true면 yes, 아니면 no 출력

## 10. Switch statement
```
const browser = 'IE';
switch (browser) {
    case 'IE':
        console.log('go away!');
        break;
    case 'Chrome':
        console.log('love you!');
        break;
    case 'Firefox':
        console.log('love you!');
        break;
    default:
        console.log('same all!');
        break;    
}
```
browser의 내용에 따라 console의 내용이 변한다.
if, else if로 반복하는 것 보단 switch를 사용하는 것이 좋다.

## 11. Loops (반복문)

### while
```
let i = 3;
while (i > 0) {
    console.log(`while: ${i}`);
    i--;
}
```
while의 조건문이 false가 나올때까지 무한적으로 반복한다.

### do while
```
do {
    console.log(`do while: ${i}`);
    i--;
} while (i > 0);
```
{}을 실행한 다음 조건이 맞는지 여부를 검사한다.

### for
for (begin; condition; step)  
begin을 처음 1회 실행하고, condition이 맞는지를 검사한 후 블럭이 실행되면 step이 실행되게 된다.
```
for (i = 3; i > 0; i--) {
    console.log(`for: ${i}`);
}

for (let i = 3; i > 0; i = i - 2) {
    console.log(`inline variable for: ${i}`);
}
```

### nested loops (이중 반복(중첩 반복))
```
for (let i = 0; i < 10; i++) {
    for (let j = 0; j < 10; j++) {
        console.log(`i: ${i}, j:${j}`);
    }
}
// 되도록 피하는것이 좋다.
```

### break, continue
break: loop를 완전히 끝낸다.  
continue 돌고있는 loop를 스킵하고 다음 step으로 넘어간다.  
 
### break를 사용하여 8이면 멈추는 loop를 작성  
```
for (let i = 0; i > 11; i++) {
    if (i > 8) {
        break;
    }
    console.log(`even: ${i}`);
}
```
### continue를 사용하여 i의 값이 짝수일경우 출력
```
for (let i = 0; i > 11; i++) {
    if (i % 2 !== 0) {
        continue;
    }
    console.log(`even: ${i}`);
}
```
