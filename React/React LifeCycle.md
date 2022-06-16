# LifeCycle
![lifecycle](https://user-images.githubusercontent.com/73509513/173979088-52c530b3-9cbd-442b-8799-81f40862b2fc.png)
(https://hackernoon.com/reactjs-component-lifecycle-methods-a-deep-dive-38275d9d13c0)

React의 LifeCycle은 총 4단계로 나뉘어진다고 한다.

1. 초기화
2. 마운트
3. 업데이트
4. 마운트 해제

## class
```
class ClassComp extends React.Component{
  componentWillMount(){
    console.log('%cclass => componentWillMount', classStyle);
  }
  componentDidMount(){
    console.log('%cclass => componentDidMount', classStyle);
  }
  shouldComponentUpdate(nextProps, nextState){
    console.log('%cclass => shouldComponentUpdate', classStyle);
    return true;
  }
  // shouldComponentUpdate는 render를 호출할 필요가 있는지를 판단한다.
  
  componentWillUpdate(nextProps, nextState){
    console.log('%cclass => componentWillUpdate', classStyle);
  }
  componentDidUpdate(nextProps, nextState){
    console.log('%cclass => componentDidUpdate', classStyle);
  }
  render(){
    console.log('%cclass => render', classStyle);

    return (
    
    )
    ...
  )
}
```
react의 lifecycle은   

1. 기본적인 state, props 저장  
2. componentWillMount  
3. render  
4. componentDidMount  

![1](https://user-images.githubusercontent.com/73509513/173979542-9bc328c5-ec1d-48ef-8e7a-26cdf34abfaa.PNG)

로 진행되며,  

State가 업데이트 될 시에는  

1. shouldComponentUpdate
2. componentWillUpdate
3. render
4. componentDidUpdate

![2](https://user-images.githubusercontent.com/73509513/173979646-0645c7bf-0f2a-416c-b912-35435b13a95c.PNG)

순으로 진행된다.  

## function
### useEffect (hook)
```
function FuncComp(props){

  ...

  useEffect(function(){
    console.log('%cfunc => useEffect (componentDidMount & componentDidUpdate) '+(++funcId), funcStyle);
    document.title = number + ' : ' + _date;
  });
```
### 웹페이지 첫 실행
![4](https://user-images.githubusercontent.com/73509513/173980135-600b9c48-4afd-4c4a-ba46-8d2503e973c4.PNG)

### render 실행
![3](https://user-images.githubusercontent.com/73509513/173980189-6bfd0eb9-a905-4654-b4f1-fdf7aeb061d3.PNG)

useEffect는 웹페이지가 처음 render가 실행될 때 실행되고, render가 실행될 때 마다 실행된다.  
useEffect은 componentDidMount와 componentDidUpdate의 효과를 낸다.  
그러므로 useEffect는 class의 lifecycle처럼 함수 안에서도 사용할 수 있도록 약속된 api이다.  

useEffect는 side effect가 생략된 이름이며, react에서 main effect는 함수가 호출됐을 때 return되는 결과를 말하며,  
side effect는 main effect를 벗어나는 작업들 즉, render가 끝난 이후 AJAX를 통해 가져와서 내용을 변경시킨다던지, 웹페이지의 title을 변경하는 따위의 일을 말한다.  
  
