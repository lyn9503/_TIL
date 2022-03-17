# 함수의 정의와 호출
```
const num1 = 1;
const num2 = 2;

function add(num1, num2) {
    return num1 + num2;
}

const sum = add(3, 4);

console.log(sum);
```
함수는 함수의 이름, 값을 받아오는 변수를 지정하고, { }의 코드블록(기능)을 정의할 수 있다.   
위 함수는 add라는 이름을 가진 함수로, num1과 num2를 더해 return하는 기능을 가지고 있다.  
sum에 3, 4란 값이 입력되면 함수를 호출하고 add의 num1, num2에 값이 저장되고, num1, num2의 더한 값 7을 return한 후 sum에 할당된다.  

# 함수를 다른 변수에 할당
```
function add(num1, num2) {
    return num1 + num2;
}

const doSomething = add;

const result = doSomething(2, 3);
console.log(result);
const result2 = add(2, 3);
console.log(result2);
```

doSomething이라는 변수의 공간이 할당되는데 이 공간에 add 함수의 주소가 할당되어진다.  
이로인해 doSomething과 add는 같은 함수의 주소를 가지고 있어 함수를 호출할 때 같은 값을 넣어도 동일하게 출력된다.  

```
function print() {
    console.log('print');
}
print(8, 33);
```

print 함수에 아무 인자를 넣지 않고 만든 뒤 함수를 호출할 때 ( )에 인자값을 적어도 출력되지 않는다.  
그러므로 함수를 만들 때 아무런 인자값을 사용하지(받지) 않으면 Input을 받지 않는다.  

# 함수를 다른 함수에 인자로 할당
```
function surprise(operator) {
    const result = operator(2, 3); // add(2, 3)
    console.log(result);
}

surprise(add);
```
surprise에는 operator에 add의 reference가 복사되어져 operator를 호출하는 것은 add를 수행하는 것과 동일하다.  

```
function divide(num1, num2) {
    return num1 / num2;
}


surprise(divide);
```
위 divide도 동일하게 operator에 reference가 복사되어 나누게 된다.
