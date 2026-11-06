microsoft office

설치: 릴리스의 `mcp_microsoft_office.exe` 를 실행합니다(서버 7개 내장). 서버 exe 는 `release\<버전>\<서버>\` 에도 있습니다.

## 버전 히스토리

새 버전은 이전 버전 **위쪽**에 `### <버전>` 제목으로 추가합니다. `push-release.ps1` 이 이 항목을 GitHub 릴리스 노트로 씁니다.

### 0.6.2

- C# (.NET Framework 4.8) 단일 exe 서버 7개(excel, word, powerpoint, visio, outlook, outlook_todo, onenote)와 설치기 mcp_microsoft_office.exe
- 설치/제거 시 폴더를 잡고 있는 서버 프로세스를 강제 종료
