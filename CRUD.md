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
# Update
# Delete
