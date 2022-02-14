### Tag

- Tag는 HTML문서를 이루는 중요한 요소이며, 시작 <>과 종료 </>로 이루어져 있다.

## Box OR Item

### Box Tag

- Tag안에 content가 없는 이상 사용자에게 보여지지 않는 태그
- ex)
```
  - <header></header>
  - <footer></footer>
  - <section></section>
  - <div></div>
  - <span></span>
```
### Item Tag

- Tag안에 content가 없어도 사용자에게 보여지는 태그
- ex)
```
  - <a></a>
  - <input></input>
  - <table></table>
```
### Block과 Inline

- Block은 하나의 태그가 공간을 차지하면 그 뒤에오는 태그는 다음 줄로 내려간다.
- Inline은 Block과의 반대로 먼저 쓰여진 태그 옆에 작성된다.
``` 
    <p>This is a sentence. <b>That</b> is..</p>
    <p>This is a sentence. <span>That</span> is..</p>
    <p>This is a sentence. <div>That</div> is..</p>
```
### List
- ul 태그는 순서가 없는 목록을 만들 때 사용하며 ul 내부에 li 요소를 포함해 각 항목을 표시한다.
- ol 태그는 순서가 있는 목록을 만들 때 사용하며 ul과 같이 내부에 li를 포함한다.
- ol에는 type, reserved와 같은 속성을 사용할 수 있다.
```
    <ul>
      <li>Hello</li>
      <li></li>
      <li></li>
    </ul>
    
    <ol type="i" reversed> <!--type="i" = roman 언어 타입으로 변경, reversed 순서를 거꾸로-->
      <li>1</li>
      <li>2</li>
      <li>3</li>
    </ol>
```    
### Input and Type

- 사용자에게 입력받는 태그 lable도 주로 같이 사용한다.
```
<label for="input_name">name: </label>
<input id="input_name" type="text">
```
