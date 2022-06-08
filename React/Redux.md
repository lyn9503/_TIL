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
