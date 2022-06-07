# Redux

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
