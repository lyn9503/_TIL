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

## Clean Up
```
  useEffect(() => {
    console.log('%cfunc => useEffect (componentDidMount & componentDidUpdate) '+(++funcId), funcStyle);
    document.title = number + ' : ' + _date;
    return function(){
      console.log('%cfunc => useEffect return (componentDidMount & componentDidUpdate) '+(++funcId), funcStyle);
    }
  });
```
![1](https://user-images.githubusercontent.com/73509513/174519516-8c0efc97-9b8d-44e3-b241-9b5de1950803.PNG)  

useEffect는 웹페이지가 처음 render가 실행될 때 실행되고, render가 실행될 때 마다 실행된다.  
useEffect은 componentDidMount와 componentDidUpdate의 효과를 낸다.  
그러므로 useEffect는 class의 lifecycle처럼 함수 안에서도 사용할 수 있도록 약속된 api이다.  

useEffect는 side effect가 생략된 이름이며, react에서 main effect는 함수가 호출됐을 때 return되는 결과를 말하며,  
side effect는 main effect를 벗어나는 작업들 즉, render가 끝난 이후 AJAX를 통해 가져와서 내용을 변경시킨다던지, 웹페이지의 title을 변경하는 따위의 일을 말한다.  

## Skipping Effect

```
  useEffect(() => {
    console.log('%cfunc => useEffect number (componentDidMount & componentDidUpdate) '+(++funcId), funcStyle);
    document.title = number;
    return function(){
      console.log('%cfunc => useEffect number return (componentDidMount & componentDidUpdate) '+(++funcId), funcStyle);
    }
  }, [number]);

  useEffect(() => {
    console.log('%cfunc => useEffect _date (componentDidMount & componentDidUpdate) '+(++funcId), funcStyle);
    document.title = _date;
    return function(){
      console.log('%cfunc => useEffect _date return (componentDidMount & componentDidUpdate) '+(++funcId), funcStyle);
    }
  }, [_date]);
```

![2](https://user-images.githubusercontent.com/73509513/174519521-5e14577f-dc61-496f-a37d-ee4130c22741.PNG)  

![3](https://user-images.githubusercontent.com/73509513/174519589-a26f1648-31dc-4458-9fe7-4cddac741f37.PNG)

이전 useEffect 코드에서 ``document.title = number + ' : ' + _date;``를 document.title = number;로 변경하면  
number의 state만 참조해서 작업을 진행한다.   
이는 number의 값이 바뀌지 않으면 작업을 하지 않는데 useEffect를 활용하면 number의 값이 바뀔때만 함수가 호출되도록 할 수 있다.  
이는 함수가 끝나고 [] 중괄호를 넣고 number를 적으면 된다.  
이렇게 추가하게 되면 number의 state가 변경될 때마다 첫번째 인자인 콜백함수가 호출되도록 약속되어진다.  

## componentWillUnMount (function, class)
```
function App() {
  var [funcShow, setFuncShow] = useState(true);
  var [classShow, setClassShow] = useState(true);
  return (
    <div className="container">
      <h1>Hello World</h1>
      <input type = "button" value="remove func" onClick={()=>{
        setFuncShow(false);
      }}></input>

      <input type = "button" value="remove class"onClick={()=>{
        setClassShow(false);
      }}></input>
      {funcShow ?<FuncComp initNumber={2}></FuncComp> : null}
      {classShow ? <ClassComp initNumber={2}></ClassComp> : null}
    </div>
  );
}
```
### function
```
  useEffect(() => {
    console.log('%cfunc => useEffect (componentDidMount) '+(++funcId), funcStyle);
    document.title = number;
    return function(){
      console.log('%cfunc => useEffect return (componentWillUnMount) '+(++funcId), funcStyle);
    }
  }, []);
```
### class
```
class
  componentWillUnmount(nextProps, nextState){
    console.log('%cclass => componentWillUpdate', classStyle);
  }
```

![4](https://user-images.githubusercontent.com/73509513/174519605-2efb0771-e203-4d23-ba87-a8b25c620969.PNG)  

![5](https://user-images.githubusercontent.com/73509513/174519611-94b137e6-30ef-4a30-9633-f55686b6e1e4.PNG)  

componentDidMount만 작업하게 하려면 []빈 배열만 주면 1회만 실행이 되어진다.  

App에 input 태그로 버튼을 만들어 버튼을 클릭하면 useState의 상태가 false로 바뀌고  
useEffact의 return 함수 즉 componentWillUnMount가 실행되어 삭제된다.  
class도 마찬가지로 componentWillUnMount가 실행되어 삭제되어진다.  
이후 Clean Up이 실행된다.  
