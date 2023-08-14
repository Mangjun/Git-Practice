# Git과 Github에 대해 공부
* 목표: 협업을 위한 기능들을 학습

## 학습하기 전 준비
* [Git 설치](https://git-scm.com/downloads)
* [Github](https://github.com/)
* [SourceTree 설치](https://www.sourcetreeapp.com/) → History 보기 편함

## 기본 명령어
```
git init // git이 이 디렉터리를 관리   
git add // 변경사항에 대해서 git이 추적   
git commit // 변경사항에 대해서 작업을 확정
```

## Github에 작업 올리기
```
git remote add 별명 [git repository 주소] // 현재 디렉터리를 git repository에 연결   
git branch -M master // master branch 생성   
git push 별명 master // master branch git repository에 업로드
```

## Git의 branch
* branch의 사용 이유
  * master branch는 현재 운영 중인 서비스의 소스코드로 사용되기 때문에
  * 협업을 하는 경우

* branch 기본 명령어
  ```
  git branch // 현재 branch 확인   
  git branch [branch 명] // branch 생성   
  git checkout [branch 명] // branch 변경
  ```

* merge 명령어
  ```
  git checkout master   
  git merge [병합할 branch 명]
  ```


## Pull Request
* PR이 필요한 이유
  * 협업에서 master branch에 merge를 사용하기 위해 필요

* PR을 사용한 업무 Flow
  1. local - 새로운 작업 branch에서 코드 작성
  2. local - 작업 완료 후 commit, push
  3. Github - 새로운 branch push 시, 저장소에 PR 만들기 버튼 표시
  4. Github - PR 생성
  5. Github - PR 메뉴에서 PR을 확인, 협업자들이 코드 리뷰 진행
  6. Github - merge 하기 버튼 클릭
  7. Github - master branch에 새로운 기능 적용

## Git의 rebase
* rebase 사용 이유
  * commit을 재배치하기 위해서(PR이 안될 경우)

* rebase 명령어
  ```
  // 충돌이 없는 경우(한 줄기)   
  git checkout [병합할 branch 명]   
  git rebase master   

  // 충돌이 있는 경우(여러 줄기)   
  git checkout [병합할 branch 명]   
  git rebase master // 충돌로 인해서 rebase 실패   
  // 직접 충돌 코드 정리   
  git add .   
  git rebase --continue
  ```

## Github 실전 협업
* 작업 Flow
  1. Github - 개발 진행할 repository fork
  2. local - fork한 repository를 local로 clone
  ```
  git clone [fork한 내 repository 주소]
  ```
  3. local - remote 명령어를 통해 upstream 생성
  ```
  git remote add upstream [개발 진행할 repository 주소]
  ```
  4. local - remote의 origin, upstream 확인
  ```
  git remote -v
  ```
  5. Github - 개발 프로젝트 내 작업할 issue 생성(티켓 생성)
  6. local - 작업 branch 생성
  7. local - 작업 후 commit
  8. local - 내 repository로 push
  9. Github - PR 생성 후 merge 완료
  10. local - master branch upstream pull 진행 후, origin의 master push 진행(origin 최신 소스 유지)

## Github 활용
* stash 명령어
  * 사용 이유: commit하기 전에 branch 변경 시
  * 명령어:
  ```
  git stash // 현재 작업 내용 임시 저장   
  git stash list // 임시 저장된 list 확인   
  git stash pop // 마지막에 저장한 작업 불러오기   
  git stash apply stash@{번호} // 특정 작업 불러오기
  ```

* branch 전략과 git flow 사용