# Array
[1. Declaration (배열 선언)](#1-declaration-%EB%B0%B0%EC%97%B4-%EC%84%A0%EC%96%B8)  
[2. Index position (배열 접근)](#2-index-position-%EB%B0%B0%EC%97%B4-%EC%A0%91%EA%B7%BC)  
[3. Looping over an array](#3-looping-over-an-array)  
[4. Addtion, deletion, copy (삽입, 삭제, 복사)](#4-addtion-deletion-copy-%EC%82%BD%EC%9E%85-%EC%82%AD%EC%A0%9C-%EB%B3%B5%EC%82%AC)  
[5. Searching (검색)](#5-searching-%EA%B2%80%EC%83%89)  

## Array란?
**배열은 자료구조의 한가지이며, Index를 기준으로 데이터가 저장되어진다.**

## 1. Declaration (배열 선언)
```
const arr1 = new Array();
const arr2 = [1, 2];
```
배열은 new 키워드로 만들 수 있는 방법과 [ ]로 만들 수 있는 방법 두가지가 있다.

## 2. Index position (배열 접근)
```
const fruits = ['🍎', '🍌'];
console.log(fruits);
console.log(fruits.length);
console.log(fruits[0]);
console.log(fruits[1]);
console.log(fruits[2]);
console.log(fruits[fruits.length - 1]);
```
첫번째 사과에 접근하려면 [ ]를 이용해 Index 번호를 적어 접근, 출력되게 된다. 
배열의 Index 범위 이후에 있는 번호를 출력하면 undefined가 출력되게 된다.  
첫번째 데이터를 찾을때에는 [0]을 많이 이용하고, 마지막 데이터를 찾을 때에는 배열의 길이에 -1 을 해서 찾는다.  
길이에 -1을 하는 이유는 배열이 0부터 시작하기 때문에 총 길이의 -1을 하면 마지막 Index를 찾기 때문이다.  

## 3. Looping over an array

### for
```
for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}
```
i가 0부터 fruits의 길이(2)까지 반복하면서 출력  

### for of
```
for (let fruit of fruits) {
  console.log(fruit);
}
```
fruits의 데이터를 순차적으로 할당하면서 { }을 실행해 출력하게 된다.  

### forEach
```
fruit.forEach(function (fruit, index, array) {
    console.log(fruit, index, array);
});
```
```
fruits.forEach((fruit) => console.log(fruit));
```
forEach는 callback 함수를 받아오는데 이는 배열의 각 요소에 대해 정의된 콜백 함수를 호출하고 결과가 포함된 배열을 반환한다.  
forEach의 함수에서는 보통적으로 array는 받아오지 않는다.  

## 4. Addtion, deletion, copy (삽입, 삭제, 복사)
### push
배열의 맨 뒤에 추가
```
fruits.push('🍓', '🍑');
console.log(fruits);
```
### pop
배열의 맨 뒤부터 지우기
```
const poped = fruits.pop();
fruits.pop();
console.log(fruits);
```
만약 하나 더 지우려면 fruits.pop();을 한번 더 사용하면 된다.  

### unshift
배열의 맨 앞에 추가
```
fruits.unshift('🍓', '🍋');
console.log(fruits);
```

### shift
배열의 맨 앞부터 지우기
```
fruits.shift();
fruits.shift();
console.log(fruits);
```

shift, unshift은 pop과 push보다 느리다.  
이는 데이터를 한칸씩 앞, 뒤로 옮긴 후 빈공간에 데이터를 집어넣거나 삭제하는 것을 반복하기 떄문이다.  
그래서 pop과 push를 사용하는 것이 더 좋은 방식이다.  

### splice
데이터를 지정된 위치에서 지우는 방식
```
splice(start: number, deleteCount?: number ...items: T[]);
```
deleteCount는 원하는 갯수를 적지않아도 되지만 적지 않으면 시작하는 데이터부터 전부 삭제된다.  
또한 뒤에 데이터를 입력하면 지워진 위치부터 추가된다.  
```
fruits.push('🍓', '🍑', '🍋');
console.log(fruits);
fruits.splice(1, 1);
console.log(fruits);
fruits.splice(1, 0, '🍏', '🍉');
console.log(fruits);
```
### concat
두가지의 배열을 묶어서 만들기
```
const fruits2 = ['🍐', '🥥'];
const newFruits = fruits.concat(fruits2);
console.log(newFruits);
```
새로 묶여진 배열을 리턴해 기존의 데이터에 새로운 데이터를 뒤에 추가한다.  

## 5. Searching (검색)
### indexOf
Index 검색
```
console.log(fruits);
console.log(fruits.indexOf('🍎'));
console.log(fruits.indexOf('🍉'));
console.log(fruits.indexOf('🥥'));
```
### includes
배열에 데이터가 있는지 없는지 즉 true, false로 리턴
```
console.log(fruits.includes('🍉'));
console.log(fruits.includes('🥥'));
```
### lastIndexOf
마지막 Index 검색
```
fruits.push('🍎');
console.log(fruits);
console.log(fruits.indexOf('🍎'));
console.log(fruits.lastIndexOf('🍎'));
```
똑같은 데이터가 하나 더 존재할경우 indexOf를 사용하면 같은 데이터중 Index의 우선순위가 높은 데이터를 검색하고  
lastIndexOf는 Index의 우선순위가 낮은 즉 마지막을 검색한다.  
