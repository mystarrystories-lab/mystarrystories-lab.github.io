# Jane 홈페이지

홈페이지: https://mystarrystories-lab.github.io/

## 에이전트 인수인계

전체 설정·요구사항·현재 구현·데이터 구조·검사·배포 절차는 [PROJECT_HANDOFF.md](PROJECT_HANDOFF.md)에 있습니다.
먼저 [AGENTS.md](AGENTS.md)를 읽습니다. 도구별 진입점: [Claude](CLAUDE.md), [Codex](CODEX.md),
[AGY](AGY.md), [Gemini/Antigravity](GEMINI.md), [Grok](GROK.md).

GitHub Pages는 `main` 브랜치의 루트 폴더를 배포합니다.
`index.html`, `style.css`, `app.js`를 수정합니다. JSON을 불러오므로 HTTP 서버로 미리 봅니다.

```powershell
python -m http.server 4173 --bind 127.0.0.1
```

브라우저에서 http://127.0.0.1:4173/ 를 열고, 확인 후 터미널에서 Ctrl+C로 서버를 종료합니다.

## 브랜치 작업 → PR → merge → 자동 배포

```powershell
git switch main
git pull --ff-only origin main
git switch -c update-homepage
# index.html 수정
git add index.html
git commit -m "Update homepage"
git push -u origin update-homepage
```

GitHub에서 Compare & pull request를 눌러 main으로 PR을 만들고 Merge pull request를 누릅니다.
Actions에서 배포 상태를 확인합니다. 작업마다 새 브랜치 이름을 사용합니다.
merge 후 로컬도 갱신합니다.

```powershell
git switch main
git pull --ff-only origin main
```

## main에 직접 push하기

```powershell
git switch main
git pull --ff-only origin main
# index.html 수정
git add index.html
git commit -m "Update homepage"
git push origin main
```

## 커밋 작성자 설정

아직 작성자 정보가 없다면 본인 정보로 한 번 설정합니다.
이메일은 GitHub의 비공개 커밋 이메일을 사용할 수 있습니다.

```powershell
git config user.name "본인 이름"
git config user.email "본인 GitHub 커밋 이메일"
```

첫 push에는 GitHub 로그인이 필요할 수 있습니다.
비밀번호와 API 키는 저장소에 올리지 않습니다.
