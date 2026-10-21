# Issue(할 일 카드) → PR로 닫기

> **Issue = 레포에 붙이는 할 일 카드(포스트잇)**
> 카드 쓰기(Issue) → 작업(브랜치) → 결재 요청(PR) → 합치기(머지) → 카드 자동으로 닫힘

| 용어 | 비유 | 언제 배웠나 |
| --- | --- | --- |
| Issue | 할 일 카드 | **오늘** |
| 브랜치 | 그 카드를 작업하는 평행 우주 | D5 |
| PR | "다 했어요, 합쳐 주세요" 결재 요청 | D5 |
| 머지 | 결재 완료, main에 합침 | D5 |

## 1. 새 레포 만들기 (`my-service`)
1. GitHub → 오른쪽 위 **+** → **New repository**
2. 이름 `my-service` · **Public** (Pages 무료 공개에 필요) → Create
3. 내 컴퓨터로 받기
   - 명령어: `git clone https://github.com/내아이디/my-service.git`
   - GitHub Desktop: **File → Clone repository** → my-service
4. VS Code로 열고 Claude Code에게 뼈대를 만들게 해요 (`04_오후_나만의서비스_미션카드.md`의 14:10 프롬프트). Issue 양식(`.github/ISSUE_TEMPLATE/기능.md`)과 PR 양식(`.github/pull_request_template.md`)도 이때 같이 만들어져요
5. 만든 파일을 읽어 본 뒤 커밋·푸시: `"[직군] D6: 뼈대"`

## 2. Issue 쓰기
1. 레포 → 위쪽 **Issues** 탭 → **New issue** → **기능** 양식 선택
   - Issues 탭이 안 보이면: **Settings → General → Features → Issues** 체크
   - 양식이 안 나오면: `.github` 폴더가 푸시됐는지 확인 (GitHub 웹에서 폴더가 보여야 해요)
2. 제목: 무엇을 할지 한 줄 (예: "나라 고르면 현지 날씨 보이기")
3. 완료 기준: 눈으로 확인할 수 있는 문장 2~3줄
4. **Submit new issue** → `#1` 번호 확인 → 같은 방법으로 #2, #3

## 3. Issue 하나 = 브랜치 하나
| 하는 일 | 명령어 (Windows·Mac 같음) | GitHub Desktop |
| --- | --- | --- |
| 최신 받기 | `git switch main` → `git pull` | Current branch: main → **Fetch/Pull** |
| 브랜치 만들기 | `git switch -c feat/1-weather` | **Current branch → New branch** → `feat/1-weather` |
| 프롬프트로 만들기 | Claude Code에 Issue 내용 붙여 넣기 | (같음) |
| 저장 | `git add index.html` → `git commit -m "[직군] #1 날씨 보이기"` | 파일 체크 → Summary → **Commit** |
| 올리기 | `git push -u origin feat/1-weather` | **Publish branch** |

브랜치 이름 규칙: `feat/이슈번호-짧은영어` (예: `feat/2-rate`)

## 4. PR로 Issue 닫기
1. GitHub의 **Compare & pull request** (Desktop: **Create Pull Request**)
2. PR 양식이 자동으로 나와요 → 맨 위 `Closes #1` 번호 확인
3. **Files changed** 탭을 직접 한 번 읽기 (혼자 하는 레포라 이게 리뷰예요)
4. **Merge pull request** → **Confirm merge**
5. Issues 탭에서 #1이 **Closed**인지 확인 ✅ → 내 컴퓨터: `git switch main` → `git pull`

## 자주 막히는 곳
| 증상 | 해결 |
| --- | --- |
| PR에 `Closes #1`을 썼는데 안 닫혀요 | main으로 머지됐는지 확인 |
| Issues 탭이 없어요 | Settings → Features → Issues 체크 |
| Issue 양식이 안 나와요 | `.github` 폴더가 main에 푸시됐는지 확인 |
| Claude가 커밋·푸시까지 해 버려요 | 요청 끝에 "커밋은 제안만 해 줘" (CLAUDE.md 규칙 마지막 줄) |
| main에서 작업해 버렸어요 | 커밋 전이면 `git switch -c feat/1-weather` 하면 작업이 따라와요 |
