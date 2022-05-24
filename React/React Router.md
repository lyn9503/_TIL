# React Router

## import
```
import {BrowserRouter, Route, Switch, Link} from 'react-router-dom';
```
사용할 react-router-dom의 component를 연결

## Component
```
function Home(){
  return (
    <div>
      <h2>
        Home
      </h2>
      Home...
    </div>
  )
}

function Topics(){
  return (
    <div>
      <h2>
        Topics
      </h2>
      Topics...
    </div>
  )
}

function Contact(){
  return (
    <div>
      <h2>
        Contact
      </h2>
      Contact...
    </div>
  )
}
```
Link 이동시 보여질 내용

## Link
```
<ul>
  <li>
    <Link to="/">
      Home
    </Link>
  </li>

  <li>
    <Link to="/topics">
      Topics
    </Link>
  </li>

  <li>
    <Link to="/contact">
      Contact
    </Link>
  </li>
</ul>
```
Link 코드

### a 태그, Link 태그
`<a>` 태그는 HTML에서 페이지를 재 렌더링해 이동하는 방법이며, 항상 새로운 데이터를 다시 불러오게 되어 가지고 있는 state 등이 사라진다는 단점이 있다.  
`<a href=" ">`를 사용해 경로를 지정한다.

`<link>`는 react-router-dom에서 제공하며, `<a>`태그와는 다르게 데이터는 유지되고,  
  변경되어야 하는 페이지만 재 렌더링 되어 불필요한 데이터를 불러오지 않는다는 장점이 있다.
`<link to=" ">`을 사용해 경로를 지정한다.
  
## Route
```
<Switch>
  <Route exact path="/">
    <Home/>
  </Route>

  <Route path="/topics">
    <Topics/>
  </Route>

  <Route path="/contact">
    <Contact/>
  </Route>

  <Route path="/">
    Not Found
  </Route>
</Switch>
```
각 component들의 경로(path) 설정

### exact
exact를 사용하지 않고 경로를 연결해주면 Home과 Topics(or Contact)가 충돌을 일으켜 함께 나오게 된다. 정확한 경로를 연결하기 위해 exact를 사용해야 한다.
  
### Switch
Switch는 경로가 일치하는 첫번째 component가 발견되면 나머지는 버린다.

## BrowserRouter
```
<BrowserRouter>
  <App />
</BrowserRouter>
```
## useParams
```
var contents = [
  {id:1, title:'HTML', description:'HTML is ...'},
  {id:2, title:'JS', description:'JS is ...'},
  {id:3, title:'React', description:'React is ...'},
]

function Topic(){
  var params = useParams();
  var topic_id = params.topic_id;
  var selected_topic = {
      title:'Sorry',
      description:'Not Found'    
  }
  for(var i=0; i<contents.length; i++){
      if(contents[i].id === Number(topic_id)){
          selected_topic = contents[i];
          break;
      }
  }
  return (
      <div>
          <h3>{selected_topic.title}</h3>
          {selected_topic.description}
      </div>
  );
}

function Topics(){
  var lis = [];
  for(var i=0; i<contents.length; i++){
      lis.push(
      <li key={contents[i].id}>
        <Link to={'/topics/'+ contents[i].id}>
          {contents[i].title}
        </Link>
      </li>)
  }

  return (
      <div>
          <h2>Topics</h2>
          <ul>
              {lis}
          </ul>
          <Routes>
            <Route exact path="/topics/:topic_id" element={<Topic />} />
          </Routes>
      </div>
  )
}
```
React에서 Router사용시 Parameter를 사용하고 싶을때 useParams를 사용한다.  
위 코드에서는 Topic에서 parameter를 지정해주며, lis라는 배열을 생성해 Topics의 content, description을 출력해주고, 각각의 contents도 출력한다.

## React-Router-Dom V6
```
<Router>
  <div>
    <h1>Hello Router</h1>
     <ul>
       <li><Link to="/">Home</Link></li>
       <li><Link to="/topics">Topics</Link></li>
       <li><Link to="/contact">Contact</Link></li>
     </ul>
    <Routes>
      <Route path="/" element={<Home />}></Route>
      <Route path='/topics/*' element={<Topics />}></Route>
      <Route path="/contact" element={<Contact />}></Route>
    </Routes>
  </div>
</Router>
```
이전 버전에서는 Switch와 Route만 사용해주고 뒤에 component를 넣으면 됐지만,  
V6 버전부터는 최상위 태그 위에 Router로 감싸주어야 하며, Route사용시 element를 사용해서 component를 연결해주어야 한다.
