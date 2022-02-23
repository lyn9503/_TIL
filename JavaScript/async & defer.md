# js 파일을 읽어오는 여러가지 방법

## head에 사용하는 경우
```
<head>
    ···
    <script src="main.js"></script>
</head>
```  

![1](https://user-images.githubusercontent.com/73509513/155283352-7c872972-3b48-4313-b5a3-f835063d315d.png)

브라우저가 한줄 씩 읽어 DOM요소로 변환한다.  
스크립트에 도달하면 fetching js와 executing js를 서버에서 다운받고 parsing HTML로 넘어간다.  
하지만 큰 용량의 js파일을 script를 head안에 표현하면 매우 느려진다.  

## body에 사용하는 경우
```
<body>
    ···
    <script src="main.js"></script>
</body>
```  

![2](https://user-images.githubusercontent.com/73509513/155283359-b7427130-17ec-4590-8580-63b5fe7ca839.png)

다른 방법으로는 body에 사용하는 방법이 있는데 이는 사용자가 html파일을 빨리 볼 수 있게 된다.  
하지만 js에 너무 의존적인 웹 페이지일 경우 사용자가 정상적인 페이지를 보는 시간이 길어질 수 있다.  

## head + async를 사용하는 경우
```
<head>
    ···
    <script src async="main.js"></script>
</head>
```  

![5](https://user-images.githubusercontent.com/73509513/155283366-a306ddc1-fa59-409e-b77b-913eeb2541ba.png)

또 다른 방법으로는 head안에 사용하되 async(boolean 타입으로 기본적으로 true)을 사용하는 방법이다.  
async을 사용하게 되면 브라우저가 html을 다운로드 받고 parsing을 하다가 js를 만나면 병렬로 서버에서 다운받는 명령을 내리고,  
다운로드가 끝나면 다운받은 js를 실행한다.  
html을 parsing 하는 동안 병렬로 다운받게 되므로 정상적인 페이지를 보는 시간이 단축되는 효과가 있다.  
하지만 js가 html이 분석 되기도 전에 실행되기 때문에 DOM요소를 직접 건들이는 경우 문제가 발생할 수 있다.  

## head + defer를 사용하는 경우
```
<head>
    ···
    <script src defer="main.js"></script>
</head>
```  

![6](https://user-images.githubusercontent.com/73509513/155283374-f13d0b93-2729-4c0a-afd3-57371653d4df.png)

마지막으로 defer를 사용하는 경우도 있다.
이는 html를 parsing하는 도중 js를 만나면 서버에서 다운로드를 병렬로 시작하며 async과 같지만
defer는 html이 parsing되고 난 이후 페이지를 보여준 후 js를 실행하는것에 차이가 있다.

## async와 defer의 차이점
async는 다운로드 된 js부터 실행하기 때문에 js가 순서에 의존적인 경우 async을 사용하면 문제가 발생할 수 있다.
하지만 defer는 모두 다운로드 한 후 순서대로 js파일을 실행한다.
이런 경우로 head안에 defer옵션을 사용하는 것이 효율적이고 안전하다.  
  
  
### JavaScript가 뭔가요?
https://developer.mozilla.org/ko/docs/Learn/JavaScript/First_steps/What_is_JavaScript

### 강의
https://www.youtube.com/watch?v=tJieVCgGzhs&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=2
