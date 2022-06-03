# Proxy

react는 개발서버 포트인 3000과 php의 포트인 8000를 fetch api를 통해 통신이 가능하다 ex(`fetch('http://localhost:8080/api_path`)  
하지만 웹 어플리케이션에서 다른 포트번호나 도메인에 접근하려고 하면 브라우저의 보안 기능으로 인해 오류가 발생한다. 
이를 해결하기 위해 php나 Django등의 백엔드 서버에서 8000번 포트를 접속 허용을 해줘야 하는데 이것이 CORS(Cross-Origin Resource Sharing)이다.  

하지만 백엔드 서버에서 접속 허용을 해주는 것은 매우 귀찮은 일이라고 한다. 그래서 이러한 문제를 해결하기 위해 Proxy를 사용한다.  

Proxy를 사용하게 되면 `fetch('http://localhost:8080/...)`이라고 적을 필요 없이 `fetch('data.json')`처럼 단순화 시킬 수 있으며,  
이를 사용하기 위해서 package.json에 `proxy:'http://localhost:8080`을 즉 백엔드 서버의 host이름과 포트번호를 적어주기만 하면 된다.  

Proxy의 작동 방법은 React는 React Dev Server(3000)에 접속하며 `fetch('/api_path')`가 없다는 사실을 알면 package.json의 proxy 정보를 보고 해당 백엔드 서버에 접속한 뒤  
서버에 있는 정보를 React Dev Server에 보내주게 되고, 이 정보를 React Dev Server가 대신 응답해준다.

## data.json
```
{
    "result":"ok"
}
```
상위 폴더에 data.json을 생성후 npx local-web-server를 통해 8000번 포트를 열어준다.

## index.js
```
class App extends React.Component{
  render(){
    return (
      <div>
        <input type="button" value="get data" onClick={
          function(){
            fetch('/data.json')
              .then(function(result){return result.json()})
              .then(function(json){console.log(json);})
          }.bind(this)
        }></input>
      </div>
    )
  }
}
```
버튼 클릭시 packagejson의 proxy 서버 host이름과 포트 번호를 찾고 data.json을 넘겨주어 console에 result값을 띄운다.

## packagejson
```
{
...

"proxy":"http://localhost:8000",

...
}
```
Proxy 사용을 위해 host이름과 포트번호가 담긴 proxy를 생성한다.

![1](https://user-images.githubusercontent.com/73509513/171798036-7f85d66e-4fb9-48fa-a0b1-d7731fee3086.PNG)  

![2](https://user-images.githubusercontent.com/73509513/171798041-5c85948a-45b9-4f7a-8dbc-5a4567b34b2f.PNG)  

![3](https://user-images.githubusercontent.com/73509513/171798043-84614a05-a497-41c7-aa40-a99d147db6c3.PNG)
