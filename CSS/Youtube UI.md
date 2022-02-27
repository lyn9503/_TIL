# 목표
지금까지 익힌 html, css를 활용해서 유튜브 UI를 비슷하게 제작  
유튜브 강의를 본 후 참고하지 않고 스스로 제작할 것.  

## 참고 유튜브 사진
![화면 캡처 2022-02-22 163058](https://user-images.githubusercontent.com/73509513/155086101-86860658-556b-4705-90f4-d3169bb83f79.png)

# 분할
![분할](https://user-images.githubusercontent.com/73509513/155086128-1587ce08-6979-411c-94bd-b43974164454.png)

# 1. 상단
## html
```
    <!-- 내비게이션 -->
    <nav class="navbar">
        <div class="navList">
            <a href="#" class="bar">
                <i class="fa-solid fa-bars"></i>
            </a>

            <a href="#" class="image">
            <i class="fa-brands fa-youtube"></i>
            </a>

            <span class="text">Premium</span>
        </div>

        <div class="navSearch">
            <input type="search" value="검색" >

            <a href="#" class="searchIcon">
                <i class="fa-solid fa-magnifying-glass"></i>
            </a>
            <a href="" class="searchMIC">
                <i class="fa-solid fa-microphone"></i>
            </a>
        </div>

        <div class="navIcon">
            <a href="#">
                <i class="fa-solid fa-video"></i>
            </a>
            <a href="#">
                <i class="fa-solid fa-ellipsis"></i>
            </a>
            <a href="#">
                <i class="fa-solid fa-bell"></i>
            </a>
            <a href="#">
                <i class="fa-solid fa-circle-user"></i>
            </a>
        </div>
    </nav>
```
nav 태그를 이용해 상단을 형성해주고, div를 이용해 이미지, 검색창 등등을 구성했으며, 아이콘은 무료 소스사이트에서 가져왔다.  

링크를 이용하는 부분은 a 태그, 검색을 위한 부분은 input 태그를 사용해 구현했다.

## css
```
/** nav **/
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 5px 10px;
  background: var(--backgroundColor);
}
.navList {
  display: flex;
  font-size: 1em;
}

.navList a {
  padding: 8px;
}

.navList .bar {
  color: var(--color);
}

.navList .image {
  color: var(--imageColor);
}

/**navList span .text**/
.text {
  display: flex;
  align-items: center;
  color: var(--color);
  font-size: 1em;
  margin-right: 1em;
  font-weight: bold;
}

.navSearch {
  display: flex;
  text-align: center;
  flex-basis: 50%;
  font-size: 0.8em;
}

.navSearch input {
  font-size: 1.1em;
  width: 100%;
  max-width: 800px;
}

.navSearch i {
  padding: 5px 10px;
  font-size: 1.1em;
  color: var(--color);
}

.searchIcon {
  background: var(--iconColor);
  outline: 0;
}

.navIcon {
  display: flex;
}

.navIcon a {
  text-decoration: none;
  padding: 3px 9px;
  margin-right: 16px;
  font-size: 0.8em;
  color: var(--color);
}
```
큰 틀이되는 nav는 flexBox로 만들어 justify-content: space-between; 을 이용해 각 요소들이 균등한 공간을 가지게 배치를 우선적으로 해주었고,  
요소들이 너무 윗쪽으로 치우쳐져 align-items: center; 를 사용해 행을 중심으로 중앙 정렬되게 해주었다.  

유튜브 이미지의 Premium은 원래는 유튜브 로고와 글자가 합쳐진 이미지이지만 구할 수 없어 text로 구현했으며, flex로 설정 후 목표 사진에 맞게 조절했다.  

input 태그는 원본 유튜브가 브라우저 창을 늘렸을 때 같이 늘어난 것을 파악해 max-width: 를 사용하여 최대 800px까지 늘어나도록 했다.  

맨 우측의 요소는 가져온 소스들을 이용해서 배치하였고 a 태그의 밑줄이나 색깔을 없애기 위해 text-decoration: none;을 사용해 없애 주었으며,  
padding, margin-right를 이용해 배치해 완성시켰다.  

![22](https://user-images.githubusercontent.com/73509513/155088897-f8d1194c-24d1-4512-aeff-feca8e5ab8bb.png)

# 2. 메인
## html
```
    <!-- 메인 -->
    <main>
        <!-- 비디오 -->
        <article class="player">
            <video controls src=""></video>
        </article>

        <!-- 해시태그 -->
        <article class="mainHash">
            <div class="tag1">
                <a href="#">#카트</a>
                <a href="#">#세계최초</a>
                <a href="#">#까까영상</a>
            </div>
            
            <!--영상 타이틀-->
            <div class="title">
                <span>ㄹㅇ 세계 최초 ㅋㅋㅋㅋ 🔥이것이 바로 『K-드리프트』 다!! ㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋ</span>
            </div>
        </article>
        
        <!-- 조회수 -->
        <article class="artView">
            <div class="view">
                <span>조회수 1,248회 : 2022.2.21</span>
            </div>
            
            <!-- 버튼 -->
            <div class="button">
                <button href="#">
                    <i class="fa-solid fa-thumbs-up"></i>
                    좋아요
                </button>

                <button href="#">
                    <i class="fa-solid fa-thumbs-down"></i>
                    싫어요
                </button>

                <button href="#">
                    <i class="fa-solid fa-share"></i>
                    공유
                </button>

                <button href="#">
                    <i class="fa-solid fa-arrow-down"></i>
                    오프라인 저장
                </button>
                
                <button href="#">
                    <i class="fa-solid fa-scissors"></i>
                    클립
                </button>
                
                <button href="#">
                    <i class="fa-solid fa-plus-minus"></i>
                    저장
                </button>
                
                <button href="#">
                    <i class="fa-solid fa-ellipsis"></i>
                </button>
            </div>
        </article>
        <hr/>
    </main>
```
영상이 들어가는 부분, 하단 유튜버 이미지와, 영상 제목으로 이루어진 부분 조회수, 버튼 등으로 구성되어진 부분 총 세 부분으로 나누었다.  

## css
```
/** main **/
.player {
  text-align: center;
  background: var(--playerColor);
}

.player video {
  width: 100%;
  height: 100%;
  max-width: 1200px;
}

.mainHash {
  display: flex;
  flex-direction: column;
  padding: 8px 20px;
}

.tag1 a {
  font-size: 0.6em;
  color: var(--fontColor);
  text-decoration: none;
}

.title {
  font-size: 0.8em;
}

.artView {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  padding: 2px 20px;
}

.view {
  font-size: 0.6em;
}

.button button {
  border: 0;
  outline: 0;
  font-size: 0.7em;
  background: var(--color);
}
```
브라우저가 늘어날 때 영상이 중앙에서 늘어나야 하므로 text-align: center; 를 사용해 늘어나도 중간을 유지하게 했으며, 
영상이 화면에 꽉 차게 보이도록 width와 height를 100%로 지정, 늘어날 때 max-width를 사용해 최대로 늘어날 수 있는 영상의 크기를 제한했다.  

제목 부분은 flex를 적용, 행으로 배치를 위해 flex-direction: column;을 사용해 주었고, 유튜버 이미지와 구분을 위해 padding으로 떨어뜨렸다.  

조회수와 버튼들은 열로 배치를 위해 flex를 적용, flex-direction을 row로, justify-content를 space-between을 사용해 양 옆으로 떨어뜨려 주었고, 
버튼들은 기본적으로 버튼 영역, 라인이 포함되어 border와 outline을 0으로 설정해 제거해 주었다.  

![33](https://user-images.githubusercontent.com/73509513/155095716-6fc0044d-dd90-4f6b-9ba8-e2059f45c479.png)

# 3. 하단
## html
```
    <!-- 하단 -->
    <footer class="footer1">
    
        <!-- 유튜버 정보 -->
        <div class="footerDiv">
            <img class="youImg" src="./dong.jpg">
            <div class="footerVal">
                <span class="name">동호형</span>
                <span class="sub">구독자 10.9 만명</span>
            </div>
        </div>
        
        <!-- 구독, 알림 여부 -->
        <div class="footerBtn">
            <button class="subing">
                <span class="subSpan">
                    구독중
                </span>
            </button>
            <button class="bell">
                <i class="fa-solid fa-bell"></i>
            </button>
        </div>
    </footer>
    
    <!-- 영상 설명 -->
    <footer class="footer2">
        <div class="value">
            <div class="tag2">
                <a href="#">#카트</a>
                <a href="#">#세계최초</a>
                <a href="#">#까까영상</a>
            </div>
            <span>
                영상 재미있게 보시고, 구독과 좋아요, 알림설정까지 부탁 드립니다!
            </span>
            <span>
                생방송 트위치 : <a href="https://www.twitch.tv/kimdh0630">https://www.twitch.tv/kimdh0630</a>
            </span>
        </div>
    </footer>
    
     <!-- 게임 정보, 찾기 -->
    <footer class="footer3">
    
        <!-- 게임 정보 -->
        <button class="footerBtn1">
            <div class="backColor">
                <img src="./channels4_profile.jpg" class="img1" align="left">
                <div class="span1">
                    <li>크레이지레이싱 카트라이더</li>
                    <li>2004</li>
                    <li>게임 찾아보기 ></li>
                </div>
            </div>
        </button>
        
        <!-- 게임 찾기 -->
        <button class="footerBtn2">
            <div class="backColor2">
                <img src="./photo.jpg" class="img2" align="left">
                <div class="span2">
                    <li class="li1">게임</li>
                    <li class="li2">모든 게임 찾아보기 ></li>
                </div>
            </div>
        </button>
        
    </footer>
```
유튜버의 정보와 구독자 수, 구독과 알림여부, 영상 설명등이 들어가 있다.  

## css
```
/** footer **/
.footer1 {
  display: flex;
  padding-left: 18px;
  flex-wrap: nowrap;
  justify-content: space-between;
}

.footerDiv {
  display: flex;
  flex-direction: row;
  align-items: center;
}

.youImg {
  border-radius: 70%;
}

.footerVal {
  display: flex;
  padding: 10px;
  flex-direction: column;
}

.name {
  font-size: 0.5em;
}
.sub {
  font-size: 0.5em;
}

.footerBtn {
  padding-right: 15px;
}

.subing {
  border: 0;
  outline: 0;
  font-size: 0.8em;
  padding: 10px;
}

.bell {
  border: 0;
  outline: 0;
  background: white;
  font-size: 0.8em;
  padding: 10px;
}

.value {
  display: flex;
  flex-direction: column;
  font-size: 0.6em;
  padding-left: 5.3em;
}

.tag2 a {
  font-size: 1em;
  color: var(--fontColor);
  text-decoration: none;
}

.footer3 {
  display: flex;
  padding-left: 3.11em;
  padding-top: 1em;
}

.footerBtn1,
.footerBtn2 {
  border: 0;
  outline: 0;
  width: 400px;
  background: var(--color);
}

.footerBtn1 {
  margin-right: 15px;
}

.backColor {
  background: var(--btnColor);
  height: 111.51px;
}

.backColor2 {
  background: var(--btnColor);
  height: 111.51px;
}

.img1 {
  width: 75px;
  height: 110px;
}

.img2 {
  width: 60px;
  height: 60px;
  border-radius: 70%;
  margin-top: 25px;
  margin-left: 15px;
}

.span1 {
  display: flex;
  flex-direction: column;
  align-items: baseline;
  padding: 10px 15px;
  list-style: none;
  font-size: 1.1em;
}

.span2 {
  display: flex;
  flex-direction: column;
  align-items: baseline;
  padding: 10px 15px;
  list-style: none;
  font-size: 1.1em;
}

li {
  line-height: 2.3em;
}

.li1,
.li2 {
  margin-top: 8px;
}
```
footer1에는 유튜버 이미지, 이름, 구독자 수 , 구독과 알림여부를 justify-content: space-between; 를 사용해 배치 했으며, 이미지를 원형으로 보이게  
border-radius: 70%;를 적용해 주었고, 유튜버 이름과 구독자의 수는 행으로 배치되게 flex-direction: column;를 사용해 적용, 중앙으로 정렬 해 주었다.

footer2에는 영상 설명을 flex를 적용, column을 사용해 행으로 배치해 나열 해 주었다.

footer3에는 게임 정보와 게임 찾기 이며, button 태그로 만들어 태그가 기본적으로 가진 border, outline을 제거하고 색상을 바꿔주었으며, 
width를 400px로 고정했고, 각 버튼에 들어가 있는 글씨들의 배치를 위해 display: flex;를 적용 후 column을 넣어 행으로 배치되게 해주었으며,
li 태그의 기본적인 스타일을 없애주기 위해 list-style을 없애주었다.

![44](https://user-images.githubusercontent.com/73509513/155095746-8e43811e-48cc-41f9-ae00-8011d5c50f9b.png)

## media 쿼리
```
@media screen and (max-width: 768px) {
  .navSearch {
    display: none;
  }
  .navView {
    flex-direction: column;
  }
  .view {
    display: none;
  }
}
```
768px (태블릿 사이즈) 이하로 내려 갈 시에 검색창이 보여지지 않게 display: none;을 적용해 가려주었다.

## 결과물
![66](https://user-images.githubusercontent.com/73509513/155095757-f126aed0-e3f5-4372-b279-94a42e68d718.png)  
![55](https://user-images.githubusercontent.com/73509513/155095751-1808525f-2948-43db-bd83-f1e2efb8f136.png)

## 코드
<details>
<summary>youtube.html</summary>
    
<div markdown="1">
    
```
<body>
    <!-- 내비게이션 -->
    <nav class="navbar">
        <div class="navList">
            <a href="#" class="bar">
                <i class="fa-solid fa-bars"></i>
            </a>

            <a href="#" class="image">
            <i class="fa-brands fa-youtube"></i>
            </a>

            <span class="text">Premium</span>
        </div>

        <div class="navSearch">
            <input type="search" value="검색" >

            <a href="#" class="searchIcon">
                <i class="fa-solid fa-magnifying-glass"></i>
            </a>
            <a href="" class="searchMIC">
                <i class="fa-solid fa-microphone"></i>
            </a>
        </div>

        <div class="navIcon">
            <a href="#">
                <i class="fa-solid fa-video"></i>
            </a>
            <a href="#">
                <i class="fa-solid fa-ellipsis"></i>
            </a>
            <a href="#">
                <i class="fa-solid fa-bell"></i>
            </a>
            <a href="#">
                <i class="fa-solid fa-circle-user"></i>
            </a>
        </div>
    </nav>

    <!-- 메인 -->
    <main>
        <!-- 비디오 -->
        <article class="player">
            <video controls src=""></video>
        </article>

        <!-- 해시태그 -->
        <article class="mainHash">
            <div class="tag1">
                <a href="#">#카트</a>
                <a href="#">#세계최초</a>
                <a href="#">#까까영상</a>
            </div>
            <!--영상 타이틀-->
            <div class="title">
                <span>ㄹㅇ 세계 최초 ㅋㅋㅋㅋ 🔥이것이 바로 『K-드리프트』 다!! ㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋ</span>
            </div>
        </article>
        <!-- 조회수 -->
        <article class="artView">
            <div class="view">
                <span>조회수 1,248회 : 2022.2.21</span>
            </div>
            <!-- 버튼 -->
            <div class="button">
                <button href="#">
                    <i class="fa-solid fa-thumbs-up"></i>
                    좋아요
                </button>

                <button href="#">
                    <i class="fa-solid fa-thumbs-down"></i>
                    싫어요
                </button>

                <button href="#">
                    <i class="fa-solid fa-share"></i>
                    공유
                </button>

                <button href="#">
                    <i class="fa-solid fa-arrow-down"></i>
                    오프라인 저장
                </button>
                <button href="#">
                    <i class="fa-solid fa-scissors"></i>
                    클립
                </button>
                <button href="#">
                    <i class="fa-solid fa-plus-minus"></i>
                    저장
                </button>
                <button href="#">
                    <i class="fa-solid fa-ellipsis"></i>
                </button>
            </div>
        </article>
        <hr/>
    </main>

    <!-- 하단 -->
    <footer class="footer1">

        <!-- 유튜버 정보 -->
        <div class="footerDiv">
            <img class="youImg" src="./dong.jpg">
            <div class="footerVal">
                <span class="name">동호형</span>
                <span class="sub">구독자 10.9 만명</span>
            </div>
        </div>

        <!-- 구독, 알림 여부 -->
        <div class="footerBtn">
            <button class="subing">
                <span class="subSpan">
                    구독중
                </span>
            </button>
            <button class="bell">
                <i class="fa-solid fa-bell"></i>
            </button>
        </div>
    </footer>

    <!-- 영상 설명 -->
    <footer class="footer2">
        <div class="value">
            <div class="tag2">
                <a href="#">#카트</a>
                <a href="#">#세계최초</a>
                <a href="#">#까까영상</a>
            </div>
            <span>
                영상 재미있게 보시고, 구독과 좋아요, 알림설정까지 부탁 드립니다!
            </span>
            <span>
                생방송 트위치 : <a href="https://www.twitch.tv/kimdh0630">https://www.twitch.tv/kimdh0630</a>
            </span>
        </div>
    </footer>

     <!-- 게임 정보, 찾기 -->
    <footer class="footer3">
        <!-- 게임 정보 -->
        <button class="footerBtn1">
            <div class="backColor">
                <img src="./channels4_profile.jpg" class="img1" align="left">
                <div class="span1">
                    <li>크레이지레이싱 카트라이더</li>
                    <li>2004</li>
                    <li>게임 찾아보기 ></li>
                </div>
            </div>
        </button>
        <!-- 게임 찾기 -->
        <button class="footerBtn2">
            <div class="backColor2">
                <img src="./photo.jpg" class="img2" align="left">
                <div class="span2">
                    <li class="li1">게임</li>
                    <li class="li2">모든 게임 찾아보기 ></li>
                </div>
            </div>
        </button>
    </footer>

    <hr/>
</body>
```
    
</div>
</details>


<details>
<summary>youtube.css</summary>
<div markdown="1">
    
```
:root {
  --color: white;
  --imageColor: red;
  --backgroundColor: rgb(44, 44, 44);
  --iconColor: gray;
  --playerColor: black;
  --fontColor: rgb(0, 81, 255);
  --btnColor: rgb(247, 247, 247);
}
/** body **/
body {
  margin: 0;
  font-size: 24px;
}
/** nav **/
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 5px 10px;
  background: var(--backgroundColor);
}
.navList {
  display: flex;
  font-size: 1em;
}

.navList a {
  padding: 8px;
}

.navList .bar {
  color: var(--color);
}

.navList .image {
  color: var(--imageColor);
}
/**navList span .text**/
.text {
  display: flex;
  align-items: center;
  color: var(--color);
  font-size: 1em;
  margin-right: 1em;
  font-weight: bold;
}

.navSearch {
  display: flex;
  text-align: center;
  flex-basis: 50%;
  font-size: 0.8em;
}

.navSearch input {
  font-size: 1.1em;
  width: 100%;
  max-width: 800px;
}

.navSearch i {
  padding: 5px 10px;
  font-size: 1.1em;
  color: var(--color);
}

.searchIcon {
  background: var(--iconColor);
  outline: 0;
}

.navIcon {
  display: flex;
}

.navIcon a {
  text-decoration: none;
  padding: 3px 9px;
  margin-right: 16px;
  font-size: 0.8em;
  color: var(--color);
}
/** main **/
.player {
  text-align: center;
  background: var(--playerColor);
}

.player video {
  width: 100%;
  height: 100%;
  max-width: 1200px;
}

.mainHash {
  display: flex;
  flex-direction: column;
  padding: 8px 20px;
}

.tag1 a {
  font-size: 0.6em;
  color: var(--fontColor);
  text-decoration: none;
}

.title {
  font-size: 0.8em;
}

.artView {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  padding: 2px 20px;
}

.view {
  font-size: 0.6em;
}

.button button {
  border: 0;
  outline: 0;
  font-size: 0.7em;
  background: var(--color);
}

/** footer1 **/
.footer1 {
  display: flex;
  padding-left: 18px;
  flex-wrap: nowrap;
  justify-content: space-between;
}

.footerDiv {
  display: flex;
  flex-direction: row;
  align-items: center;
}

.youImg {
  border-radius: 70%;
}

.footerVal {
  display: flex;
  padding: 10px;
  flex-direction: column;
}

.name {
  font-size: 0.5em;
}
.sub {
  font-size: 0.5em;
}

.footerBtn {
  padding-right: 15px;
}

.subing {
  border: 0;
  outline: 0;
  font-size: 0.8em;
  padding: 10px;
}

.bell {
  border: 0;
  outline: 0;
  background: white;
  font-size: 0.8em;
  padding: 10px;
}

/** footer2 **/
.value {
  display: flex;
  flex-direction: column;
  font-size: 0.6em;
  padding-left: 5.3em;
}

.tag2 a {
  font-size: 1em;
  color: var(--fontColor);
  text-decoration: none;
}

/** footer3 **/
.footer3 {
  display: flex;
  padding-left: 3.11em;
  padding-top: 1em;
}

.footerBtn1,
.footerBtn2 {
  border: 0;
  outline: 0;
  width: 400px;
  background: var(--color);
}

.footerBtn1 {
  margin-right: 15px;
}

.backColor {
  background: var(--btnColor);
  height: 111.51px;
}

.backColor2 {
  background: var(--btnColor);
  height: 111.51px;
}

.img1 {
  width: 75px;
  height: 110px;
}

.img2 {
  width: 60px;
  height: 60px;
  border-radius: 70%;
  margin-top: 25px;
  margin-left: 15px;
}

.span1 {
  display: flex;
  flex-direction: column;
  align-items: baseline;
  padding: 10px 15px;
  list-style: none;
  font-size: 1.1em;
}

.span2 {
  display: flex;
  flex-direction: column;
  align-items: baseline;
  padding: 10px 15px;
  list-style: none;
  font-size: 1.1em;
}

li {
  line-height: 2.3em;
}

.li1,
.li2 {
  margin-top: 8px;
}

@media screen and (max-width: 768px) {
  .navSearch {
    display: none;
  }
}

```
    
</div>
</details>

## 참고 강의
유튜브 사이트 따라 만들기(드림코딩) - https://www.youtube.com/watch?v=67stn7Pu7s4  

## 무료 소스
https://fontawesome.com/
