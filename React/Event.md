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

## setState
