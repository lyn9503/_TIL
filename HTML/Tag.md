### Tag

- Tag는 HTML문서를 이루는 중요한 요소이며, 시작 <>과 종료 </>로 이루어져 있다.

## Box OR Item

### Box Tag

- Tag안에 content가 없는 이상 사용자에게 보여지지 않는 태그
- ex)

  - <header>
  - <footer>
  - <section>
  - <div>
  - <span>

### Item Tag

- Tag안에 content가 없어도 사용자에게 보여지는 태그
- ex)
  - <a>
  - <input>
  - <table>

### Block과 Inline

- Block은 하나의 태그가 공간을 차지하면 그 뒤에오는 태그는 다음 줄로 내려간다.
- Inline은 Block과의 반대로 먼저 쓰여진 태그 옆에 작성된다.
- 
    <p>This is a sentence. <b>That</b> is..</p>
    <p>This is a sentence. <span>That</span> is..</p>
    <p>This is a sentence. <div>That</div> is..</p>

### List

    ol>li*3 : ol안에 li 태그 3개를 한번에 작성해준다.
  
    <ol type="i" reversed> <!--type="i" = roman 언어 타입으로 변경, reversed 순서를 거꾸로-->
      <li>1</li>
      <li>2</li>
      <li>3</li>
    </ol>
    
    <ul>
      <li>Hello</li>
      <li></li>
      <li></li>
    </ul>

### Input and Type

- 사용자에게 입력받는 태그 lable도 주로 같이 사용한다.
'''
   <label for="input_name">name: </label>
   <input id="input_name" type="text">
'''
