# GitHub 저장소 연결 + Vercel 배포 가이드

## 1. Git 초기화 및 첫 커밋

프로젝트 폴더에서 터미널(PowerShell 또는 명령 프롬프트)을 열고 아래를 **순서대로** 실행하세요.

```bash
git init
git add .
git status
git commit -m "Initial commit: AI Tool Finder 정적 사이트"
```

- `git status`로 커밋될 파일을 확인한 뒤, `node_modules`나 `.env`가 포함되지 않았는지 확인하세요.
- `data/tools.db`를 저장소에 **포함**하려면 `.gitignore`에서 `# data/tools.db` 줄이 **주석 상태**인지 확인하세요.  
  **제외**하려면 해당 줄의 `#`를 제거해 `data/tools.db`를 저장소에서 빼세요.

---

## 2. GitHub 저장소 연결

1. **GitHub**에서 새 저장소(Repository)를 만듭니다.  
   - [github.com/new](https://github.com/new)  
   - 저장소 이름 예: `ai-tool-finder`  
   - "Add a README" 등은 체크하지 않고 **빈 저장소**로 생성해도 됩니다.

2. 생성된 저장소의 **URL**을 복사합니다.  
   - HTTPS: `https://github.com/사용자명/저장소명.git`  
   - SSH: `git@github.com:사용자명/저장소명.git`

3. 아래에서 **`YOUR_REPO_URL`** 자리에 복사한 URL을 넣고 실행합니다.

```bash
git remote add origin YOUR_REPO_URL
```

예시 (HTTPS):

```bash
git remote add origin https://github.com/myusername/ai-tool-finder.git
```

4. 기본 브랜치를 `main`으로 하고 푸시합니다.

```bash
git branch -M main
git push -u origin main
```

- 처음 푸시 시 GitHub 로그인 또는 토큰 입력이 필요할 수 있습니다.

---

## 3. Vercel 배포

1. [vercel.com](https://vercel.com)에 로그인 후 **Add New** → **Project** 선택.

2. **Import Git Repository**에서 방금 푸시한 GitHub 저장소(`ai-tool-finder`)를 선택합니다.

3. **Configure Project**  
   - Framework Preset: **Other** (또는 자동 감지된 그대로)  
   - Build Command: **비워 두기** (정적 사이트라 빌드 없음)  
   - Output Directory: **비워 두기**  
   - 그대로 **Deploy** 클릭.

4. 배포가 끝나면 `https://프로젝트명.vercel.app` 로 접속할 수 있습니다.  
   - 메인: `https://프로젝트명.vercel.app/`  
   - 관리자: `https://프로젝트명.vercel.app/admin.html` 또는 `https://프로젝트명.vercel.app/admin`

---

## 4. 설정 파일 요약

| 파일 | 역할 |
|------|------|
| `.gitignore` | `node_modules`, `.env`, (선택) `data/tools.db` 제외 |
| `vercel.json` | 루트 `/` → `index.html`, `/admin` → `admin.html` 매핑 |
| `package.json` | 프로젝트 메타정보 (빌드 스크립트 없음, 정적 사이트) |

이후 코드를 수정하면 아래만 실행해 다시 배포할 수 있습니다.

```bash
git add .
git commit -m "변경 내용 요약"
git push
```

Vercel이 GitHub와 연동되어 있으면 `git push` 시 자동으로 재배포됩니다.
