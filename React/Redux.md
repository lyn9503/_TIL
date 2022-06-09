# Redux
## Redux란?
React에서 State를 더 효율적으로 관리하는 라이브러리이며, Redux는 State의 관리를 Component 외부에서 처리하는 것이다.
Redux를 사용하게 되면 store라는 내부에 State를 담게 된다.

## Redux 용어

### Action
State의 변화를 일으킬 때 참조하는 객체이며, Event와 같다.  
Dispatch를 사용할 때 Reduce로 넘길 type을 정의하며, 실행이 끝나면 type을 반환하고 Reduce로 전달된다.  

### Store
애플리케이션의 State의 값들을 내장하고 있으며, Reduce에 의해서만 State의 값이 변경된다.

### Reducer
State를 변화시키는 로직이 있는 함수이며, Reducer에서 State를 사용할 경우 반드시 State를 초기화 해야 한다.
만약 값을 갱신할 경우 반드시 Reducer에서 해야한다.

### Dispatch
Action(Event)를 Store에 전달하는 것을 의미한다.

### Subscribe
Store의 값이 필요한 Component는 Store를 Subscribe(구독)한다.  
Component에서 Store를 구독하는 작업은 후에 Redux의 connect 함수가 대신 한다.  
Redux의 내장 함수를 사용하여 subscribe, unsubscribe 함수를 사용하여 구독 및 구독 취소를 할 수 있다.  

# React만 작성

## App.js
```
import AddNumberRoot from './Components/AddNumberRoot';
import DisplayNumberRoot from './Components/DisplayNumberRoot';

class  App extends Component {
  state = {number: 0}

  render(){
    return (
      <div className="App">
        <h1>Root</h1>
        <AddNumberRoot onClick={function(size){
          this.setState({number:this.state.number + size});
        }.bind(this)}></AddNumberRoot>
        <DisplayNumberRoot number={this.state.number}></DisplayNumberRoot>
      </div>
    );
  }
}
```
AddNumberRoot와 DisplayNumberRoot을 처리하는 js파일  

AddNumberRoot에서 전달된 size의 값을 setState를 통해 state의 number가 업데이트 된다.  
이후 DisplayNumberRoot의 number의 값의 state를 업데이트 해준다.

## Components
### AddNumber.jsx
```
export default class AddNumber extends Component {
    state = {size:1}
    render() {
      return(
        <div>
          <h1>Add Number</h1>

          <input type="button" value="+" onClick={function(){
              this.props.onClick(this.state.size);
          }.bind(this)}></input>

          <input type="text" value={this.state.size} onChange={function(e){
              this.setState({size:Number(e.target.value)});
          }.bind(this)}></input>
        </div> 
      )
    }
}
```
inpot의 값을 설정하고, + 버튼을 누르면 그 값의 state를 업데이트 한다.  

### AddNumberRoot.jsx
```
export default class AddNumberRoot extends Component{
  render(){
    return (
      <div>
        <h1>Add Number Root</h1>
        <AddNumber onClick={function(size){
            this.props.onClick(size);
        }.bind(this)}></AddNumber>
      </div>
    )
  }
}
```
AddNumber의 + 버튼이 눌러지면 input의 값(size)이 Root(App.js)로 전달된다.  

### DisplayNumberRoot.jsx
```
export default class DisplayNumberRoot extends Component {
  render() {
    return(
      <div>
        <h1>Display Number Root</h1>
        <DisplayNumber number={this.props.number}></DisplayNumber>
      </div> 
    )
  }
}
```
Root에서 업데이트된 number의 값을 DisplayNumber로 전달시킨다.  

### DisplayNumber.jsx
```
export default class DisplayNumber extends Component {
    render() {
      return(
        <div>
          <h1>Display Number</h1>
          <input type="text" value={this.props.number} readOnly></input>
        </div> 
      )
    }
}
```
DisplayNumberRoot에서 받은 number 값을 표시해준다. 값은 건들 수 없게 readOnly로 설정한다.  

