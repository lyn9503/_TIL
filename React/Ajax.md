# Ajax

## Ajax component 초기화

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

## Ajax component 상태 변경

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
