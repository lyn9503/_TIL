# Selector(선택자)
### Selector는 HTML에 어떤 태그를 고를것인지 규정하는 문법

# Selector의 종류
### 1. 결합 선택자  
```
 자손 선택자  
  A B  
  ex) .parent .child  
  A를 만족하는 요소의 자손(하위) 요소 중 B를 만족하는 요소를 가르킨다.  
```
```
 자식 선택자
  A > B
  ex) .parent > .child
  A를 만족하는 요소의 자식 요소 중 B를 만족하는 요소를 가르킨다.
```
```
 인접 형제 선택자
  A + B
  ex) p ~ span
  A의 다음 형제 요소를 만족하면서 B를 만족하는 요소를 가르킨다.
```
```
 일반 형제 선택자
  A ~ B
  ex) <p> </p>
      <span> </span>
      <h1> </h1>
      p + h1 -> 불가능
      p + span -> 가능
  A의 바로 다음의 형제 요소를 만족하면서 B를 만족하는 요소를 가르킨다.
```
### 2. ID 선택자
``` 
 #ID
 ID를 선택한다.
```
### 3. Class 선택자
```
 .classname
  클래스를 선택한다.
 A.classname
  A에 대한 클래스를 선택한다.
```
### 4. 전체 선택자
```
 *
 모든 요소를 선택한다.
```
### 5. 의사 클래스
```
 :first-child
 형제 요소 중 제일 첫번째 요소를 나타낸다.
```
```
 :only-child
 유일한 요소를 나타낸다.
```
```
 :last-child
  다른 요소 내부의 마지막 하위 요소를 선택
```
```
 :nth-child
  같은 부모의 n번째 자식의 요소를 선택
```
```
 :nth-last-child(A)
  제일 마지막 요소부터 선택
```
```
 :nth-of-type(A)
  n번째 형제를 선택
  키워드(even, odd), 정수, 공식(An+B)가 들어갈 수 있다.
```
```
 :first-of-type
  첫번째 요소부터 선택
```
```
 :last-of-type
  마지막 요소를 선택
```
```
 :only-of-type
  같은 유형의 요소가 없을때(해당 유형의 유일한 요소를 선택)
```
```
 :empty
  하위 항목이 없는 요소 선택
```
```
 :not(X)
  X와 일치하지 않는 모든 요소를 선택한다.
  ex) not(#id) : id가 없는 모든 요소를 선택한다.
```
### 6. 속성 선택자
```
 [attribute] 속성 선택
 A[attribute] A에 대한 속성 선택
 [attribute="value"] 속성에 대한 특정값을 선택
 [attribute^="value"] 특정 문자열로 시작하는 속성을 모두 선택
 [attribute$="value"] 특정 문자열로 끝나는 요소를 모두 선택
 [attribute*="value"] 특정 문자열을 포함하는 요소를 모두 선택
```

