# Ajax

## 1. Ajax component 초기화

## json 파일

### list.json
```
[
    {"id":1, "title":"HTML"},
    {"id":2, "title":"CSS"},
    {"id":3, "title":"JS"}
]
```
### 1~3.json

```
// 1.json
{
    "id":"1",
    "title":"HTML",
    "desc":"HTML is ...."
} 

// 2.json
{
    "id":"2",
    "title":"CSS",
    "desc":"CSS is ..."
}

// 3.json
{
    "id":"3",
    "title":"JS",
    "desc":"JS is ..."
}
```

## Nav Component
```
class Nav extends Component{
  state = {
    list:[]
  }

  componentDidMount(){
    fetch('list.json')
      .then(function(result){
        return result.json();
      })
      .then(function(json){
        console.log(json);
        this.setState({list:json});
      }.bind(this));
  }
  
```
list.json을 fetch를 이용해 동기적으로 받아온다.

component가 생성될 때 Ajax call을 통해서 그 component를 초기화 해야할 경우에는  
componentDidMount라는 약속되어있는 메소드에 Ajax call을 넣고 Ajax를 통해 가져온 데이터로 render에 영향을 주는 것이 아닌  
state를 통해 render에 영향을 받도록해서 처리를 한다.  

componentDidMount은 컴포넌트가 만들어진 후 첫 렌더링을 다 마친 뒤 실행되는 메소드이다.  
componentDidMount에는 Ajax 처리, JavaScript 프레임워크 연동 등을 작성한다.

```
render(){
  var listTag = [];

  for(var i=0; i<this.state.list.length; i++){
    var li = this.state.list[i];
    listTag.push(<li><a href={li.id}>{li.title}</a></li>
  }
  return (
    <nav>
      <ul>
        <li><a href="1">HTML</a></li>
        <li><a href="1">HTML</a></li>
        <li><a href="1">HTML</a></li>
      </ul>
    </nav>
  );
}
```
동기적으로 받아온 list.json을 반복문을 사용해 listTag에 각각의 값을 넣어준다.  

### 출력

