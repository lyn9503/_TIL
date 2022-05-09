# Component
Component는 UI를 재사용이 가능한 개별적인 여러 조각으로 나누는 것이다.

# Component가 없다면?
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
