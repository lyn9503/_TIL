# Object

## 1. Literals and properties
```
const name = 'ellie';
const age = 4;
print(name, age);
function print(name, age) {
    console.log(name);
    console.log(age);
}
```

premitive 타입은 변수 하나당 하나의 값만 담을 수 있다. 변수를 출력하려면 이름과 나이를 각각 parameter로 전달해 주어야한다.  
또 함수 작성시에도 두가지의 parameter를 가져올 수 있도록 작성해야하는데 이렇게 작성하면 추가해야할 인자들이 많아지므로 관리하기 힘들어지고 그룹으로 묶기도 힘들다.  
object는 key와 value라는 property의 집합체이다.  

### object를 만드는 방법
```
const obj1 = {}; //{}
const obj2 = new Object(); // class
```
{}로 만드는 방법, class를 이용해서 만드는 방법 두가지가 있다.  
{}로 만드는 방법은 **object literal**이라고 하며 class를 이용해서 만드는 방법은 **object constructor**라고 불린다.  
```
const ellie = { name: 'ellie', age: 4 };

function print(person) {
    console.log(person.name);
    console.log(person.name);
}

print(ellie);
```
이렇게 object로 작성하게 되면 간편하게 데이터를 관리할 수 있게 된다.  

```
ellie.hasJob = true;
console.log(ellie.hasJob);
delete ellie.hasJob;
console.log(ellie.hasJob);
```
자바스크립트는 동적으로 타입이 런타임때 결정되는데 이러한 특성으로 뒤늦게 하나의 property를 추가할 수 있지만 유지보수 측면에선 좋은 방법이 아니므로 되도록 피해햐한다.  

## 2. Computed properties
```
console.log(ellie.name);
console.log(ellie['name']);
```
자바스크립트에서 object는 .과 [ ] 두가지로 접근이 가능하다.  
주의해야 할 점은 [ ](Computed properties)을 사용할 시 무조건 ' '(string)타입으로 지정해 접근해야 한다.  
.는 정확히 그 key에 해당하는 값을 받아올 때 사용하며  
[ ]는 정확히 어떤키가 필요할지 모를때 런타임에서 결정될 때, 실시간으로 원하는 key 값을 받아올 때 사용한다.  
```
ellie['hasJob'] = true;
console.log(ellie.hasJob);
```
Computed properties는 위처럼 delete로 지운 object를 다시 살려 볼 수 있다.
```
function printValue(obj, key) {
    console.log(obj.key);
}
printValue(ellie, 'name');
```
위의 함수에서 key가 사용자에게 입력받아서 출력해야할때 개발자 시점에서는 key의 값이 무엇인지 모른다.  
그래서 위와같이 console.log(obj.key);로 작성하게 되면 undefined라고 출력하게 된다.  
```
function printValue(obj, key) {
    console.log(obj[key]);
}
printValue(ellie, 'name');
```
이처럼 key의 값을 모를경우 [ ]을 사용하면 정상적으로 출력이 되는 것을 알 수 있다.

## 3. Property value shorthand
```
const person1 = {name: 'bob', age: 2};
const person2 = {name: 'steve', age: 3};
const person3 = {name: 'dave', age: 4};
```
위와같이 여러개의 object를 만들때 일일히 동일한 이름과 나이 즉 key와 value를 작성해야하는 문제점이 있다.
```
const person4 = makePerson('ellie', 30);

function makePerson(name, age) {
    return {
        name,
        age,
    };
}
console.log(person4);
```
위처럼 class가 없던 시절에 함수를 통해 값을 입력하는 방식을 사용했다.  

## 4. Constructor function
```
const person5 = new Person('ellie', 40);

function Person(name, age) {
    this.name = name;
    this.age = age;
}
```
위 처럼 class를 사용해 작성하면 자바스크립트 엔진이 알아서 오브젝트를 생성해 준다.  
함수에서 생략된 것은 this = {};에 property를 넣는 것과 return this;이다.  

## 5. in operator
in operator는 해당하는 object안에 key의 유무를 확인하는 것이다.   
```
console.log('name' in ellie);
console.log('age' in ellie);
console.log('random' in ellie);
console.log(ellie.random);
```
object안에 키가 맞다면 true, 맞지 않으면 false, 정의하지 않은 key라면 undefined를 출력한다.  

## 6. for..in vs for..of
### for (key in obj)
```
console.clear();
// 이전 출력내용 삭제
for (key in ellie) {
    console.log(key);
}
```

for in은 object가 가지고있는 key의 값이 { }을 돌때마다 key라는 지역변수에 할당된다.  
{ }안의 console.log(key);를 출력하게 되면 ellie안의 값이 출력된다.  
이는 key의 모든 값을 받아 처리하고 싶을 때 사용되어진다.  

### for (value of iterable)
for of는 object를 쓰는것이 아닌 array(배열)과 같은 array list를 사용한다.  
```
const array = [1, 2, 4, 5];
for (let i = 0; i < array.length; i++) {
    console.log(array[i]);
}
```
위처럼 for문을 사용해 array의 길이만큼 돌려 출력할 수 있지만 많이 작성해야 하므로 좋지않다.  

```
for(value of array) {
    console.log(value);
}
```
for of를 사용해 array의 값이 value에 할당되면서 순차적으로 출력되거나 계산할 수 있다.  
for문을 사용하는 것에 비해 매우 간결해진다.  

## 7. Fun Cloning
```
const user = {name: 'ellie', age: '20'};
const user2 = user;
user2.name = 'coder';
console.log(user);
```
user가 가르키고 있는 name의 값을 coder로 변경

### 과거에 사용된 object 복사
```
const user3 = {};
for (key in user) {
    user3[key] = user[key];
}
console.clear();
console.log(user3);
```
// 과거에는 빈 object를 생성 후 for in을 이용해 수동적으로 할당해 주는 방법을 사용했다.

### assign
**Object.assign(target, source);**
assign은 복사를 하려는 target과, 복사할 source를 같이 전달해야하며 return값은 target과 source가 통합되어 return한다.  
```
const user4 = {};
Object.assign(user4, user);
console.log(user4);
```
빈 user4에 user의 값이 전달, 복사되어 출력되게 된다.  
```
const user5 = Object.assign({}, user);
console.log(user5);
```
위처럼 작성해도 된다.  

### assign example
```
const fruit1 = {color: 'red'};
const fruit2 = {color: 'blue', size: 'big'};
const mixed = Object.assign({}, fruit1, fruit2);
console.log(mixed.color);
console.log(mixed.size);
```
위 코드처럼 2개의 복사할 값이있다면 뒤에 나오는 object의 property가 덮어 씌워져 fruit2의 내용이 출력된다.  
만약 fruit3, fruit4가 있다면 fruit4가 덮여 씌워져 출력된다.  
