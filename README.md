# 강의정리
### 공부 이유  :pencil2:
* 제대로 공부 안한 상태에서 쓰다보니 커밋이 수십 개가 되고 기록이 중구난방해짐
* 깃허브 쓸거면 제대로 쓰자
### 공부 자료  :pencil2: 
##### <a href= "https://www.inflearn.com/course/%EA%B9%83-%EC%9E%85%EB%AC%B8/dashboard"> <h3> ㆍ 인프런 - 지옥에서 온 관리자 Git </h3> </a>
___
## Git의 기본 원리
![image_1](https://user-images.githubusercontent.com/130421694/233297282-3a004bda-c6f8-42a6-9fec-c9cd61f1d2e1.png)
* 워킹 디렉토리 - 개발자가 작업하는 공간 
* 인덱스 - 커밋하기 전에 저장되는 임시 공간
	+ 트리 형태로 저장
	+ 이전에 작업한 형상은 사라지지 않고 덮어쓴 폴더에서 해시 값을 통해 참조
	+ 폴더 : 트리
	+ 파일 : BLOB 객체
* 헤더 영역 - 커밋하면 저장되는 공간
	+ 개발자가 작업한 파일들은 헤더 영역에서 pull, merge 등을 통해 형상 관리
___
## Git 초급
* git init - 현재 디렉토리를 git 영역으로 지정
* git add - 파일을 인덱스에 스테이징
	- . : 모든파일
	- 파일이름 : 지정파일
* git status - 파일 변경 상태 확인
* git commit -m "커밋 메세지" - 커밋 메세지를 남기면서 헤더 영역으로 커밋
	+ git commit --amend -m "변경 커밋 메세지" - 최종 로그 메세지 변경
* git log - 커밋 기록 확인
___
## Git 중급
* git reset - 인덱스 영역에서 커밋을 취소 및 커밋 기록 삭제
	+ soft - 커밋 기록만 삭제
	+ mixed - 커밋 기록, 인덱스 기록 삭제
	+ hard - 커밋 기록, 인덱스 기록, 파일 전부 삭제
		- 도착지 헤더 값

* git reflog - git reset hard로 삭제한 기록을 포함해서 한 번이라도 커밋한 내용을 모두 조회
___
## Git 고급
* git branch - 브랜치 확인
	+ branchName - 생성
* git checkout branchName - 브랜치로 이동
	+ -b : 생성과 함께 이동
* git merge branchName - 대상 브랜치를 현재 브랜치로 병합
	+ 두 브랜치의 분기점에서 현재 브랜치에 커밋 변경 기록이 있나?
		+ 없다 - fast-forward merge → 포인터 위치만 변경
		+ 있다 - 3-way merge → 공통 조상과 두 브랜치의 끝점, 세 점을 분석해 병합
* merge 충돌 - 3-way merge를 할 때 같은 파일의 내용이 다르면 merge 충돌이 일어남
	+ 2개 변경 사항을 모두 반영한 결과가 생성
	+ 개발자가 직접 수정해줘야 함 → 지양 사항
* git rebase -i HEAD~x - 현재 브랜치에서 x개 까지의 커밋 기록을 정리
	+ vi 에디터에서 편집
	+ 과거 기록만 pick, 나머지는 squash 치고 esc → :wq
	+ 새로 열린 창에서 지울 기록 지우고, pick 한 것만 남겨서 esc → :wq
___
## Github 사용법
* git remote add origin "깃허브 주소" - Github에 연결, 로컬에서는 origin으로 사용
	+ git ls-remote - 원격 연결 확인
	+ git remote rm origin - 원격 연결 끊기
* git push origin main - main 브랜치의 현재 커밋 상황을 Github에 등록
	+ 업로드 + 병합
* git pull origin main - 작업한 적이 있는 디렉토리에서 origin 내용 가져오기
	+ 다운로드 + 병합
* git clone "깃허브 주소" - 한 번도 작업하지 않은 디렉토리에서 원격 저장소 내용 가져오기
	+ git init + git remote add ~~~ + git pull
* git fetch - 깃허브의 브랜치 가져오기, 파일은 가져오지 않음
	+ 현재 작업 컴퓨터에 없는 깃허브의 브랜치를 받을 때 사용
* git checkout -b topic origin/topic - 브랜치 생성과 동시에 깃허브 브랜치를 병합
* git merge --squash topic - topic 브랜치를 현재 브랜치에 병합하면서 커밋 이력 하나로 합침
	+ git rebase 외에 커밋 내역 정리할 수 있는 명령어
	+ vi 에디터에서 작업할 필요 없어 편함
___
## Github 혼자 개발하기
* 브랜치 3개 이상 만들어서 작업
	+ main - 실제 서비스를 배포할 브랜치
	+ dev - 개발을 진행할 브랜치
	+ topic - 세부적인 작업을 진행할 브랜치, 완료되면 dev에 병합
* git merge --no-ff branchName - 병합 기록이 안남는 fast-forward merge 에서 병합 기록 남기고 병합
* git tag tagName - 브랜치에 태그 달기
* git tag -n - 태그 확인
* git push --tags origin main - 원격 저장소에 태그 남기기

---

