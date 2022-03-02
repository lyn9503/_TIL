# Class
 
class는 연관(관련)있는 데이터를 묶어놓는 컨테이너같은 것이다.  

```
class person{
    name;
    age;
    // field (속성)
    speak();
    // method (행동)
}
```

class는 데이터는 들어있지 않고 틀만 있으며, class를 이용해서 데이터를 넣어 만드는 것이 object이다.  
자바스크립트에서 class는 ES6에서 추가되었다.  

## 1. Class declarations
```
class Person {
    //constructor
    constructor(name, age){
        // fields
        this.name = name;
        this.age = age
    }

    // methods
    speak() {
        console.log(`${this.name}: hello!`);
    }
}
```
class를 이용해서 person이라는 클래스를 생성하고, constructor(생성자)를 이용해서 나중에 object를 만들 때 필요한 데이터를 전달한다.  
전달받은 데이터를 name과 age라는 fields에 할당한다.  

**object 생성**
```
const ellie = new Person('ellie', 20);
console.log(ellie.name);
console.log(ellie.age);
ellie.speak();
```
![1](https://user-images.githubusercontent.com/73509513/156286100-cb07fe69-c1f9-48bb-b26e-5c2071a2a743.PNG)

## 2. Getter and setters
```
class User {
    constructor(firstName, lastName, age) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.age = age;
    }
```

getter를 정의하는 순간 위의 this.age는 메모리에 있는 age의 값을 읽어오는 것이 아닌 아래의 getter를 호출한다.  
setter를 정의하는 순간 age의 값을 할당할때 메모리에 있는 age의 값을 할당하는 것이 아닌 setter의 값을 호출한다.  
![callstack 오류](https://user-images.githubusercontent.com/73509513/156287309-d68c78e5-5fd2-4807-a4b7-d0f69ad7a9ae.PNG)

이러한 작동방식으로 인해 setter로 돌아와서 setter의 값을 무한 호출하는 문제로 callstack 오류가 발생한다.  
    
```
    /**
    get age() {
        return this.age;
    }

    set age(value) {
        this.age = value;
    }
    **/
```
위의 문제를 해결하려면 getter와 setter 안에서 쓰이는 변수의 이름을 변경할 필요가 있다.  

```
    get age() {
        return this._age;
    }

    set age(value) {
      if (value < 0) {
          throw Error('나이의 값이 적습니다.');
      }
```
이렇게 나이의 값이 0 아래일 때 경고문을 띄우거나 아래처럼 value의 값이 - 라면 0을 띄우거나 지정된 value를 띄울 수 있다.  

```
        this._age = value < 0 ? 0 : value;
    }
}
```

```
const user1 = new User('Steve', 'Job', -1);
console.log(user1.age);
```
![2](https://user-images.githubusercontent.com/73509513/156286589-e11122f9-c7d0-437e-ae3d-9c02ffb665e0.PNG)

getter와 setter는 위처럼 사람의 나이가 -1인 이러한 문제를 방어적인 자세로 만들 수 있드록 해준다.  

## 3. Fields (public, private)
```
class Experiment {
    publicField = 2;
    #privateField = 0;
}
const experiment = new Experiment();
console.log(experiment.publicField);
console.log(experiment.privateField);
```
![3](https://user-images.githubusercontent.com/73509513/156286651-0335f70d-3ad1-4aad-829f-4a62ff6f92a7.PNG)

생성자를 만들지 않고 field를 작성하면 public 즉 외부에서 접근이 가능하며, # 기호를 붙이게 되면 private 즉 class 외부에서 접근이 불가능하다.  
위의 출력을 보면 publicField은 2라는 값이 표시되지만 privateField는 접근이 불가능해 undefined를 출력하게 된다.  
하지만 최근에 추가되어 지원하는 브라우저가 적다.  

## 4. Static properties and methods
```
class Article {
    static publisher = 'Dream Coding';
    constructor(articleNumber) {
        this.articleNumber = articleNumber;;
    }

    static printPublisher() {
        console.log(Article.publisher);
    }
}
```
class안에 있는 field와 method들은 새로운 object를 만들때마다 복제되어 값만 지정되어 만들어지는데  
간혹 object에 상관없이 class가 가지고있는 고유한 값과 동일하게 반복적으로 사용되는 method들이 있을 수 있다.  
이를 static을 사용해 작성하게 되면 메모리의 사용이 줄어들게 된다.    

## 5. Inheritance
공통적으로 사용되는 속성값을 재사용해 간편하고, 유지보수를 쉽게 해준다.  
```
class Shape {
    constructor(width, height, color) {
        this.width = width;
        this.height = height;
        this.color = color;
    }

    draw() {
        console.log(`drawing ${this.color} color of`);
    }

    getArea() {
        return this.width * this.height;
    }
}
```
상속은 필요한 함수만 바로 재정의해서 사용이 가능하다.  

```
class Rectangle extends Shape {
    draw(){
        super.draw();
        console.log('🟦');
    }
}
```
![4](https://user-images.githubusercontent.com/73509513/156286904-99b068ef-d5ef-493f-9df2-0e38b42c86a7.PNG)

함수를 재정의해서 console.log('🟦');를 출력할 수 있지만 Shape class의 draw() 함수의 console.log는 출력되지 않는다.  
만약 Shape의 draw를 출력하기 위해서는 super를 사용해 부모의 draw를 출력하게 할 수 있다.  

```
class Triangle extends Shape {
    getArea() {
        return (this.width * this.height) / 2;
    }
}
```
![5](https://user-images.githubusercontent.com/73509513/156286964-24dadd99-6499-482d-9768-ffeefd26921e.PNG)

삼각형은 높이와 넓이의 값에 2를 나눠줘야 표현되는데 Shape의 getArea()에는 width와 height만 곱해서 return한다.  
이는 getArea()를 width와 height의 값을 곱하고 2로 나눈 값을 다시 return 시키게 재정의하면 된다.  

```
const rectangle = new Rectangle(20, 20, 'blue');
rectangle.draw();
console.log(rectangle.getArea());
const triangle = new Triangle(20, 20, 'red');
triangle.draw();
console.log(triangle.getArea());
```
![10](https://user-images.githubusercontent.com/73509513/156287123-a61067ae-dcfb-44f4-bdb6-e572d503a465.PNG)

extends 키워드를 이용해서 class를 작성하면 위에 작성된 Shape의 속성값을 Rectangle이 상속받아진다.  

## 6. Class checking: instanceOf
**instanceOf는 작성된 object가 Class를 이용해 만들어진 것인지 아닌지 확인하는 것이다.**  

```
console.log(rectangle instanceof Rectangle);
```
true
```
console.log(triangle instanceof Rectangle);
```
false
```
console.log(triangle instanceof Triangle);
```
true
```
console.log(triangle instanceof Shape);
```
triangle은 Shape을 상속받았기에 true  
```
console.log(triangle instanceof Object);
```
자바스크립트에서 만든 모든 class나 object들은 자바스크립트의 object를 상속한것이다. true  

![7](https://user-images.githubusercontent.com/73509513/156287153-b89b5f55-9e91-4839-b72e-b723d1c86139.PNG)

![object 상속](https://user-images.githubusercontent.com/73509513/156287349-44fa1afa-79c6-486a-89fe-1beb5f01105e.PNG)

```
console.log(triangle.toString());
```

자바스크립트에서 object는 위 사진처럼 공통적으로 상속된 값을 사용할 수 있다.  

![8](https://user-images.githubusercontent.com/73509513/156287402-074a5a50-81bf-49ae-bba4-8ebb7f7fccdd.PNG)

하지만 위에서 toString을 작성하지 않아 object Object라는 의미없는 값이 출력된다.  

```
class Shape {
    constructor(width, height, color) {
        this.width = width;
        this.height = height;
        this.color = color;
    }

    draw() {
        console.log(`drawing ${this.color} color of`);
    }

    getArea() {
        return this.width * this.height;
    }

    toString() {
        return `Triangle: color: ${this.color}`
    }
}
```
![9](https://user-images.githubusercontent.com/73509513/156287647-3b8d3562-abb0-4731-821e-8e0426d3be3f.PNG)

이를 해결하려면 Shape class 안에 toString 함수를 작성하면 해결된다.  
