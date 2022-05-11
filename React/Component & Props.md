# Component
Component는 UI를 재사용이 가능한 개별적인 여러 조각으로 나누는 것이다.

## Component가 없다면?
```
<html>
    <body>
        <header>
            <h1>WEB</h1>
            world wide web!
        </header>

        <nav>
            <ul>
                <li><a href="1.html">HTML</a></li>
                <li><a href="2.css">CSS</a></li>
                <li><a href="3.js">JavaScript</a></li>
            </ul>
        </nav>

        <article>
            <h2>HTML</h2>
            HTML is HyperText Markup Languege.
        </article>
    </body>
</html>
```
위 코드처럼 간단하면 이해하기 쉽지만 각각 태그의 코드의 수가 천줄, 몇천줄이상 되면 이해하기 힘들어진다.  
이러한 문제점을 해결하기 위해 Component를 이용해 각각 태그를 나누어준다.

# HTML을 Component화
Component에는 함수와 클래스 두가지로 표현할 수 있다.  
Component를 만들때 그 Component는 하나의 최상위 태그로 시작해야한다. (header, div, ...)

## 함수
```
function Subject() {
  return <header>
            <h1>WEB</h1>
            world wide web!
         </header>
  ;
}

function TOC() {
  return <nav>
          <ul>
            <li><a href="1.html">HTML</a></li>
            <li><a href="2.css">CSS</a></li>
            <li><a href="3.js">JavaScript</a></li>
          </ul>
         </nav>
  ;
}

function Content() {
  return <article>
          <h2>HTML</h2>
          HTML is HyperText Markup Languege.
         </article>
  ;
}
```
함수는 JavaScript 함수를 작성해 정의한다.  

## 클래스
```
class Subject extends Component{
  render(){
    return (
      <header>
        <h1>WEB</h1>
        world wide web!
      </header>
    );
  }
}

class TOC extends Component{
  render(){
    return(
      <nav>
        <ul>
          <li><a href="1.html">HTML</a></li>
          <li><a href="2.css">CSS</a></li>
          <li><a href="3.js">JavaScript</a></li>
        </ul>
      </nav>
    );
  }
}

class Content extends Component{
  render(){
    return(
      <article>
        <h2>HTML</h2>
        HTML is HyperText Markup Languege.
      </article>
    );
  }
}
```
## 적용
```
class App extends Component {
  render() {
    return (
      <div className="App">
        <Subject></Subject>
        <TOC></TOC>
        <Content></Content>
      </div>
    );
  }
}
```
위에서 HTML이 담긴 Class의 이름을 정한 태그를 <>을 이용해 적용시키면 된다.

![6](https://user-images.githubusercontent.com/73509513/167335107-79c870fd-2bd7-425d-9d8a-cf0e8bc5a9c0.PNG)

# Props
component에 전달 : {this.props.title}  
component는 언제나 똑같은 내용을 보여주는데 props를 사용해 효율적으로 출력값을 변경할 수 있다.  

# component 분리
App.js파일에 여러개의 component가 몰려있어 다른 파일에서 접근하기가 힘드므로, 각각의 컴포넌트들로 나누는 것이 좋다.  

## component 파일 생성

''`
import React, { Component } from 'react';
''`
react라는 라이브러리에서 component라고 하는 클래스를 로딩한다.

## 외부에서 component 파일 불러오기

외부에서 component를 사용하기 위해서는
``
export default TOC;
``
을 작성하면 되며, 불러오려면
``
import TOC from "./components/TOC";
``
을 작성해주면 된다.  

이렇게 component를 나누어주면 코드가 한층 간결해지고, 필요한 컴포넌트만 import 해주면 되므로 간편하며, App.js가 아닌 다른 js파일에서도 사용할 수 있는 장점이 있다.  

