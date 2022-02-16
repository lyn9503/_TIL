# Layout
># layout
>>**css**는 기본적으로 **position**이 **static**으로 고정되어 있다.  
>>**article**은 **body**안에 담겨져 있어 화면의 왼쪽 끝에 기본적으로 배치되므로 **position의 값**을 변경하면 해결된다.  
>>**relative**는 **설정한 값(left 20px; top 20px;)** 에 따라 배치가 변경된다.  
>>**absolute**는 가장 가까운 상자에서 위치가 변경되어 배치된다.  
>>**fixed**는 상자안에서 벗어나 웹페이지 안에서 지정한 값에 따라 배치된다.  
>>**sticky**는 상자가 고정되어 스크롤링해도 벗어나지 않고 붙어있는다.  
 
 
># display
>>inline (태그의 크기(길이)단위)  
>>inline-block (블럭단위)  
>>block (한줄에 하나씩만 배치)


> # float  
>float은 이미지와 텍스트를 어떻게 배치할것인지 대해서 정의하는 것
>>left - 이미지가 왼쪽으로 배치되고 텍스트는 오른쪽에 배치  
>>center - 중앙을 기준으로 텍스트가 배치  
>>right - 오른쪽에 배치되고 텍스트는 왼쪽에 배치  



  ---
# FlexBox


># FlexBox의 특징
>container에 적용되는 속성값이 존재하며 각각의 item에 적용되는 속성값이 있다.  
>중심축과 반대축이 존재하며, item의 배치에 따라 중심축과 반대축이 변경된다.


># height:  
>%를 쓰게되면 컨테이너가 들어가있는 부모(body)의 높이에 %를 채운다.  
>vh를 사용하면 부모에 상관없이 채울 수 있다.


## Container에 적용되는 속성

># **display: flex**  
>(flexbox로 만들기 위한 값)


># **flex-direction:**
>row(열 값), column(행 값), -reverse 적용시 반대


># **flex-wrap:**  
>>**nowrap** - 모든 아이템을 한 줄에 정렬  
>>**wrap** - item들을 여러 줄(꽉 차면 다음줄)에 걸쳐 정렬  
>>**wrap-reverse** - item들을 반대로 정렬)  
     
     
># **flex-flow:**  
>direction과 wrap을 한번에 적용 가능하다.


># justify-content   
>아이템을 어떻게 배치할 것인지를 결정한다.  
>>**flex-start** - 아이템의 순서는 유지하되 왼쪽 정렬  
>>**flex-end** - 아이템의 순서는 유지하되 오른쪽으로 정렬  
>>**space-around** - 박스를 둘러싸게 공간을 넣어준다.  
>>**space-evenly** - 똑같은 간격의 공간을 넣어준다.  
>>**space-between** - 왼쪽과 오른쪽 끝부분은 화면에 맞게 배치 후 아이템의 사이에만 공간을 넣어준다.  
			
      
># **align-items:**
>반대축에서 아이템을 배치한다.  
>>**center** 아이템들을 수직적으로 중심에 배치한다.  
>>**baseline** 텍스트가 균등하게 배치될 수 있도록 baseline에 맞춰서 아이템을 배치한다.  
      
># **align-content:**
>justify-content와 속성값은 동일하지만 중앙을 중심으로 배치된다.  


## Item에 적용되는 속성

># order:
>기본값은 0, order는 item의 순서를 지정하는 속성. 잘 쓰이지 않는다.  

># flex-grow:  
>컨테이너가 점차 늘어날 때 item이 어떻게 늘어나는 지 결정하는 속성이다. 
 
># flex-shrink:  
>컨테이너가 점차 줄어들 때 item이 어떻게 줄어들 지 결정하는 속성이다.  

># flex-basis:  
>auto는 grow나 shrink의 값에 따라 자동적으로 조절, 임의의 값을 입력하면 해당 값에 따라 컨테이너의 width에 따라 공간을 차지한다.  
	
  
># align-self:
>item별로 item들을 정렬 할 수 있다.  
>>flex-start  
>>flex-end  
>>center  


## FlexBox Guide

https://css-tricks.com/snippets/css/a-guide-to-flexbox/
