# Evnet
Event는 애플리케이션을 역동적으로 만들어주는 것이다.  
Event는 state, props와 상호작용한다.  

## State
현재 보고있는 페이지가 welcome 페이지인지, read 페이지인지 알 수 없으므로 추가해야한다.
```
// state
mode: 'welcome',
subject:{title:'WEB', sub:'world wide web!'},
welcome:{title:'welcome', desc:'Hello, React!!'},
```
현재 페이지(mode)가 welcome페이지 일때 subject와 welcome를 표시한다.  

react에서는 만약 props나 state의 값이 바뀌면 render 함수를 다시 호출되며, 호출될 때 마다 render안의 하위 component들의 render들도 바뀌면서 화면을 표시하게 된다.  
render는 어떤 HTML을 그릴것인가 하는것을 결정하는 함수이다.

```
// render
var _title, _desc = null;

if(this.state.mode === 'welcome'){
  _title = this.state.welcome.title;
  _desc = this.state.welcome.desc;
} else if(this.state.mode === 'read'){
  _title = this.state.contents[0].title;
  _desc =this.state.contents[0].desc;
}
```
mode가 welcome일때 welcome title, desc를, read일때 contents의 title과 desc를 화면에 표시한다.

## Event
```
<header>
  <h1><a href="/" onClick={function(e){
    e.preventDefault();
    // this.state.mode = 'welcome';
    this.setState({
      mode:'welcome'
    })
  }.bind(this)}>{this.state.subject.title}</a></h1>
  {this.state.subject.sub}
</header>
```
### mode = read

![read](https://user-images.githubusercontent.com/73509513/167768220-152f11ae-0484-4c70-859c-06b0a3ba34b6.PNG)

### mode = welcome

![welcome](https://user-images.githubusercontent.com/73509513/167768224-af62607c-ba32-423d-b874-1aa909bf587f.PNG)  

WEB의 링크를 클릭했을때 mode가 welcome으로 바뀐다.  
이때 this.state.mode = 'welcome';를 적게되면 동작하지 않는데 this가 어떤 component를 가르키는지 모르므로,  
이를 해결하기 위해 함수가 끝난 직후에 bind를 사용해주면 되며, 또한 setState를 사용해야 정상적으로 mode가 welcome으로 변경되게 된다.  
e.preventDefault();는 event의 기본적인 동작을 못하게 막는것이다.  

## bind
bind는 render함수가 호출될 때 함수 안에서 this는 그 component 자신을 가르킨다.  

## setState
state는 component의 생성이 끝난 다음 동적으로 state값을 바꿀때는 setState 함수를 사용해 갑을 변경해야한다.  
그 이유는 react에서 ''this.state.mode = 'welcome' '' 이런 식으로 값을 바꾸게되면 내부에서 값이 변경되었는지 모르기 때문에 값이 변경되지 않는다.

# Component Event 추가
## Subject Evnet

### App.js
```
<Subject
  title={this.state.subject.title}
  sub={this.state.subject.sub}
  onChangePage={function(){
    this.setState({mode:'welcome'});
  }.bind(this)}
>
</Subject>
```
onChangePage를 추가해 setState를 이용해서 mode를 welcome으로 변경한다.
onChangePage는 onChangePage라는 evnet가 있어서 subject component 내의 링크를 클릭했을때 event내의 함수를 호출한다.

### Subject.js
```
<header>
  <h1><a herf="/" onClick={function(e){
    e.preventDefault();
    this.props.onChangePage();
   }.bind(this)}>{this.props.title}</a></h1>
   {this.props.sub}
</header>
```
props를 이용해 App.js의 onChangePage 함수를 호출한다.

![welcome](https://user-images.githubusercontent.com/73509513/168203957-6fc5f069-1b20-46e8-be04-1a830c74a8ed.PNG)

## TOC Event
각각의 링크(HTML, CSS, JavaScript)를 클릭했을 때 아래에 내용이 표시되게 변경

### App.js
```
if(this.state.mode === 'welcome'){
  _title = this.state.welcome.title;
  _desc = this.state.welcome.desc;
} else if(this.state.mode === 'read'){
  var i = 0;
  while(i < this.state.contents.length){
    var data = this.state.contents[i];
    if(data.id === this.state.selected_content_id) {
      _title = data.title;
      _desc = data.desc;
      break;
    }
    i = i + 1;
  }
}

...

<TOC
  onChangePage={function(id){
    this.setState({
      mode:'read', 
      selected_content_id:Number(id)
    });
  }.bind(this)}

  data={this.state.contents}>
<TOC>
```
mode가 read일 경우 while을 이용해 현재 순번에 맞는 contents의 id를 data에 넣는다.  
만약 data의 id값과 state의 selected_content_id의 값이 일치하는 경우  
title과 desc의 값을 표시하게 된다.  

각각의 링크가 onChangePage의 evnet가 발생했을 때 setState를 통해서  
mode의 값과 함께 selected_content_id의 값을 content의 값에 맞게 변경된다.

주의해야 할 점은 state 변경시 selected_content_id:id 라고 적을 경우 값이 전달은 하지만 문자열이 전달되어 아무것도 표시되지 않는다.  
이를 해결하기 위해 이를 강제로 숫자로 바꿔주는 명령어인 Number 함수를 이용해 id를 감싸주게 되면 숫자로 변경되어 정상적으로 표시가 된다.

### TOC.js
```
<a 
  href={"/content/"+data[i].id}
  data-id = {data[i].id}
  onClick={function(e){
    e.preventDefault();
    this.props.onChangePage(e.target.dataset.id);
  }.bind(this)}
  >{data[i].title}
</a>
```
debbuger를 해보면 e가 가지고있는 값을 볼 수 있는데  
e.target은 event가 가지고 있는 태그인 a태그를 가르키며 data-id = {data[i].id}에 접촉하고 있다.
data-id의 - 는 dataset이라고 하는걸 통해서 접근하는데 dataset에 들어있는 id의 값은 {data[i].id}가 가지고 있다.
그러므로 onChangePage의 함수를 호출할때 위에서 알아낸 e.target.dataset.id을 인자로 넣어주면 component로 id의 값이 넘어가게 된다.

### id = 1 (HTML)
![1](https://user-images.githubusercontent.com/73509513/168203951-4b36aa44-7df1-42a7-a051-11e8108dc363.PNG)

### id = 2 (CSS)
![2](https://user-images.githubusercontent.com/73509513/168203954-16c37656-1904-4bd7-8fa4-3a2ce2048f61.PNG)

### id = 3 (JavaScript)
![3](https://user-images.githubusercontent.com/73509513/168203956-2107b40c-12a1-4f03-a95a-05226c19288e.PNG)
