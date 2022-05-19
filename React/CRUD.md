# CRUD
## Control.js
```
render(){
  console.log(`subject render`);
   return (
    <ul>
      <li>
        <a href="/create" onClick={function(e){
          e.preventDefault();
          this.props.onChangeMode('create');
          }.bind(this)}>create </a>
      </li>

      <li>
        <a href="/update" onClick={function(e){
          e.preventDefault();
          this.props.onChangeMode('update');
         }.bind(this)}>update </a>
      </li>

      <li>
        <input onClick={function(e){
          e.preventDefault();
          this.props.onChangeMode('delete');
        }.bind(this)} type="button" value="delete"></input>
      </li>
    </ul>
  );
}
```
### mode : create
![create](https://user-images.githubusercontent.com/73509513/168527460-a08ef6db-0b23-42a6-b176-236399f053b8.PNG)  

### mode : update
![update](https://user-images.githubusercontent.com/73509513/168527463-1f1bea5a-208f-4917-866b-fb020a2ac226.PNG)  

### mode : delete
![delete](https://user-images.githubusercontent.com/73509513/168527461-d21fd630-2d60-4096-9189-5645669d6b18.PNG)  

각각 create, update, delete의 용도에 맞게 변경하기 위한 js이며, onClick함수를 통해 App.js의 Control component의 onChageMode로 전달되어 mode가 변경되게 된다.  

## Create
### CreateContents.js
```
<article>
  <h2>Create</h2>
  <form action="/create_process" method="post"
    onSubmit={function(e){
      e.preventDefault();
      this.props.onSubmit(
        e.target.title.value,
        e.target.desc.value
      );
    }.bind(this)}>
    <p>
       <input type="text" name="title" placeholder="title"></input>
    </p>

    <p>
       <textarea name="desc" placeholder="description"></textarea>
    </p>

    <p>
       <input type="submit"></input>
    </p>
  </form>
</article>
```
사용자의 입력을 받기위한 input 2개(title, desc)와 입력된 정보를 전송하기 위해 submit 버튼을 생성하고,  
props.onSubmit 함수를 통해 입력된 값의 경로인 e.target.title(desc).value를 App.j에 전달한다.

### App.js
```
else if(this.state.mode === 'create'){
  _article = <CreateContent onSubmit={function(_title, _desc){
    // add content to this.setState.contents
    this.max_content_id = this.max_content_id + 1;
        
    var _contents = this.state.contents.concat( {id:this.max_content_id, title:_title, desc:_desc} )

    this.setState({ contents: _contents }); }.bind(this)}></CreateContent>
  }
```
### Create React
![Create_React](https://user-images.githubusercontent.com/73509513/168527468-6630b2e5-c2a5-4d2c-8918-1de61f1e2b17.PNG)  

mode가 create일때 input에 입력된 title의 정보와 desc의 정보를 CreateContent.js에서 받아온다.  
이후 App.js에서 입력된 정보를 content에 넣기위해 id의 값을 1 증가시키고, `_contents`에 증가된 ID값과 title, desc의 정보를 넘겨주고, setState를 통해 변경된다.
## Concat과 Push
위에 사용된 Concat은 Push로도 정보를 저장할 수 있지만, Push로 정보를 저장하게 되면 원본 자체가 변화되어 state의 불변성에 어긋나게 되어  
기존의 정보는 유지한 채 새로운 정보를 추가하는 Concat을 사용해 불변성도 유지되며, 성능도 최적화 된다.  

## Read
### ReadContent.js
```
render(){
  console.log('content render');
  return(
    <article>
      <h2>
        {this.props.title}
      </h2>
      {this.props.desc}
    </article>
   );
}
```
title과 desc를 읽기위한 Component js파일
```
getReadContent(){
  var i = 0;
  while(i < this.state.contents.length){
    var data = this.state.contents[i];
    if(data.id === this.state.selected_content_id) {
      return data;
      break;
    }
    i = i + 1;
    }
  }
```
while을 사용해 contents의 길이만큼 반복하며, 읽어온 contents를 data에 넣어준다.  
만약 data의 id와 selected_content_id의 id값이 일치할 경우 data를 반환하고 멈춘다.  

# Update
## UpdateContent.js
```
  constructor(props) {
    super(props);
    this.state = {
      id:this.props.data.id,
      title:this.props.data.title,
      desc:this.props.data.desc
    }
    this.inputFormHandler = this.inputFormHandler.bind(this);
  }
  
inputFormHandler(e){
  this.setState({[e.target.name]:e.target.value});
}
```
객체를 생성 및 초기화 하기위한 constructor함수를 사용해 id, title, desc의 값과 inputFormHandler함수의 값을 초기화 해준다.  
inputFormHandler함수는 title, desc의 값의 state를 변경해주는 함수이다.  

```
  render(){
      return(
        <article>
          <h2>Update</h2>
          <form action="/create_process" method="post"
            onSubmit={function(e){
              e.preventDefault();
              this.props.onSubmit(
                this.state.id,
                this.state.title,
                this.state.desc
              );
            }.bind(this)}
          >
            <input type="hidden" name="id" value={this.state.id}></input>
            {/**id는 사용자에게 보일 필요가 없기 때문에 hidden form을 쓴다. */}
            <p>
              <input type="text" 
                     name="title" 
                     placeholder="title" 
                     value={this.state.title}
                     onChange={this.inputFormHandler}>
                     
              </input>
            </p>

            <p>
              <textarea name="desc" 
                        placeholder="description"
                        value={this.state.desc}
                        onChange={this.inputFormHandler}>
              </textarea>
            </p>

            <p>
              <input type="submit"></input>
            </p>
          </form>
        </article>
      );
    }
  }
```
content를 업데이트 하기 위해서는 id의 값이 필요한데 이는 사용자에게 보여질 필요가 없으므로 hidden을 사용해 숨겨준다.  
input과 textarea의 내용은 inputFormHandler 함수를 통해 state를 변경하게 된다.  

## App.js
```
  } else if(this.state.mode === 'update'){
    _content = this.getReadContent();
    _article = <UpdateContent data={_content} onSubmit={
      function(_id, _title, _desc){
        var _contents = Array.from(this.state.contents); // contents 원본을 복사한 새로운 javascript가 만들어진다.
        var i = 0;
        while(i < _contents.length){
          if(_contents[i].id === _id){
            _contents[i] = {id:_id, title:_title, desc:_desc};
            break;
          }
          i = i + 1;
        }
        this.setState({
          contents: _contents
        });
        console.log(_title, _desc);
      }.bind(this)}></UpdateContent>
  }
```
mode의 state가 update일 경우 `_content` 는 getReadContent()함수를 호출해 contents의 값을 입력받는다.  
`_article`은 UpdateContent.js의 onSubmit 함수의 값을 전달 받고 id와 title, desc의 값을 Array를 통해 원본을 복사한다.  
while을 통해 contents의 길이만큼 반복하게 되며, contents의 id값과 `_id`의 값이 일치하다면 `_contents`의 [i]번째에 전달받은 값을 넣고 멈춘다.  
그 후 setState를 통해 contents에 `_contents`의 값을 넣게되면 그 contents는 값이 변경되게 된다.  

# Delete
```
<Control onChangeMode={function(_mode){
  if(_mode === 'delete') {
    if(window.confirm('really?')){
      var _contents = Array.from(this.state.contents);
      var i = 0;
      while(i < this.state.contents.length){
        if(_contents[i].id === this.state.selected_content_id){
          _contents.splice(i, 1);
          break;
        }
        i = i + 1;
      }
      this.setState({
        mode:'welcome',
        contents:_contents
      });
      alert('delete');
      }
      } else {
          this.setState({
          mode:_mode
        });
      }
    this.setState({
      mode:_mode
    });}.bind(this)}>
</Control>
```
`_mode`가 delete일 경우 정말로 삭제할 것인지를 묻기위해 window.confirm을 사용해서 사용자에게 창을 띄워준다.  
`_contents`는 contents의 값을 복사하며, while을 사용해 contents의 i번째 id 값과 selected_content_id의 id 값이 일치하면  
splice를 통해 삭제한 후 멈추게된다.  
이후 setState에서 mode와 contents의 state를 welcome으로 변경한 뒤 맞는 contents를 보여주게 되고, alert을 통해 삭제가 되었다고 사용자에게 알려준다.  
