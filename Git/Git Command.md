# git 활용하기

## core.autocrlf
git config --global core.autocrlf true (window)  
git config --global core.autocrlf input (mac)

운영체제 마다 에디터에서 줄바꿈이 다르기 때문에 리파지토리를 공유하는 경우 내가 수정하지 않아도 줄바꿈의 문자열이 달라져서 문제가 생길 수 있다.  
이를 해결해주는 것이 core.autocrlf 이다.  

## git Command
git 명령어(config, add ...) Option  

### git 생성 명령어
1. 진행할 프로젝트 디렉토리 생성  
2. 생성한 프로젝트 디렉토리 이동 - cd projects  
3. git 디렉토리 생성 - mkdir git  
4. git 디렉토리 이동 - cd git  
5. git 초기화 - git init (git 삭제 - rm -rf .git)  
   (init을 사용하면 숨겨진 폴더가 생성되며, 경로옆에 master 브랜치가 달린다.)  


### 만약 명령어를 단축해서 사용하고 싶다면?
`git config --global alias.(st status)`  
( )에 자신이 지정하고 싶은 축약어와 명령어를 입력하면 git st만 적어도 git status와 동일하게 작동한다.  

### 명령어의 정보
`git config --h`  

### 파일 추가하기
`git add`  

![git_add](https://user-images.githubusercontent.com/73509513/174749432-e8701c08-fdfc-4c03-957c-6c9828aad428.PNG)  

echo hello world! > a.txt를 작성하게 되면 hello world!가 적힌 txt파일이 생성되어진다.  
하지만 git status 명령어를 입력하게 Untracked files라고 나오게 되는데 이는 아직 commit할 수는 없지만 Untracked된 파일이 있어 git add로 track해 주어야 한다.  
git add a.txt 명령어를 입력하면 a.txt는 staging area 즉 commit할 수 있는 공간으로 이동되어 지고 commit을 할 수 있게 된다.  
(만약 여러개의 파일을 추가하고 싶다면 `git add a.txt b.txt` 나 `git add *.txt` 로 적어주면 된다.)  

혹시라도 파일을 수정하게 되면 modified 라고 나오게 되며 a.txt는 staging area에 올라와 있지만 추가된 내용은 working dirctory에 존재하게 된다.  
이는 다시 git add를 통해 staging area로 올려주면 된다.  

만약 `git rm --cached *` 로 삭제하게 되면 다시 Untracked files 즉  working dirctory로 옮겨지게 된다.  

`git add *` 을 하게 되면 staging area로 옮겨지게 된다.  

### gitignore

![git_ignore](https://user-images.githubusercontent.com/73509513/174749966-c6b9863d-c324-4026-acf8-75ca07851f76.PNG)

빌드안에 부수적으로 생긴 log파일 등을 git에 포함하지 않고 싶을때 gitgnore를 사용하게 된다.  
`echo *.log > .gitignore` 를 입력하게 되면 log 확장자를 포함하는 모든 것을 추가하지 않게 된다.  
특정한 디렉토리도 가능하며, 그 디렉토리 안에 있는 것도 가능하다 ex) `build/` , `build/*.log`  

### git status

![git_status](https://user-images.githubusercontent.com/73509513/174749550-b8115685-bbc5-45b4-8a90-6e4e6689c468.PNG)

status는 기본적으로 `--long` 옵션이 적용되어 있다.  
`git status -s` 를 입력하게 되면 간략한 상태를 볼 수 있다.  
초록색 A라고 적혀진 것은 파일이 추가가 되었으며, staging area에 올라온 commit이 가능한 상태를 말하며,  
빨간색 ??은 아직 tracking이 되지 않은 working dirctory에 존재하는 상태를 의미한다.  

이 상태에서 c.txt를 추가하게 되면 A옆에 M이라고 적혀져 있는데 추가한 파일이 아직 working dirctory에 존재한다고 알려준다.  

### git diff

![git_diff](https://user-images.githubusercontent.com/73509513/174749587-4491b660-f6d3-4c61-9ad3-848fe587f543.PNG)

파일을 비교하는 명령어이며, 정확하게 어떤 파일이 수정되어졌는지 확인하려고 할때 사용하는 명령어이다.  
`git diff` 만 입력하게 되면 working dirctory 에 있는 파일만 비교하게 된다.  

`diff --git a/c.txt b/c.txt`
a는 이전버전을 의미하며, b는 지금버전을 의미한다.  
`index 12a8798..311c32c 100644`  
index는 git 내부에서 파일을 참고할 때 쓰는 것이다.  
`--- a/c.txt`  
`+++ b/c.txt`  
`@@ -1 +1,2 @@`  
-는 --- a/c.txt 을 말하며 이전 파일의 첫째줄을 말하며, +는 +++ b/c.txt을 말하고 새로 변경된 사항인 1번째 ~ 2번째 줄까지 확인하라는 의미이다.  
 `hello world!`  
`+add`

줄이 추가가되면 초록색 +로 나오며, 만약 줄이 삭제된 경우 빨간색 -로 표시하게 된다.  

staging area에 올라온 것을 보고 싶다면  
`git diff --staged`를 입력하면 된다.  

##git commit

staging area에 있는 변경사항을 git 리파지토리에 옮겨주는 명령어이다.
아무 옵션도 입력하지 않으면 기본적으로 작성된 템플릿이 나온다.
기본적으로는 Title을 작성하고, Description(상세설명)을 작성한 후 저장하게 된다.

![git_commit](https://user-images.githubusercontent.com/73509513/174749706-7deee727-fbb8-4069-9d31-291daa3b1460.PNG)

`[master (root-commit) 65b5b0b] Title`
 `3 files changed, 3 insertions(+)`
 `create mode 100644 b.txt`
 `create mode 100644 c.txt`
 `create mode 100644 style.css`
저장하게 되면 명령창에는 해시코드 id와 title이 나오며, 아래에 만들어진 파일들이 나오게 된다.

이후 git log 를 입력하게 되면 누가 언제 만들었는지, 제목과 상세설명등이 나오게 된다.

![git_commit_second](https://user-images.githubusercontent.com/73509513/174749811-9fc3de43-17d5-454d-b921-f9cb6baa5c94.PNG)

`git commit -m "second commit"` 을 입력하게 되면 간단하게 commit을 하게 된다.

![git_commit_-a](https://user-images.githubusercontent.com/73509513/174749796-64244ec7-c33a-4544-a858-af8a522f4e04.PNG)

`git commit -am "third commit"` 을 입력하면 working dirctory에 있는 내용도 전부 commit할 수 있다.

commit을 할 경우 작업된 내용 전체를 할 것이 아닌 각각의 작업들을 하나하나 의미를 부여해서 commit하는 것이 좋다.

commit시 주의해야할 점은 commit시 고친 내용만 commit해야하며, 고친내용에 자기가 추가한 내용이나 다른 버그들을 고친 내용을 같이 commit해서는 안된다.
