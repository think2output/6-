# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 이 폴더는
D6 수업 오전 미션 결과물. 공개 API를 부르는 **HTML 한 장짜리 화면**만 있다 (weather, rate, city, morning).
빌드·설치·테스트 도구 없음. 확인은 파일을 브라우저로 더블클릭해서 연다.
API 응답 확인은 `curl -s "<🔌 주소>"`로 한다. 만들기 전에 실제 응답 필드 이름을 curl로 먼저 본다.

## API 화면 규칙
- 키가 필요 없는 공개 API만 쓴다. 주소에 `key=`, `token=`, `apikey=`가 필요하거나 문서에 Authentication이 있으면 만들지 말고 "이 API는 키가 필요해서 D8 방식이 필요해요"라고 알려 줘. (왜: HTML은 누구나 코드를 볼 수 있어서 키가 새어 나감)
- API 주소는 파일 맨 위 `const API = { ... }` 한 곳에 모으고, 각 줄에 `// 🔌` 주석을 단다. `fetch` 하는 줄에도 `// 🔌 API 호출` 주석을 단다. (왜: 어디가 API인지 바로 찾으려고)
- 화면 맨 아래에 "🔌 이 화면이 쓰는 API" 상자를 두고, 실제로 부른 주소와 "새 탭에서 원본 JSON 보기" 링크를 보여 준다. (왜: 주소를 바꾸면 주문이 바뀌는 걸 눈으로 보려고)
- 카드마다 **로딩 중** 문구와 **불러오기 실패** 화면을 넣는다. 한 카드가 실패해도 다른 카드는 보이게 따로 부른다. (왜: 무료 API는 멈추거나 바뀜)
- 화면에 **데이터 출처**를 적는다. Open-Meteo는 "Weather data by Open-Meteo.com". (왜: API 규칙이 출처 표기를 요청함)
- 날짜가 있는 데이터(환율 등)는 **기준 날짜**를 함께 보여 준다. API 문서가 실시간이라고 하지 않으면 "실시간"이라고 쓰지 않는다. (왜: 환율은 하루 한 번 발표되는 기준값)
- HTML 파일 하나에 CSS와 JavaScript를 함께 넣는다. 더블클릭으로 열려야 한다. (왜: 설치 없이 바로 확인하려고)
- 커밋·푸시는 하지 말고, 커밋 메시지만 제안한다. 형식: `"[직군] D6: <미션> <이름>"` (왜: 세이브 포인트는 내가 검사한 뒤에 찍음)

## 기존 파일들이 따르는 공통 구조
- `<head>` 첫 `<script>`에 `const API` (주소가 위도·경도·통화 등에 따라 바뀌면 화살표 함수로 둔다). 동네가 고정된 화면은 `PLACE` 이름 상수도 함께 둔다.
- 본문 스크립트: `fetch`는 `getJson(url)` 한 곳에서만 하고 `res.ok`를 검사한다. 카드마다 `load___()` 함수가 로딩 → 성공 / `catch`에서 실패 상자 + "다시 시도" 버튼을 그린다.
- 색은 `:root` CSS 변수 + `prefers-color-scheme: dark` 재정의. 다른 화면을 만들 때 같은 변수 이름을 쓴다.
- 날씨 코드(WMO) → 한국어·이모지 표, 미세먼지 등급표는 파일마다 복사돼 있다 (파일 하나 규칙 때문). 하나를 고치면 나머지도 같이 고친다.

## API별로 이미 확인한 함정
- **Frankfurter**: `api.frankfurter.app`은 301로 넘어간다 → `https://api.frankfurter.dev/v1/latest?base=USD&symbols=KRW` 사용. 100엔은 `&amount=100`. 응답 `date`가 기준일 (ECB, 영업일 하루 한 번).
- **Open-Meteo 지오코딩**: 한국어 이름("서울", "부산", "수원시")은 0건이거나 엉뚱한 마을이 나온다. 영어("Seoul")로 찾고 `language=ko`로 한국어 이름을 받는다. 결과는 `population` 큰 순으로 정렬.
- **Open-Meteo 대기질**: `air-quality-api.open-meteo.com`, CAMS 1시간 모델 값. 환경부 등급(PM10 30/80/150, PM2.5 15/35/75)은 원래 24시간 평균 기준이라 "참고용"으로 표시.
- **Nager.Date**: 공휴일 이름은 `localName`(한국어) 우선, 없으면 `name`.
- **Dog CEO**: `message`가 사진 주소. 이미지 로드 실패(`img` error)도 실패 화면으로 처리.

## 실수에서 배운 규칙
<!-- AI 실수를 찾을 때마다 한 줄씩: - (날짜) (해라/하지 마라) ___ (왜: ___) → 검사: ___ -->