![5](https://user-images.githubusercontent.com/73509513/172285675-80988daf-1237-4d4b-a249-e51b7a589c06.PNG)


# Redux 도입
## store.js
```
import {createStore} from 'redux';
export default createStore(function(state, action) {
    if(state === undefined){
        return {number:0}
    }
    if(action.type === 'INCREMENT'){
        return {...state, number:state.number + action.size}
    }
    return state;
}, window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__())
```
createStore는 state와 action을 정의하고 state가 undefined일 경우 number의 값을 0으로,  
action.type이 INCREMENT일경우 state의 number값과 action의 size를 더하고 return한다.  
window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()는 브라우저에서 Redux Devtools를 사용하기 위한 코드이다.  

## App.js
```
class App extends Component {
  state = {number:0}
  render(){
    return (
      <div className="App">
        <h1>Root</h1>
        <AddNumberRoot></AddNumberRoot>
        <DisplayNumberRoot></DisplayNumberRoot>
      </div>
    );  
  }
}
```
Redux는 store를 통해 state가 관리되므로 onClick 메소드는 삭제한다.  

## AddNumber.jsx
```
import React, {Component} from 'react';
import store from '../store';

export default class AddNumber extends Component {
    state = {size:1}
    render() {
      return (
        <div>
          <h1>Add Number</h1>
          
          <input type="button" value="+" onClick={function(){
            store.dispatch({type:'INCREMENT', size:this.state.size});
          }.bind(this)}></input>
          
          <input type="text" value={this.state.size} onChange={function(e){
            this.setState({size:Number(e.target.value)});
          }.bind(this)}></input>
        </div>
      )
    }
  }
```
store에 size의 state를 변경하기 위해 dispatch(store의 action을 발생) 해준다.  

## AddNumberRoot.jsx
```
export default class AddNumberRoot extends Component{
    render(){
      return (
        <div>
          <h1>Add Number Root</h1>
          <AddNumber></AddNumber>
        </div>
      )
    }
  }
```
store를 통해 state의 값이 바뀌므로 onClick메소드 삭제

## DisplayNumber.jsx
```
import React, {Component} from "react";
import store from "../store";

export default class DisplayNumber extends Component {
  state = {number:store.getState().number}
  
  constructor(props){
    super(props);
    store.subscribe(function(){
      this.setState({number:store.getState().number});
    }.bind(this));
  }
  
    render() {
      return (
        <div>
          <h1>Display Number</h1>
          <input type="text" value={this.state.number} readOnly></input>
        </div>
      )
    }
  }
```
constructor의 store가 subscribe하고 있기 때문에 store의 값이 바뀌면 콜백함수가 호출되면서 state의 값을 변경하게 된다.  
input에 표시되는 값(number)는 store의 state를 가르키게 변경한다.

## DisplayNumberRoot.jsx
```
    render(){
      return (
        <div>
          <h1>Display Number Root</h1>
          <DisplayNumber></DisplayNumber>
        </div>
      )
    }
  }
```
AddNumberRoot와 동일  

# React Component에서 Redux 종속성 기능 제거(Container Component 도입)

## Components/AddNumberRoot & DisplayNumberRoot

## Components/DisplayNumberRoot.jsx
```
import React, {Component} from 'react';
import DisplayNumber from '../Containers/DisplayNumber';

export default class DisplayNumberRoot extends Component {
  render() {
    return(
      <div>
        <h1>Display Number Root (DisplayNumberRoot.jsx)</h1>
        <DisplayNumber></DisplayNumber>
      </div> 
    )
  }
}
```

## ## Components/AddNumberRoot.jsx
```
import React, {Component} from 'react';
import AddNumber from '../Containers/AddNumber';

export default class AddNumberRoot extends Component{
  render(){
    return (
      <div>
        <h1>Add Number Root (AddNumberRoot.jsx)</h1>
        <AddNumber></AddNumber>
      </div>
    )
  }
}
```
AddNumber를 감싸기 위해 Components에서 Containers로 변경해준다.

## Components/AddNumber.jsx
```
import React, {Component} from 'react';

export default class AddNumber extends Component {
    state = {size:1}
    render() {
      return(
        <div>
          <h1>Add Number (AddNumber.jsx)</h1>

          <input type="button" value="+" onClick={function(){
              this.props.onClick(this.state.size);
              //store.dispatch({type:'INCREMENT', size:this.state.size})
          }.bind(this)}></input>

          <input type="text" value={this.state.size} onChange={function(e){
              this.setState({size:Number(e.target.value)});
          }.bind(this)}></input>
        </div> 
      )
    }
}
```
이전 코드는 부품으로써 가치가 있다. onClick 메소드가 있는한 어디서든지 사용이 가능하기 때문이다.  
redux로 변경한 코드는 애플리케이션의 상태에 의존하기 때문에 재사용이 불가능해졌다.  
이를 해결하기 위해선 redux에 종속된 기능을 제거하면 된다.  
AddNumber의 Component를 감싸는 Component를 만들고 그 새로운 Component는 redux의 store를 핸들링하는 Component로 만들고  
AddNumber Component는 redux를 모르는 Component로 만들면 된다.  

## Components/DisplayNumber.jsx
```
import React, { Component } from 'react';

export default class DisplayNumber extends Component {
  /*state = {number:store.getState().number}

  constructor(props){
    super(props);
    store.subscribe(function(){
      this.setState({number:store.getState().number});
    }.bind(this))
  }*/

    render() {
      return(
        <div>
          <h1>Display Number (DisplayNumber.jsx)</h1>
          <input type="text" value={this.props.number} readOnly></input>
        </div> 
      )
    }
}
```
constructor를 Containers의 DisPlayNumber.jsx에 옮긴다.  
DisplayNumber는 render의 value값이 redux에 종속되어 있다.  

## Containers/AddNumber.jsx
```
import Addnumber from "../Components/AddNumber";
import React, { Component } from "react";
import store from '../store';

export default class extends Component {
    render(){
        return <Addnumber onClick={function(size){
            store.dispatch({type:'INCREMENT', size:size})
        }.bind(this)}></Addnumber>
    }
}
```
AddNumber를 감싸는 Containers Component  
Containers component를 만들어서 redux와 상호작용하게 만든다.  
이전의 AddNumber component는 다시 재사용될 수 있게 되돌렸다  

## Containers/DisPlayNumber.jsx
```
import DisplayNumber from '../components/DisplayNumber';
import React, { Component } from 'react';
import store from "../store";

export default class extends Component{
    state = {number:store.getState().number}
    constructor(props){
        super(props);
        store.subscribe(function(){
            this.setState({number:store.getState().number});
        }.bind(this));
    }
    render(){
        return <DisplayNumber number={this.state.number}></DisplayNumber>
    }
} 
```
Components의 DisplayNumber.jsx에 존재하는 constructor를 가져오고, DisplayNumber를 사용하기 위해 props 값인 number를 주입시켜준다.  

# Redux Connect & Provider

## index.js
```
import {Provider} from 'react-redux';
import store from './store'
...
root.render(

<Provider store={store}>
  <App />
</Provider>
)
```
component를 생성할 때 마다 store를 가져오는건 매우 귀찮은 일이므로 Redux가 제공하는 Component인 Provider를 사용해 App을 감싸준다.  
Provider는 무조건 props를 받아야 하는데 이 props는 store로 한다.  
이렇게 되면 Provider component를 통해 각 하위 component로 store를 공급해준다.  

## connect - mapStateTOprops()

```
import DisplayNumber from '../Components/DisplayNumber';
import {connect} from 'react-redux';

function mapReduxStateTOReactprops(state){
    return {
        number:state.number
    }
}

export default connect(mapReduxStateTOReactprops) (DisplayNumber);
```

connect 메소드는 connect를 실행하면 return값이 함수고, 그 return된 함수를 다시 실행해서 export하는데  
이는 아래의 수동으로 했던 랩핑 component와 똑같은 값을 리턴한다.  


connect는 2개의 인자 `mapStateTOprops()`, `mapDispatchToProps()` 가 들어와야 한다.  

```
function mapReduxStateTOReactprops(state){
    return {
        number:state.number
    }
}
```

위 함수가 호출될 때 redux의 state 값을 인자로 받도록 약속되어 있다.  

위 코드와 같이 작성하게 되면  
```
state = {number:store.getState().number}

store.subscribe(function(){
            this.setState({number:store.getState().number});
        }.bind(this));

number={this.state.number}
```
이전에 작성했던 코드와 같아지게 된다.  

mapStateTOprops(), mapDispatchToProps() 두 인자는 원하는 이름으로 변경해도 된다.  
mapStateTOprops()는 redux의 State를 React의 props로 맵핑해주며,  
mapDispatchToProps()는 Redux의 Dispatch를 React의 Props로 연결해준다 라고 이해하면 된다.  

아래의 이전 코드에서 number라는 props는 state값이 store의 subscribe를 통해 state의 값을 number로 주면  
그 state의 number값이 바뀔때마다 setState에서 render가 실행되면서 number의 값이 변경된다.  
이 작업을 수월하게 해주는 것이 mapStateTOprops()이다.  

```
import React, { Component } from 'react';
import store from "../store";

export default class extends Component{
    state = {number:store.getState().number}
    constructor(props){
        super(props);
        store.subscribe(function(){
            this.setState({number:store.getState().number});
        }.bind(this));
    }
    render(){
        return <DisplayNumber number={this.state.number} unit={this.props.unit}></DisplayNumber>
    }
} 
```

## connect - mapDispatchToProps()
```
import AddNumber from "../Components/AddNumber";
import {connect} from 'react-redux';

function mapDispatchToProps(dispatch){
    return {
        onClick:function(size){
            dispatch({type:'INCREMENT', size:size});
        }
    }
}
export default connect(null, mapDispatchToProps)(AddNumber);
```
mapDispatchToProps()는 Redux의 dispatch를 React의 component에 props로 연결시켜주는 정보를 담고있는 함수를 작성하면된다.

아래 주석처리된 코드에서 onClick은 전달해야할 props 값이므로 mapDispatchToProps의 return에 작성해주면 되며,  
mapDispatchToProps()가 호출될 때 dispatch을 인자로 받으면 store대신 dispatch을 사용한다.

```
export default class extends Component {
    render(){
        return <Addnumber onClick={function(size){
            store.dispatch({type:'INCREMENT', size:size})
        }.bind(this)}></Addnumber>
    }
}
```
