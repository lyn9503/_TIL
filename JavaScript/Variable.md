# Variable(변수)

## 1. Use strict
**ES5에서 추가**되었으며 **기본적인 자바스크립트 문법에서 사용**한다.  
자바스크립트는 느슨하게 개발하려는 목적으로 인해 대부분의 오류를 묵인하려 한다.  
이러한 현상을 피하기위해 Use strict를 사용하면 보이지 않던 오류들이 보이게 된다.  
```
'use strict';
```

## 2. Variable
### let
![12](https://user-images.githubusercontent.com/73509513/155650406-a05ea9ad-2274-46f6-89c8-d5231aa4708b.png)
let이라는 변수를 지정하게 되면 **메모리를 가르키는 포인터가 생성**된다.  
이 변수가 가르키는 **메모리의 공간에 hello라는 값이 저장**되게 된다.  
let은 **ES6에서 추가**되었다.
```
let name = 'ellie';
console.log(name);
name = 'hello';
console.log(name);
```
![1](https://user-images.githubusercontent.com/73509513/155651299-049d8bb7-c09c-4b09-aad0-18455697fe30.png)

### var
var hoisting 이란? **어디에 선언했는지 상관없이 항상 제일위로 선언을 끌어올려 주는 것이다.**  
let과 다르게 변수에 **값을 지정하지 않아도 사용**이 가능하지만 **선언하지도 않은 값**을 사용할 수 있으므로 **위험성**이 존재한다.  
**block scope**을 무시한다.
```
console.log(age);
age = 4;
console.log(age);
var age
```
![2](https://user-images.githubusercontent.com/73509513/155652227-1ff26d04-5aab-436d-902c-ce32bf78a7f5.png)

### Block scope
**밖에서는 더이상 블럭안에 있는 내용을 볼 수 없으며**, console.log로 블럭 밖에서 접근해도 **아무값도 나오지 않는다.**
```
{
    let name = 'ellie';
    console.log(name);
    name = 'hello';
    console.log(name);
}
```

### Global scope
**어느곳에서나 접근**이 가능하며 **블럭 안에 작성**해도 접근이 가능하다.  
어플리케이션이 실행되는 순간부터 **메모리에 상주**하기 때문에 **최소한**으로 사용하는것이 좋고, 가능하면 **클래스나 함수등 필요한 부분만 사용하는 것**이 좋다.  
```
let globalName = 'global name';  
```

## 3. constants
![13](https://user-images.githubusercontent.com/73509513/155650407-e86909a3-277f-4d72-97f9-3a4ec162935b.png)
constants를 선언하면 가르키고 있는 **포인터가 잠겨**있어 **값이 절대 변하지 않는다.**  
**보안**, **thread 보호**, **개발자 실수** 같은 이유로 왠만하면 값을 할당한 다음에 **다시는 변경되지 않는 데이터 타입을 사용**해야 한다.  
```
const dayInWeek = 7;
const maxNumber = 5;
```

## 4. Variable types
**primitive** (더이상 나눠지지 않는 단위들) **single item** - number, string, boolean, null, underiedn, symbol  
**object** (single item을 한군데 묶어서 관리) - box container  
**function** : first-class function (변수에 할당이 가능, 함수에 인자로도 전달가능, 리턴이 가능하다.)  

### data types for number
다른언어는 숫자를 입력할 때 데이터타입을 지정하고 사용하지만 자바스크립트에서는 **데이터타입을 선언하지 않아도 변수에 자동으로 할당**된다.  
```
const count = 17;
const size = 17.1;
console.log(`value: ${count}, type: ${typeof count}`);
console.log(`value: ${size}, type: ${typeof size}`);
```
![3](https://user-images.githubusercontent.com/73509513/155651371-09e55929-ef0d-4fe1-8c0d-8010c6e3cb9b.png)


### number의 특별한 값  
```
const infinity = 1 / 0;
const negativeInfinity = -1 / 0;
const nAn = 'not a number' / 2;
console.log(infinity);
console.log(negativeInfinity);
console.log(nAn);
```
![4](https://user-images.githubusercontent.com/73509513/155651403-2a2823aa-d08a-4d32-8894-59386a85f73c.png)

### string
자바스크립트에는 값의 길이에 상관없이 **string으로 취급**된다.  
선언할 값에 이미 선언한 **문자열을 붙이는 것도 가능**하다.  
```
const char = 'c';
const brendan = 'brendan';
const greeting = 'hello' + brendan;
console.log(`value: ${greeting}, type: ${typeof greeting}`);

const helloBob = 'hi ${brendan}!'; 
// template literals (string) : 원하는 값을 적고 ``와 ${}을 이용하면 변수에 값에 자동적으로 붙여서 나온다.

console.log('value: ' + helloBob + ', ' + 'type: ' + typeof helloBob);
console.log(`value: ${helloBob}, type: ${typeof helloBob}`);
// 기존의 + 기호를 사용하면 '' 안에 일일히 넣어서 표현해줘야 하지만 ``을 이용하면 간편하게 표현이 가능하다.
```
![5](https://user-images.githubusercontent.com/73509513/155651718-e87d355c-1664-44c1-8b38-4789207d29d9.png)

### boolean
**false** - 0, null, undefined, NaN, ''  
**true** - any other value(어떤 값이든 true)  
```
const canRead = true;
const test = 3 < 1; // false
console.log(`value ${canRead}, type: ${typeof canRead}`);
console.log(`value ${test}, type: ${typeof test}`);
```
![6](https://user-images.githubusercontent.com/73509513/155651909-11d024f3-bfb1-47ed-8d26-a1037338abb7.png)

### null
```
let nothing = null;
console.log(`value: ${nothing}, type: ${typeof nothing}`)
```
![10](https://user-images.githubusercontent.com/73509513/155651922-a7fc9d23-2f4a-4f47-a533-d3a09fad07f9.png)

### Undefined
선언은 되었지만 아무 값도 지정되어 있지 않은 것.  
```
let x;
console.log(`value: ${x}, type: ${typeof x}`);
```
![11](https://user-images.githubusercontent.com/73509513/155651944-fd2c040b-8691-4d52-860e-6bd8a180f072.png)

### symbol
**고유한 식별자가 필요**하거나 코드에 **우선순위**를 주고싶을때 사용한다.  
```
const symbol1 = Symbol('id');
const symbol2 = Symbol('id');
```

symbol 검사
심볼은 같은 값을 지정했어도 다른 심볼로 만들어지기 때문에 주어지는 값에 상관없이 고유한 식별자를 만들때 사용한다.  
```
console.log(symbol1 === symbol2); //false
```
![7](https://user-images.githubusercontent.com/73509513/155652069-54d4ef40-2b3a-461a-9a25-2540221929a7.png)

만약 값이 같은 심볼을 만들려면 **for**를 이용하면 된다.  
```
const gSymbol1 = Symbol.for('id');
const gSymbol2 = Symbol.for('id');
console.log(gSymbol1 === gSymbol2); //true
```
![12](https://user-images.githubusercontent.com/73509513/155652084-01befddd-05a3-4f19-a003-3c00ff3b014b.png)

심볼을 출력하려면 **description**을 사용해 string으로 변환 후 출력해야한다.  
```
console.log(`value: ${symbol1.description}, type: ${typeof symbol1}`);
```

### object
![14](https://user-images.githubusercontent.com/73509513/155650408-78702460-9a61-4840-b062-59b50a46389a.png)
const로 지정된 ellie는 **한번 할당된 object는 다른 object로 변경이 불가능**하지만
**object안에 있는 변수들은 변경이 가능**하다.
```
const ellie = { name: 'ellie', age: 20};
ellie.age = 21;
```

## 5. Dynamic typing : dynamically typed language
변수를 선언할 때 **어떤 타입인지 선언**하지 않으며 **프로그램이 시작될 때 타입이 변경**될 수 있다.  
```
let text = 'hello';
console.log(text.charAt(0)); // h 출력
console.log(`value: ${text}, type: ${typeof text}`); // type: string 지정

text = 1;
console.log(`value: ${text}, type: ${typeof text}`); // type: number로 변경

text = '7' + 5; //string인 7에 number인 5를 더하게 되면 5를 string으로 변환 하고 '75'로 합해지게 된다.
console.log(`value: ${text}, type: ${typeof text}`); // type: string로 변경

text = '8' / '2'; //string 끼리 나누게 되면 number로 변환하고 나누어지게 된다.
console.log(`value: ${text}, type: ${typeof text}`);
```
![8](https://user-images.githubusercontent.com/73509513/155652099-fca8f3e1-d4e4-42fc-b991-2de3f4667342.png)

```
console.log(text.charAt(0));
```
![9](https://user-images.githubusercontent.com/73509513/155652112-bc206f75-4b77-4b8f-9413-313025d6a198.png)

만약 개발자가 number타입으로 바뀐것을 모르고 string으로 착각하고 사용한다면 에러가 발생한다.
