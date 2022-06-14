# Class & Function의 차이

### Class
```
class ClassComp extends React.Component{
  render(){
    return(
      <div className="container">
        <h2>Class style Component</h2>
      </div>
    )
  }
}
```

### Function
```
function FuncComp(){
  return(
    <div className="container">
      <h2>Function style Component</h2>
    </div>
  )
}
```
React에서 Component를 만들때 Class는 render() 함수로 Function은 return으로 시작하면 된다.  
Function은 자기 자신이 render()함수이다.  

# props
```
function App() {
  return (
    <div className="container">
      <h1>Hello World</h1>
      <FuncComp initNumber={2}></FuncComp>
      <ClassComp initNumber={2}></ClassComp>
    </div>
  );
```
각 component에 initNumber의 값 설정

### Class
```
class ClassComp extends React.Component{
  render(){
    return(
      <div className="container">
        <h2>Class style Component</h2>
        <p>Number : {this.props.initNumber}</p>
      </div>
    )
  }
}
```
Class는 this.props를 사용해 initNumber의 값을 가져오면 된다.

### Function
```
function FuncComp(props){
  return(
    <div className="container">
      <h2>Function style Component</h2>
      <p>Number : {this.props.initNumber}</p>
    </div>
  )
}
```
Function은 React가 호출할 때 첫번째 파라미터의 인자값으로 전달된 props값을 전달하도록 약속되어 있다.  
그러므로 Function은 initNumber를 호출할 때 this를 쓰지 않고 props라는 parameter를 사용한다.  
props parameter에는 initNumber의 값이 들어있다.  

# state
Class는 무리없이 state의 사용이 가능하지만 Function은 useState라는 React Hook의 기능을 사용한다.  
useState의 추가 : ``import React, {useState} from 'react';``

## setState(Class)
```
class ClassComp extends React.Component{
  state = {
    number:this.props.initNumber
  }

  render(){
    return (
      <div className="container">
        <h2>Class style Component</h2>
        <p>Number : {this.state.number}</p>

        <input type="button" value="random" onClick={
          function(){
            this.setState({number:Math.random()});
          }.bind(this)
        }></input>

      </div>
    )
  }
}
```
Class는 State 사용시 초기화를 해주어야 한다.  
state의 number안에 props로 initNumber의 값을 가져오고, Number에 state의 number를 불러온다.  

버튼을 추가해 setState를 이용해 number의 값이 무작위로 바뀌도록 했다.  
이는 setState가 state의 값을 변경하기 때문인데, 버튼을 클릭할 때 마다 setState에 의해 state의 값이 바뀌고,  
state의 값이 바뀌면 render() 메소드가 호출되면서 바뀐 결과가 반영되기 때문이다.  

## useState(Function (Hook))
```
function FuncComp(props){
  var numberState = useState(props.initNumber);
  var number = numberState[0]; // 상태 값 (state)
  var setNumber = numberState[1]; // 상태를 변경할 값 (setState)

  return (
    <div className="container">
    
      <h2>Function style Component</h2>
      <p>Number : {number}</p>
      <p>Date : {_date}</p>

      <input type="button" value="random" onClick={
          function(){
            setNumber(Math.random());
          }
        }></input>
        
    </div>
  )
}
```
이전에는 Class에서만 state를 사용할 수 있었지만 Hook의 추가로 인해 사용이 가능해졌다.  
Hook은 React에 내장되어 있으며, 사용자도 Hook을 생성해 만들 수 있다.  
Function에서 Hook을 이용해 state는 useState를 사용하며, 이 useState는  2개의 값으로 이루어진 배열을 return한다.  
useState에 initNumber의 값을 넣으러면 props.initNumber를 써주면 되며, number에 배열의 첫번째 공간으로 지정해주면 된다.  

useState에서 Class의 setState의 역할을 하는 것이 두번째 공간이다.  
setNumber라는 변수에 useState의 두번째 공간을 할당했으며, 이 setNumber에는 함수가 담겨있고, 이 함수를 통해서 number의 값이 변경된다.  

``var [number, setNumber] = useState(props.initNumber);``  
useState를 사용할 때 위에처럼 초기 설정을 해주어도 되지만 한줄로 정의할 수도 있다.  
이는 useState가 2개의 공간을 가진 배열이라서 가능하며, 첫번째 배열의 공간에 initNumber로 props를 이용해 가져오며, 두번째 공간은 값 변경을 위한 공간이므로 아무것도 할당하지 않는다.
