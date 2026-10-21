# GitHub Pages로 내 서비스 공개하기 (17:00~17:20)

> **GitHub Pages = 내 HTML을 무료로 걸어 두는 전시장.** 레포 설정 한 번이면 누구나 여는 링크가 생겨요.

## 공개 전 확인 3가지
- [ ] 레포가 **Public**이다 (무료 계정은 Public 레포만 Pages 가능)
- [ ] 레포 맨 위(루트)에 **`index.html`** 이 있다 — 이 파일이 첫 화면이 돼요
- [ ] **API 키, 비밀번호, 개인정보가 코드에 없다** — 오늘은 키 없는 API만 썼으니 안전해요

## 켜는 법
1. GitHub에서 `my-service` 레포 → 위쪽 **Settings**
2. 왼쪽 메뉴 **Pages**
3. **Build and deployment → Source**: `Deploy from a branch`
4. **Branch**: `main` / 폴더 `/ (root)` → **Save**
5. 1~2분 기다린 뒤 새로고침 → 위에 **"Your site is live at …"** 주소가 떠요
   - 주소 모양: `https://내아이디.github.io/my-service/`
6. 링크를 휴대폰에서도 열어 보기 📱

## 고친 다음엔?
main에 머지(또는 push)하면 **1~2분 뒤 자동으로** 링크에도 반영돼요.
안 바뀐 것 같으면: 레포 **Actions** 탭에서 초록 체크 확인 → 브라우저 강력 새로고침(`Ctrl+Shift+R` / `Cmd+Shift+R`)

## 안 될 때
| 증상 | 해결 |
| --- | --- |
| Pages 메뉴에 Branch 선택이 없어요 | 레포가 Private이에요 → Settings 맨 아래 **Danger Zone → Change visibility → Public** |
| 404가 떠요 | `index.html` 이름·위치 확인 (폴더 안에 있으면 안 됨, 대소문자 정확히) |
| 화면은 뜨는데 데이터가 안 와요 | `F12` → Console 확인. 주소가 `http://`로 시작하면 `https://`로 바꾸기 |
| 예전 화면이 보여요 | 1~2분 더 기다리고 강력 새로고침 |

## 왜 오늘은 공개해도 되고, D8은 다른 방법을 쓰나
- 오늘 API는 **회원 카드(키)가 없는 창구**라, 코드가 다 보여도 문제없어요
- GitHub Pages에 올린 파일은 **누구나 코드를 볼 수 있어요.** 키가 필요한 API를 여기 넣으면 키가 그대로 노출돼요
- 그래서 D8에서는 키를 서버 쪽에 숨기는 방법(Next.js + Vercel)을 배워요

## 제출
Slack에 링크 올리기: `[○조] 이름 · 서비스 이름 · https://...github.io/my-service/`
