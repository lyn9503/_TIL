# 반응형 헤더 만들기

## 목표
![1](https://user-images.githubusercontent.com/73509513/154872954-6d490ebd-81fb-40d1-9c7b-80fedd29a015.png)

## 조건
1. 각 요소들을 flexBox로 만들어 상단에 배치  
2. flex 활용  
3. 스크린 사이즈가 768 이상 일때 행으로 배치 768 이하는 토글 버튼이 보여져야 하고 요소들이 열로 배치  

## 1. 헤더 기준 잡기

### css 연결

```
<link href="responsive1.css" rel="stylesheet" type="text/css" />
```

### 무료 이미지 사이트 스크립트 적용
![2](https://user-images.githubusercontent.com/73509513/154873440-08514630-2d20-4703-b0da-fa640fbd56ff.png)

위의 사이트를 이용해 로고와 아이콘 등을 가져왔다.
```
<script src="https://kit.fontawesome.com/ff268ec48f.js" 
        crossorigin="anonymous">
<script>
```

### 로고 메뉴 아이콘 공간 만들기

```
<nav class="navbar">
  <div class="navbar_logo">
    <i class="fa-brands fa-artstation"></i>
    <a href="">Test</a>
  </div>
```
nav, div태그 선언 후 css 적용을 위해 class 이름 할당 (navbar, navbar_logo)  
(i 태그는 fontawesome.com의 무료 소스를 이용)  
```
  <ul class="navbar_menu">
    <li><a href="">Home</a></li>
    <li><a href="">Galary</a></li>
    <li><a href="">Weddings</a></li>
    <li><a href="">FAQ</a></li>
    <li><a href="">Bookings</a></li>
</ul>
```
list 태그인 ul, li를 이용해 메뉴를 선언   
```
  <div class="navbar_icon">
    <i class="fa-brands fa-twitter-square"></i>
    <i class="fa-brands fa-facebook-square"></i>
  </div>
```
아이콘은 무료 소스를 이용해 적용  
```
    <a href="#" class="navbar_toogleBtn">
      <i class="fa-solid fa-bars"></i>
    </a>
</nav>
```
토글버튼 선언  

## 2. css 적용
```
body {
  margin: 0;
}
```
nav 태그 상하좌우 여백을 없애기 위해 margin을 0으로 설정  
```
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: rgba(25, 3, 77, 0.884);
  padding: 8px 12px;
}
```
반응형으로 만들기위해 flex로 선언하고, 각 요소들을 균등있게 배치하기 위해 space-between을 적용  
요소들이 가운데로 정렬되어야 하므로 align-items: center  
양 옆으로 붙어있어 이를 떼어내기 위해 padding 값을 넣어 배치  

```
a {
  text-decoration: none;
  color: white;
}
```
anchor 태그에는 기본적으로 밑줄과 색깔이 지정되어 있으므로 text-decoration을 이용해 없애주고  
색상을 white로 변경  

```
.navbar_logo {
  font-size: 1.5em;
  color: white;
}

.navbar_logo {
  color: bisaue;
}
```
로고의 크기와 색상 지정  
(부모의 크기가 기본적으로 16px이므로 1.5em을 이용하면 24px로 적용)  

```
.navbar_menu {
  display: flex;
  list-style: none;
  padding-left: 0;
}

.navbar_menu li {
  padding: 8px 12px;
}
```
메뉴 배치  
display를 flex로 선언해주고  
list 태그에는 '과 같은 스타일이 적용되어 있으므로 list-style을 none으로 선언  
메뉴에는 padding이 들어가있어 padding-left: 0;을 이용해 없애준다.  

각 list가 조금씩 떨어져 보여야 하므로 padding 값을 8px, 12px로 선언한다.  

```
.navbar_icon {
  display: flex;
  padding-right: 0;
}

.navbar_icon i {
  padding: 8px 12px;
  font-size: 1.5em;
}
```
아이콘 배치  
display를 flex로 선언  
메뉴와 같이 아이콘도 기본적으로 padding이 들어가 있으므로 제거  
무료 소스를 가져온 i태그가 붙어져 보이므로 padding값과 크기를 조절  

```
.navbar_toogleBtn {
  display: none;
  position: absolute;
  right: 32px;
  font-size: 1.5em;
  color: white;
}
```
토글 배치
토글 버튼은 화면이 작아질 때 보여져야 하므로 평소에는 보여지지 않게 display: none;으로 가려준다.  
position을 지정해주지 않으면 navbar_icon 다음에 배치되므로 position을 absoltue로 선언 해주면 맨 위로 이동한다.  
토글은 스크린의 사이즈가 적을 때 보여지는데 이를 오른쪽 상단에 배치해야 하므로 right를 32px를 주어 오른쪽 끝에 배치되도록 한다.  
이후 사이즈와 색상을 지정한다.  

## 3. @media 적용
```
@media screen and (max-width: 768px) {
  .navbar {
    flex-direction: column;
    align-items: flex-start;
  }
  .navbar_menu {
    flex-direction: column;
    align-items: center;
    width: 100%;
  }
  .navbar_icon {
    justify-content: center;
    width: 100%;
  }
  .navbar_toogleBtn {
    display: flex;
  }
}
```
768 이하(태블릿 사이즈) 스크린에서 표현되게 해줘야 하므로 @media를 이용해 적용한다.  
768 사이즈 이상에서는 열로 보여주지만 768 이하 사이즈에서는 행으로 보여져야 하므로  
navbar, menu를 flex-direction: column; 을 이용해 요소들이 행으로 처리될 수 있도록 한다.  
menu가 아래로 정렬되게 align-items: center;를 이용해 정렬해주며  
꽉 차게 보여야 하므로 width: 100%로 맞춰준다.  

위의 html에서 토글버튼이 none으로 보여지지 않게 했다. 사이즈가 768 이하로 작아지면 보여져야 하므로  
display: flex;를 선언해 보여지게 해준다.  

## 4. 완성
![3](https://user-images.githubusercontent.com/73509513/154875737-d2c24e8b-a0c7-4483-b283-30df313e29ad.png)
![4](https://user-images.githubusercontent.com/73509513/154875738-61390b03-919d-40d8-9f1f-b26cfc31e1fc.png)

## 추가
css에서 :root{ } 를 이용해 색상을 미리 선언하면 요구에 맞춰 지정이 편리해진다.  
```
:root {
  --text-color: white;
  --background-color: rgba(25, 3, 77, 0.884);
  --accent-color: bisque;
}
```
위 코드를 선언해 주고  
```
backgound: var(--background-color);
```
var를 이용해 지정해주면 된다.  

## 강의  
https://www.youtube.com/watch?v=X91jsJyZofw

## 참고한 사이트  
무료 소스 : https://fontawesome.com/  
