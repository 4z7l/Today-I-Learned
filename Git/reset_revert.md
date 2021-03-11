# Git Reset

- 특정 commit을 사용하지 않게 되어 다시 되돌릴때
- 이전 commit 남기지 않고 새로운 commit 남김(revert는 이전 commit 남김)

|모드|의미|HEAD위치|인덱스|working directory|
|-|-|-|-|-|
|hard|- 인덱스 상태, working directory까지 모두 변경<br />- 커밋한적 없으면 복원 불가|변경|변경|변경|
|mixed|- 인덱스 상태 되돌림<br /><br />- git commit뿐만 아니라 git add 명령도 되돌림-  기본값|변경|변경|변경X|
|soft|commit만 되돌림|변경|변경 X|변경X|



# Git Revert

- 모든 변경사항을 취소하는 새로운 **commit**을 만드는거



# Reset vs Revert

- reset이 revert보다 history를 더 단순하게 만들어준다.
- 이미 remote에 push한 상태면 revert 해야함