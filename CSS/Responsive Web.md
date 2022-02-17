# Responsive web(반응형 웹) 선언
```
@media screen and (min-width: 800px) {
 .container {
    width: 50%;
 }
}
```
스크린의 최소 넓이가 800px이면 컨테이너가 50% 차지하도록 선언

screen과 and의 속성

screen - speech, print, all  
and - not, only, ,(comma)

---

# CSS Units Responsive  
 Unit은 요소의 크기나 사이즈를 결정하는 것  
 Unit은 Absolute와 Relative의 카테고리로 나눠진다.  

## Absolute(절대적)  
 Absolute는 많은 unit이 있지만 px을 주로 사용한다.  
 하지만 반응형에서는 px는 고정되어 보여지므로 px보다는 %를 이용한다.  

## Relative(상대적)
 Relative은 em, rem, vw, vh, %를 주로 사용한다.  

## em
em은 타이포그래피에서 현재의 지정된 포인트 사이즈를 나타내는 단위, 즉 폰트 사이즈를 나타내는 단위이며, 부모의 폰트 사이즈의 상대적으로 크기가 계산된다.  

```
.parent {
  font-size: 8em;
}

.child{
  font-size: 0.5em;
}
```

HTML에선 기본적으로 폰트사이즈가 16px이므로 만약 부모가 8em을 가지면 16px x 8 즉 128px를 가진다.  
자식은 0.5em을 가지므로 부모의 사이즈의 절반의 사이즈를 가진다. (128 * 0.5 = 64px)
	
## rem

rem의 r은 root를 가르키며 em과 다르게 부모에 의해 사이즈가 조절되는 것이 아니라 root에 의해 폰트의 사이즈가 결정된다.

```
html {
  font-size: 100%;
}

.parent {
  font-size: 8rem;
}

.child {
  font-size: 0.5rem;
}
```

위의 코드에서 parent는 root 요소인 HTML에서 기본적으로 지정된 16px의 8배가 곱해진 128px로 계산되며
child는 16px의 0.5배가 곱해진 8px이 계산된다.
만약 html의 폰트사이즈가 100%가 아닌 px로 고정하게 되면 웹브라우저의 폰트 사이즈 조절에 영향을 받지 않는다.

## vw

vw는 만약 100vw라고 선언하면 브라우저 너비에 있는 100%를 쓰겠다 라고 하는 것이며
50vw라고 선언하면 브라우저의 너비에 반을 쓰겠다고 지정하는 것이다.


## vh

50vmin은 브라우저의 너비와 높이 중에 작은 값의 50%를 사용하며, 50vmax는 너비가 높이보다 크다면 넓이의 50%값이 계산된다. 


## %

부모 요소의 상대적으로 크기가 지정된다.
