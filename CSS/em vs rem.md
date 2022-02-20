# em 과 rem을 나누는 기준  
1. 부모요소 사이즈 % em  
2. 브라우저 사이즈 반응 v* rem  
3. 요소의 너비와 높이 % v*  
4. 폰트 사이즈 em rem  


# em 과 rem의 차이

## em
```
.level1 {
  font-size: 2em;
}

.level2 {
  font-size: 2em;
}

.level3 {
  font-size: 2em;
}

.level4 {
  font-size: 2em;
}
```
![em tree](https://user-images.githubusercontent.com/73509513/154838392-e07fb481-1b8d-48c4-a0e0-46b2d5efcccf.png)

em을 사용했을때 level의 폰트사이즈가 점차 커지지만 부모에 의해 2배씩 커지므로 em을 많이 사용하면 계산하기가 어려워진다.

## rem
```
.component {
  width: 50%;
  border: 1px solid burlywood;
  font-size: 2rem;
}
.level1 {
  font-size: 2rem;
}

.level2 {
  font-size: 2rem;
}

.level3 {
  font-size: 2rem;
}

.level4 {
  font-size: 2rem;
}
```
![rem tree](https://user-images.githubusercontent.com/73509513/154838433-1c81ed6c-74b2-4117-9a31-d1655f01b98b.png)

rem을 사용하면 em과 다르게 root에 의해 값이 결정되므로 계산하기가 쉽다.

## em 반응형
```
  <body>
    <h1>Hello, dream coders 🙌</h1>
  </body>
```
```
h1 {
  display: inline-block;
  font-size: 5em;
  background-color: mediumaquamarine;
  padding: 10px;
}
```
![padding size](https://user-images.githubusercontent.com/73509513/154838636-b7f95b05-6c77-42a9-aae1-bbd378ebe57c.png)

font-size는 5em을 사용해서 반응형으로 만들었지만 padding은 10px로 유지되어 브라우저에서 폰트 크기를 변경해도 폰트 사이즈에 비해 padding이 너무 크다.
```
h1 {
  display: inline-block;
  font-size: 5em;
  background-color: mediumaquamarine;
  padding: 1em;
}
```
브라우저에서 폰트 사이즈 변경시 padding의 크기도 변경되게 하려면 em을 사용하면 된다.
```
@media screen and (max-width: 780px) {
  h1 {
    font-size: 3em;
  }
}

@media screen and (max-width: 680px) {
  h1 {
    font-size: 1.5em;
  }
}
```
@media 쿼리를 이용하면 더 역동적인 반응형을 만들 수 있다.

## rem 반응형
```
  <body>
    <section class="component">
      <header class="title">Master Front-end ✨</header>
      <p class="contents">
        Lorem ipsum dolor sit amet consectetur, adipisicing elit. Sapiente
        veniam, nulla porro distinctio aliquid, quos quidem odio consectetur
        aperiam, delectus cum. Deserunt facilis excepturi similique natus minus
        deleniti rem sit?
      </p>
    </section>
  </body>
```

```
.component {
  width: 50%;
  border: 1px solid burlywood;
  font-size: 2rem;
}
```
폰트 사이즈에 의해 변화되므로 자연스러운 연출을 위해서는 %를 이용하는 것이 좋다.

```
.title {
  background-color: burlywood;
  padding: 0.5em;
}

.contents {
  font-size: 1rem;
  padding: 0.5em;
}
```
![rem ](https://user-images.githubusercontent.com/73509513/154838739-d4e0f985-b568-462d-b00a-f3a4136e956f.png)

padding을 em을 사용하면 title과 contents의 폰트사이즈가 달라 padding의 정렬이 잘 되지 않는다.
```
.title {
  background-color: burlywood;
  padding: 0.5em 0.5rem;
}

.contents {
  font-size: 1rem;
  padding: 0.5em 0.5rem;
}
```
![rem 2](https://user-images.githubusercontent.com/73509513/154838799-4085c596-9169-48d2-b9ae-f9d9d56a3a31.png)

위의 문제를 해결하려면 padding에 rem을 추가하면 폰트사이즈에 맞게 padding이 조절되어진다.

## 참고 코드
https://github.com/dream-ellie/css-responsive-units/tree/master/rem%20vs%20em%20demos