![1](https://user-images.githubusercontent.com/73509513/171100871-480f05dd-658e-40eb-af71-916d1366fe22.PNG)  

##  3. Ajax component 상태 변경

## Article Component
```
class Article extends Component{
  render(){
    return(
      <article>
      <h2>{this.props.title}</h2>
      {this.props.desc}
    </article>
    );
  }
}
```

## App Component
```
class App extends Component {
  state = {
    article:{title:'welcome', desc:'Hello, React & Ajax'}
  }
  render(){
    return (
      <div className="App">
        <h1>Web</h1>
        <Nav onClick={function(id){
          fetch(id+'.json')
            .then(function(result){
              return result.json();
            })
            .then(function(json){
              this.setState({
                article:{
                  title:json.title, 
                  desc:json.desc
                }
              })
            }.bind(this));
        }.bind(this)}></Nav>
        <Article title={this.state.article.title} desc={this.state.article.desc}></Article>
      </div>
    );
  }
}
```
Nav component의 클릭이 발생하면 nav component 내부의 onClick 함수의 호출이 일어나고, list의 id의 인자값이 전달되며,  
fetct()를 이용해 해당하는 id의 json을 받아오고, .then을 이용해 result.json()으로 parse(parsing)해준다.  

이후 then을 이용해 json을 받아 state의 상태의 title, desc를 각 json에 맞는 title, desc로 변경한다.

## Nav Component

```
  render(){
    var listTag = [];

    for(var i=0; i<this.state.list.length; i++){
      var li = this.state.list[i];

      listTag.push(
        <li key={li.id}>
          <a href={li.id} data-id={li.id} onClick={function(e){
            e.preventDefault();
            console.log('trigger');
            this.props.onClick(e.target.dataset.id);
          }.bind(this)}>
            {li.title}
        </a>
        </li>)
    }

    return(
      <nav>
        <ul>
          {listTag}
        </ul>
      </nav>
    );
  }
```
data-id={li.id}는 li의 id값을 받아오기 위함이여 this.props.onClick() 에서 e.target.dataset.id 경로에 있는 값을 가져오기 위한 데이터 속성이다.  

### HTML(1.json)
![2](https://user-images.githubusercontent.com/73509513/171100877-39dfe493-765f-4fcc-a45d-541f24bc7d82.PNG)  
### CSS(2.json)
![3](https://user-images.githubusercontent.com/73509513/171100879-acba4bb1-3dc2-4b65-a5f1-c3a4157cef68.PNG)  
### JS(3.json)
![4](https://user-images.githubusercontent.com/73509513/171100882-54f54ded-8e0c-4240-b2ca-132256ea6c28.PNG)  

## 4. 데이터 종속성 제거
```
class Nav extends Component {
  state = {
    list:[]
  }
  componentDidMount(){
    fetch('list.json')
      .then(function(result){
        return result.json();
      })
      .then(function(json){
        console.log(json);
        this.setState({list:json});
      }.bind(this));
  }
```
componentDidMount라는 메소드가 호출될 때 fetch api가 호출되며, ajax 기능까지 가지는 component가 되어있는데 이는 좋은 기능이기는 하나 재사용이 용이하지 않다.  

```
class App extends Component {
  state = {
    article:{title:'Welcome', desc:'Hello, React & Ajax'}
    article:{title:'Welcome', desc:'Hello, React & Ajax'},
    list:[]
  }
  componentDidMount(){
    fetch('list.json')
      .then(function(result){
        return result.json();
      })
      .then(function(json){
        console.log(json);
        this.setState({list:json});
      }.bind(this));
  }
```
App class에 componentDidMount 메소드를 옴겨주었으며, App 내부에서 setState를 통해 list의 값이 변경되므로 state에 list:[]로 초기화를 시켜준다.  

```
<Nav list={this.state.list} onClick={function(id){
    fetch(id+'.json')
        .then(function(result){
            return result.json();
        })
        .then(function(json){
            this.setState({
                article:{
                    title:json.title,
                    desc:json.desc
                }
        })
    }.bind(this));
}.bind(this)}></Nav>
```
App class의 Nav에 list라고 하는 props로 this.state.list의 값을 넘겨주었다.
```
class Nav extends Component {
...
render(){
    var listTag = [];
    for(var i=0; i<this.props.list.length; i++){
...
}
```
Nav class에서 갑을 수정하는 입장이 아닌 보내는 입장이 되었으므로 반복문 안의 this.state를 this.props로 변경하였다.

## 5. 로딩기능 구현
웹페이지가 Ajax를 서버와 통신할 때 지연시간이 있는데 이 때에 사용자들에게 로딩중이라고 알려주는 기능을 구현한다.

```
class App extends Component {
  state = {
    article:{
      item:{title:'Welcome', desc:'Hello, React & Ajax'},
      isLoading:false
    },
    
    list:{
      items:[],
      isLoading:false
    }
  }
```
로딩중이 아닐때는 isLoading:false, 로딩중일때는 isLoading:ture가 되게 초기화 해준다. isLoading을 추가했으므로 title과 desc를 담는 item, items를 만들어주었다.  

```
<Nav list={this.state.list.item} onClick={function(id){ ...
...
<Article title={this.state.article.item.title} desc={this.state.article.item.desc}></Article>
```
Nav component를 불러오는 코드에 `this.state.list`라고 되어있는 부분이 있는데 item, items를 추가했으므로 변경해준다.  
또한 아래에 있는 Article component를 불러오는 코드에 `title={this.state.article.title} desc={this.state.article.desc`부분을 변경해준다. 

```
componentDidMount(){
var newList = Object.assign({}, this.state.list, {isLoading:true}); //isLoading:true라는 복제본이 생성된다.
    this.setState({list:newList})
    fetch('list.json')
        .then(function(result){
            return result.json();
        })
        .then(function(json){
            console.log(json);
            this.setState({list:{
            items:json,
            isLoading:false
        }});
    }.bind(this));
}
```
newList라는 객체를 생성한 후 isLoading:true의 복제본을 생성하고 setState로 isLoading이 변경되게 해 로딩을 표현해준다.
componentDidMount 메소드에서 `this.setState({list:json});`에서 list:json을 지우고, list의 객체를 만든 후 items:json, isLoding:false를 추가해준다.  

```
.then(function(json){
    this.setState({
        article:{
        item:{
            title:json.title,
            desc:json.desc
            },
        isLoading:false
        }
    })
    }.bind(this));
}.bind(this)}></Nav>
```
Nav component를 불러오는 곳의 fetch가 실행되는 코드 안에 title과 desc를 item으로 감싸주고, isLoading:false를 추가해준다.  

```
class NowLoading extends Component{
  render(){
    return <div>Now Loading...</div>
  }
}
```
로딩이 되고있다는 것을 보여주기위한 component

```
var NavTag = null;
    if(this.state.list.isLoading){
      NavTag = <NowLoading></NowLoading>
    } else {
      NavTag = <Nav ...
      
...

var AriticleTag = null;
    if(this.state.article.isLoading){
      ArticleTag = <NowLoading></NowLoading>
    } else {
      ArticleTag = <Article ...
```
Nav, Article component가 로딩중일 때에는 NowLoading component를 렌더링하며, 로딩이 끝나면 각 component의 내용을 보여주는 코드.  

```
NavTag = <Nav list={this.state.list.items} onClick={function(id){
        var newArticle = Object.assign({}, this.state.article, {isLoading:true});
        this.setState({article:newArticle});
```
Nav component의 각 a태그를 눌렀을때 나오는 title과 desc의 로딩중을 표현하려면 Object.assign을 통해 isLoading:true 복사본을 만들어서 state의 값을 변경하게 해주면 된다. 

```
return (
    <div className="App">
        <h1>Web</h1>
        {NavTag}
        {ArticleTag}
    </div>
);
```
App class의 최하단에 위에서 만든 NavTag과 ArticleTag를 활성화한다.

## NowLoading...
### NavTag
![NowLoading](https://user-images.githubusercontent.com/73509513/171577288-0a2a194b-8b8f-4ab9-8087-8d08273b7207.PNG)

### ArticleTag
![NowLoading  2](https://user-images.githubusercontent.com/73509513/171577533-241df3ee-e9b9-4339-9c56-c75242e92f59.PNG)
