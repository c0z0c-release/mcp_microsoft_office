# microsoft office

AI 클라이언트(Claude Desktop, Claude Code 등)가 **지금 열려 있는 Microsoft Office 앱을 직접 조작**하게 해 주는 MCP 서버 모음입니다.
파일을 읽고 새로 쓰는 방식이 아니라, 사용자가 열어 둔 Excel/Word/PowerPoint/Outlook/OneNote/Visio 앱에 연결해 보고 있는 문서를 그 자리에서 편집합니다.

## 특징

- **열려 있는 문서를 그대로 편집**: 사용자가 화면에 띄워 둔 통합 문서·문서·프레젠테이션에 바로 반영됩니다. 파일을 내려받고 다시 올리거나 덮어쓸 필요가 없고, 결과를 화면에서 바로 확인하며 이어서 고칠 수 있습니다.
- **앱의 모든 기능 사용**: 서식, 차트, 피벗, 표, 도형, 수식, 변경 내용 추적 등 앱이 제공하는 기능을 그대로 쓸 수 있습니다. 용도별 도구로 부족하면 `com_*` 도구로 앱의 기능에 직접 접근할 수 있습니다.
- **저장·닫기·메일 초안도 도구로 제공**: 문서 저장과 닫기는 별도 도구(`*_save_*`, `*_close_*`)로 실행합니다. Outlook 은 메일 초안을 임시 보관함에 저장하고, 사용자가 Outlook 에서 확인한 뒤 전송합니다.
- **설치 한 번으로 등록**: 설치기가 서버 7개를 설치하고 AI 클라이언트 설정에 등록합니다. 별도 런타임 없이 단일 exe 로 동작합니다.

## 서버

| 서버 | 대상 | 주요 기능 |
| --- | --- | --- |
| excel | Excel | 셀·표 읽기/쓰기, 서식, 차트, 피벗, 조건부 서식, PDF/이미지 내보내기 |
| word | Word | 문단·표·머리글/바닥글, 스타일, 주석, 필드, PDF 내보내기 |
| powerpoint | PowerPoint | 슬라이드·도형·표·차트, 애니메이션, 노트, 테마, 내보내기 |
| visio | Visio | 도형·스텐실 기반 다이어그램 |
| outlook | Outlook(클래식) | 메일 조회, 초안 작성, 일정, 작업 |
| outlook_todo | Outlook 작업 | 할 일 목록, 작업 생성·완료, 플래그 메일 |
| onenote | OneNote | 노트북·섹션·페이지 편집, 표, 도형, 순서도 |

각 서버는 `api_guide` 도구로 작업별 사용법(레시피)과 도구 목록을 알려 주므로, AI 가 처음에 이 도구를 호출하면 올바르게 사용할 수 있습니다.

## 요구 사항

- Windows 와 해당 Microsoft Office 데스크톱 앱(Microsoft 365 Apps / Office 2024 기준). 앱이 설치되어 있지 않으면 `APP_NOT_INSTALLED` 오류로 알려 줍니다.
- Outlook 은 **클래식 Outlook** 이 필요합니다(새 Outlook 은 COM 을 지원하지 않습니다).
- 서버와 Office 앱은 **같은 권한 수준**으로 실행되어야 합니다. 한쪽만 관리자 권한이면 연결되지 않습니다.

## 설치

릴리스의 `mcp_microsoft_office.exe` 를 실행합니다(서버 7개 내장). 서버 exe 는 `release\<버전>\<서버>\` 에도 있습니다.

## 버전 히스토리

새 버전은 이전 버전 **위쪽**에 `### <버전>` 제목으로 추가합니다. `push-release.ps1` 이 이 항목을 GitHub 릴리스 노트로 씁니다.

### 0.7.2

- 서버 안내문과 도구 설명을 AI 가 기능 중심으로 이해하도록 정리: 문서 저장·닫기는 별도 도구, Outlook 메일은 초안으로 저장되어 사용자가 Outlook 에서 전송, 메일·작업 본문은 `include_body=true` 로 조회, `outlook_request_sync` 는 Outbox 의 메일도 함께 전송됨을 명시
- OneNote 안내에서 Excel/Visio 파일 삽입 도구와 `dry_run` 미리보기 사용법을 명확히 설명
- README 에 소개, 특징(열려 있는 Office 앱에 연결해 문서를 그 자리에서 편집), 서버 목록, 요구 사항 추가

### 0.7.1

- 설치기 시작 시 GitHub 릴리스의 새 버전을 확인하고, 있으면 업그레이드할지 묻습니다(예 → 내려받아 SHA-256 검증 후 교체·재실행, 아니오 → 그대로 사용). 자동 업그레이드는 없습니다
- AI 클라이언트로 Claude Desktop 등록 지원(`--clients claude-desktop`, Microsoft Store 판과 일반 설치판 모두)
- 버전 표기를 `릴리스 버전.git 커밋 수`(예 `0.7.1.12`)로 변경. 설치기는 서버별 exe 버전을 비교해 설치/업데이트 상태를 표시
- 실행 파일이 아닌 파일을 서버로 띄우려 할 때 Windows 의 16비트 응용 프로그램 오류 창으로 자동 설치가 멈추던 문제 수정
- `todo_list_tasks` 설명 보강(status=open 에 InProgress/Waiting 포함, due=today 는 오늘 마감만)

### 0.6.2

- C# (.NET Framework 4.8) 단일 exe 서버 7개(excel, word, powerpoint, visio, outlook, outlook_todo, onenote)와 설치기 mcp_microsoft_office.exe
- 설치/제거 시 폴더를 잡고 있는 서버 프로세스를 강제 종료
