# State
State는 props와 같이 살펴봐야하는데 props와 state는 javascript 객체이며,  
props는 component에 전달되는 반면 state는 component안에서(내부적으로) 관리된다.  
주로 상위 component에서는 state라는 내부정보를 사용하고, 하위 component에 값을 전달할 때는 props를 사용한다.

## State 생성
render가 실행되기 전 constructor 함수를 통해 먼저 초기화를 해주며, 초기화 이후 state를 작성해야 한다.

```
constructor(props) {
  super(props);
  this.state = {
    subject:{title:'WEB', sub:'world wide web!'}
  }
}
```
## State 사용
render 함수내에 있는 component에 위에서 작성한 state를 불러오면 된다.  
상위 component의 state 값을 하위 component에서 props의 값으로 전달하는 것이다.

```
<Subject
  title={this.state.subject.title}
  sub={this.state.subject.sub}>
</Subject>
```

## State에 여러개의 값을 입력하는 경우
TOC.js파일을 열어서 변경하는 것은 매우 번거로운 일이므로 contents라는 state를 만들고, TOC 내부의 데이터를 변경하게 하는것이 좋다.
```
contents:[
  {id:1, title:'HTML', desc:'HTML is HyperText Markup Languege.'},
  {id:2, title:'CSS', desc:'CSS is for design.'},
  {id:3, title:'JavaScript', desc:'JavaScript is for interactive.'}
]
```
contents는 값(title)이 여러개이므로 배열을 이용해 작성해주면 된다.  

```
var lists = []; // 생성하게 될 내용들을 담을 배열 생성
var data = this.props.data; // App.js에서 TOC가 받는 값
var i = 0;
while(i < data.length){
  lists.push(// 반복문이 돌아갈 때 마다 lists에 값 전달
    <li>
      <a href={"/content/"+data[i]}>{data[i].title}</a>
    </li>); // data의 길이만큼 TOC 내용을 생성
    i = i + 1;
}
```
TOC는 내부적으로 ``this.props.data``란 값을 받고있다.  
반복문을 사용해 TOC의 내용을 생성하게 해준다.  

![1](https://user-images.githubusercontent.com/73509513/167767712-e3282b3e-13e7-456e-82d9-8add0888caf8.PNG)

여러개의 element들을 전달하게 되면 브라우저의 console창에 오류가 발생한다.  
이는 각각의 list의 항목들은 key라는 props를 가져야 하는데 없어서 발생하는 오류이다.  

이러한 오류는 li 태그에 식별자를 지정해주면 된다.  
```
<li key={data[i].id}>
```

위 오류는 우리가 만드는 애플리케이션에서 사용하는 것이 아닌 react가 내부적으로 필요에 의해 요청하는 것이다.  
