# git 저장소 초기화 및 config 설정

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

# #
