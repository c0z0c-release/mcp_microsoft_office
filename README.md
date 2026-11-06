microsoft office

설치: 릴리스의 `mcp_microsoft_office.exe` 를 실행합니다(서버 7개 내장). 서버 exe 는 `release\<버전>\<서버>\` 에도 있습니다.

## 버전 히스토리

새 버전은 이전 버전 **위쪽**에 `### <버전>` 제목으로 추가합니다. `push-release.ps1` 이 이 항목을 GitHub 릴리스 노트로 씁니다.

### 0.7.1

- 설치기 시작 시 GitHub 릴리스의 새 버전을 확인하고, 있으면 업그레이드할지 묻습니다(예 → 내려받아 SHA-256 검증 후 교체·재실행, 아니오 → 그대로 사용). 자동 업그레이드는 없습니다
- AI 클라이언트로 Claude Desktop 등록 지원(`--clients claude-desktop`, Microsoft Store 판과 일반 설치판 모두)
- 버전 표기를 `릴리스 버전.git 커밋 수`(예 `0.7.1.12`)로 변경. 설치기는 서버별 exe 버전을 비교해 설치/업데이트 상태를 표시
- 실행 파일이 아닌 파일을 서버로 띄우려 할 때 Windows 의 16비트 응용 프로그램 오류 창으로 자동 설치가 멈추던 문제 수정
- `todo_list_tasks` 설명 보강(status=open 에 InProgress/Waiting 포함, due=today 는 오늘 마감만)

### 0.6.2

- C# (.NET Framework 4.8) 단일 exe 서버 7개(excel, word, powerpoint, visio, outlook, outlook_todo, onenote)와 설치기 mcp_microsoft_office.exe
- 설치/제거 시 폴더를 잡고 있는 서버 프로세스를 강제 종료
