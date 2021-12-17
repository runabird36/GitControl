# git 명령어 사용방법 / github 연동

## [ user name / email 내용 저장 ]

```
  git config --global user.name "my name"
  git config --global user.email email
```

## [ commit 메세지 템플릿 저장 ]

- 해당 명령어 사용하기 이전에, 아래와 같이 linux명령어로 파일 생성
- touch .gitmessage.txt : 파일 생성
- vim .gitmessage.txt : 파일 내용 작성
- 해당 내용 참고 주소 [https://velog.io/@bky373/Git-%EC%BB%A4%EB%B0%8B-%EB%A9%94%EC%8B%9C%EC%A7%80-%ED%85%9C%ED%94%8C%EB%A6%BF](mailto:https://velog.io/@bky373/Git-%EC%BB%A4%EB%B0%8B-%EB%A9%94%EC%8B%9C%EC%A7%80-%ED%85%9C%ED%94%8C%EB%A6%BF)

  ```
  git config --global commit.template .gitmessage.txt
  ```

## [ git 저장공간 세가지 + 알파 구분 ]

- 실제공간 / stage 가상공간 / git directory / remote 공간 (github)

## [ local / git의 현재 상태 확인 ]

```
  git status
```

## [ Staging ]

```
  git add -A (지양)
  git add 파일명
```

## [ UnStaging ]

- 전체 파일 unstage

  ```
  git reset
  ```

- 지정된 파일 unstage

  ```
  git rm --cached 파일명
  ```

## [ Filter Staging ]

- .gitignore 파일 안에 지정된 포멧 / 파일 / 폴더 를 제외하고 staging하도록 필터링

## [ git directory 컨트롤 ]

- git directory에 실제 저장
- 이때서부터 실제 로그로 남음

  ```
  git commit : 만일 .gitmessage.txt 가 지정되어있으면 vim 메모장으로 전환
  git commit -m "메세지"
  ```

- 해당 로그보다 앞선 로그들을 강제로 강하게 삭제하고 원하는 로그로 이동

  ```
  git reset log_code(6-digits)(돌아갈 과거 로그) --hard
  ```

- 해당 코드의 로그로 돌아가는것이 아닌, 해당 로그 코드 바로 아래있는 코드로 돌아가되 새로운 로그로 쌓는것임

- 이때의 log_code는 꼭 가장 위에있는 log_code 이지 않아도 됨

- 나름대로의 정리가 끝나면 reset으로 최종 정리해도 됨

  ```
  git revert log_code(6-digits)(취소할 시점)
  ```

## [ Branch 컨트롤 ]

- branch는 생성 이후에, add해서 staging해준 뒤, commit을 통해 실제 git directory에 저장을 해줘야지 하나의 로그로 남는다.

- 브랜치 생성 (브랜치를 생성하는 시점을 기준으로, 가장 최신의 로그를 복사해서 새로운 브랜치로 생성)

  ```
  git branch branch_name
  ```

- 해당 이름의 브랜치로 이동

  ```
  git checkout branch_name
  ```

- 다 쓴 브랜치 삭제

  ```
  git branch -D branch_name
  ```

## [ Merge / Conflict / Rebase(재배치) ]

- 전제 1 : merge 할것을 : B (from)
- 전제 2 : merge 할것을 가져와서 합쳐질 공간을 : A (to)
- 라고 할때,

- A로 이동 후, B merge

- 이렇게 하면 (윈도우의 경우, vi 화면이 나옴 -> :wq)

  ```
  git checkout A
  git merge B
  ```

- conflict!

- 애초에 branch 의미단위를 잘 나누어서 같은 파일을 서로 다른 branch에서 수정하지 않도록 해야됨

- conflict 발생시!

  ```
  - git merge B 했을때,
  - conflict 된 부분을 보여줌
  - A, B 둘중 한군데를 수정 후, commit
    - git commit 만 해주기
  ```

- Rebase

- merge와 같이 지정한 브랜치를 하나로 합쳐줌
- 단, 하나 다른점은 git log --decorate --graph를 깔금하게 한줄로 만들어줌
- 팀 별 정책에 따라서 의논후 입력

  ```
  git rebase B
  ```



## [ remote 명령어 관련! / Fetch / Push / Pull ]

- 원격 저장소 경로를 변경할 때,
  ```
  -> git remote -v : 현재 원격저장소를 칭하고 있는 이름(remote_name) 확인 : origin
  -> git remote remove remote_name : remote_name과 연결된 remote 경로 삭제
  -> git remote add remote_name 깃주소 : 새롭게 지정할 remote 주소를 연결
  ```

- push 하기전에 현재 local git directory가 최신인지 확인 방법
- fetch와 pull의 차이 : 둘다 remote로 부터 가져오는것 이지만, 로컬 실제 데이터에 merge를 하냐 안하냐의 차이
  (pull 은 merge / fetch는 merge X)
  ```
  -> git fetch origin : origin 이라는 원격 저장소를 가져오되 merge는 하지 않겠다.
  -> git log --decorate --all --oneline : 어떠한 내용이 달라졌는지를, log들을 한줄로 정리해서 확인하겠다
  -> git diff HEAD origin/master : 어떠한 내용이 달라졌는지, 실제 내용을 뜯어보겠다.
  ```

- origin 이라는 remote repository(github)으로 master이라는 브랜치를 올리겠다.
  ```
  git push origin master
  ```

- origin 이라는 remote repository(github)으로 master이라는 브랜치를 받아오겠다.
  ```
  git pull origin master
  ```



## [ github 연동 ]

1. github에 repository 생성

2. 현재 로컬 git directory에 모든 내용이 commit되어있는지 확인
  ```
  git status
  ```
3. 현재 지정된 원격 repository가 있는지 확인 후, 없을 시 지정
  ```
  # 현재 지정되어있는 원격 저장소 확인
  git remote -v
  # origin 이라는 이름으로 원격 저장소 지정
  git remote add origin github원격저장소주소
  ```
4. origin 이라는 이름으로 지정된 원격 저장소에, master이라는 branch를 올리겠다
   (현재 main branch가 무엇인지 확인 필요. master 이라는 이름이 아닐수도 있음)
  ```
  # 현재 있는 branch 들 확인
  git branch
  # git push origin master
  ```
5. git pull origin master
