# Operator (연산자)

## 1. String concatenation (문자열 연결)
```
console.log('my' + 'cat');
console.log('1' + 2);
console.log('string literals: 1 + 2 + ${1 + 2}');
```
![1](https://user-images.githubusercontent.com/73509513/155867354-54e0cda9-17db-4a78-902a-402ee93b24c9.PNG)

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
![2](https://user-images.githubusercontent.com/73509513/155867360-1c678876-f27a-4d2e-b8d5-081664e6a319.PNG)


## 3. Increment and decrement operators (증감 연산자)
```
let counter = 2;
const preIncrement = ++counter;
// counter = counter + 1;
// preIncrement = counter;
console.log(`preIncremnet: ${preIncrement}, counter: ${counter}`);
```
![3](https://user-images.githubusercontent.com/73509513/155867375-35409d8b-91a7-4d8c-bfe6-71d642530d59.PNG)

```
const postIncrement = counter++;
// postIncrement = counter;
// counter = counter + 1;
console.log(`postIncremnet: ${postIncrement}, counter: ${counter}`);
```
![31](https://user-images.githubusercontent.com/73509513/155867379-10ee82ad-0587-4b78-806c-366312056b3e.PNG)

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
![4](https://user-images.githubusercontent.com/73509513/155867385-51d736f1-69fc-461d-8392-a413043b457f.PNG)

## 6. Logical operators (논리 연산자)
### || (or), && (and), ! (not) 
```
const value1 = false;
const value2 = 4 < 2;
```

### || (OR) 
OR은 하나라도 true라면 멈춘다.  
```
console.log(`or: ${value1 || value2 || check()}`);
```
![51](https://user-images.githubusercontent.com/73509513/155867610-08adcd33-9a38-43ca-98d1-7f828ed78fc4.PNG)

```
function check() {
    for (let i = 0; i < 10; i++) {
        //wasting time
        console.log('false');
    }
    return true;
}
```
check는 결국 true를 return 한다.

### && (AND) 
모두 참이여야 true값을 return 한다.
```
console.log(`AND: ${value1 && value2 && check()}`);
```
![52](https://user-images.githubusercontent.com/73509513/155867634-8f5cc05c-dced-492a-a285-dd8f214248e6.PNG)

and는 null을 check할때도 많이 쓰인다.  

nullableObject && nullableObject.something
nullableObject가 null이면 false가 되어 뒷쪽이 실행이 되지 않는다.
nullableObject null이 아닐때만 nullableObject.something을 받아오게 된다.
```
if(nullableObject != null) {
    nullableObject.something;
}
```

### ! (NOT) 
값을 반대로 바꿔서 보여준다.  
```
console.log(!value1);
```
![53](https://user-images.githubusercontent.com/73509513/155867445-26c3eb15-07ef-4d16-9ed1-3fd963b98227.PNG)

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
![6](https://user-images.githubusercontent.com/73509513/155867642-c7eb937d-459e-4dc0-a272-13e528356b02.PNG)

### === strict equality
타입이 다르다는 것을 검사한다.  
```
console.log(stringFive === numberFive);
console.log(stringFive !== numberFive);
```
![7](https://user-images.githubusercontent.com/73509513/155867645-9e449382-e629-4b41-bdde-bcdc54b84ddd.PNG)

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
![8](https://user-images.githubusercontent.com/73509513/155867648-798a9812-a45c-4780-97cc-64fc6ba13d66.PNG)

### equality = puzzler
```
console.log(0 == false); // 0은 false로 간주되어 true
console.log(0 === false); // 0은 boolean 타입이 아니기 떄문에 false
console.log('' == false); // ture
console.log('' === false); // false
console.log(null == undefined); // null과 undefined은 같은것으로 간주해 true
console.log(null === undefined); // null과 undefined은 다른 타입이므로 false
```
![9](https://user-images.githubusercontent.com/73509513/155867656-8f467e4c-69d7-4c3b-978c-1a6d42c2e934.PNG)

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
![10](https://user-images.githubusercontent.com/73509513/155867663-48f40d13-8843-45b8-876a-9d3354c140e6.PNG)

name이 ellie라면 Welcome, Ellie! 출력  
name이 ellie가 아니고 coder라면 You are amazing coder 출력  
name이 ellie, coder도 아니라면 unkwnon 출력  

## 9. Ternary operators (삼항 조건 연산자)
### ?
### condition ? value1 : value2;  
```
console.log(name === 'ellie' ? 'yes' : 'no');
```
![11](https://user-images.githubusercontent.com/73509513/155867667-7603c508-03cb-4d4e-8c2e-e260b1843c84.PNG)

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
![12](https://user-images.githubusercontent.com/73509513/155867669-266ed0ad-fb2f-42f4-945a-f7ee42ee4876.PNG)

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
![13](https://user-images.githubusercontent.com/73509513/155867673-b169d3b0-5cf8-433b-a24c-f3cf8438c0db.PNG)

while의 조건문이 false가 나올때까지 무한적으로 반복한다.

### do while
```
do {
    console.log(`do while: ${i}`);
    i--;
} while (i > 0);
```
![14](https://user-images.githubusercontent.com/73509513/155867675-00d7a824-f3ee-4751-b6ee-cd9ceee847b6.PNG)

{}을 실행한 다음 조건이 맞는지 여부를 검사한다.

### for
for (begin; condition; step)  
begin을 처음 1회 실행하고, condition이 맞는지를 검사한 후 블럭이 실행되면 step이 실행되게 된다.
```
for (i = 3; i > 0; i--) {
    console.log(`for: ${i}`);
}
```
![15](https://user-images.githubusercontent.com/73509513/155867685-d7791a28-c940-43d4-b233-809bd67a5144.PNG)

```
for (let i = 3; i > 0; i = i - 2) {
    console.log(`inline variable for: ${i}`);
}
```
![16](https://user-images.githubusercontent.com/73509513/155867687-e3242feb-2561-496c-89b9-d8b336843fd3.PNG)

### nested loops (이중 반복(중첩 반복))
```
for (let i = 0; i < 10; i++) {
    for (let j = 0; j < 10; j++) {
        console.log(`i: ${i}, j:${j}`);
    }
}
```
되도록 피하는것이 좋다.


### break, continue
break: loop를 완전히 끝낸다.  
continue 돌고있는 loop를 스킵하고 다음 step으로 넘어간다.  
 
### break를 사용하여 8이면 멈추는 loop를 작성  
```
for (let i = 0; i < 11; i++) {
    if (i > 8) {
        break;
    }
    console.log(`break: ${i}`);
}
```
![17](https://user-images.githubusercontent.com/73509513/155867695-5860982f-e3b2-49f9-ab6f-c61faa45c293.PNG)

### continue를 사용하여 i의 값이 짝수일경우 출력
```
for (let i = 0; i < 11; i++) {
    if (i % 2 !== 0) {
        continue;
    }
    console.log(`even: ${i}`);
}
```
![18](https://user-images.githubusercontent.com/73509513/155867699-e280f285-3794-4a38-a65d-66a9e7f5f64f.PNG)

