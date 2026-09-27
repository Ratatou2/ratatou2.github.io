# 게시용 웹 파일 (ratatou2.github.io)

이 폴더는 `ratatou2.github.io` 저장소 루트에 그대로 복사해 게시하는 파일이다. 앱과 스토어가 아래 주소를 쓴다.

| 파일 | 게시 주소 | 쓰는 곳 |
|---|---|---|
| `app-ads.txt` | https://ratatou2.github.io/app-ads.txt | AdMob 앱 인증(이미 게시됨, 내용 동일) |
| `dailytodo/index.html` | https://ratatou2.github.io/dailytodo/ | 앱 홈페이지(OAuth 동의 화면 홈페이지로 권장) |
| `dailytodo/privacy.html` | https://ratatou2.github.io/dailytodo/privacy.html | 앱 Premium 화면, 고객 지원 화면, Play 개인정보처리방침, OAuth 동의 화면 |
| `dailytodo/terms.html` | https://ratatou2.github.io/dailytodo/terms.html | 앱 Premium 화면, 고객 지원 화면, OAuth 동의 화면 |
| `dailytodo/delete-data.html` | https://ratatou2.github.io/dailytodo/delete-data.html | Play 데이터 보안의 "데이터 삭제 요청" |
| `dailytodo/config/ads.json` | https://ratatou2.github.io/dailytodo/config/ads.json | 프로덕션 빌드의 `AD_CONFIG_URL`(광고 운영 설정) |
| `dailytodo/style.css` | (위 페이지 공용) | |

루트 `index.html`(기존 사이트)은 이 폴더에 없으므로 건드리지 않는다.

## 게시 전에 채울 값

페이지 안의 `［입력 필요: …］`를 모두 채운다. 운영자만 알 수 있는 값이라 추측으로 넣지 않았다.

| 값 | 들어가는 곳 | 비고 |
|---|---|---|
| 운영자 이름 또는 상호 | index, privacy(머리말, 영어 요약), terms | 개인이면 실명 또는 활동명, 사업자면 상호 |
| 시행일(YYYY-MM-DD) | privacy(2곳), terms | 게시하는 날 |
| 개인정보 보호책임자 이름 | privacy 9장 | 개인 운영이면 본인 |
| 사업자등록번호, 통신판매업 신고번호 | terms 머리말 | 해당 없으면 문구 삭제(국내 판매 의무 확인은 RELEASE_USER_ACTIONS D7) |
| 대상 연령 | privacy 6장 | Play 타겟층 설정과 같게 |
| 국외 이전 구체화 여부 | privacy 3장 | 법률 검토 권장. 필요 없으면 표시 줄 삭제 |
| 운영자 직접 환불 정책 | terms 3장 | 없으면 그 줄 삭제 |
| 유료 기능 변경 예고 기간 | terms 6장 | 예: 30일 |
| 관할 법원 | terms 8장 | |
| 구독 기록 삭제 처리 기한 | delete-data 3장 | 예: 요청 후 30일 이내 |

문의 이메일은 스토어 연락처로 등록된 `dev.tou2ggom@gmail.com`을 썼다. 바꾸려면 모든 파일에서 함께 바꾼다.

## 게시 절차

1. `ratatou2.github.io` 저장소를 받아 이 폴더의 `dailytodo/`를 저장소 루트에 복사한다(`app-ads.txt`는 이미 같은 내용이면 그대로).
2. 커밋, 푸시한다. GitHub Pages 반영까지 보통 1~2분.
3. 확인:
   - 브라우저로 위 표의 주소 5개가 열리는지(로그인 없이, 200).
   - `curl -s https://ratatou2.github.io/dailytodo/config/ads.json` 결과가 `{"adsEnabled": true, "dailyLimit": 2, "configVersion": 1}`.
   - 페이지에 `［입력 필요`가 남아 있지 않은지: `curl -s <주소> | grep -c '입력 필요'`가 0.
4. 광고를 끌 때: `ads.json`의 `adsEnabled`를 `false`, `configVersion`을 1 올려 푸시. 앱 캐시 15분 + GitHub Pages 캐시 약 10분 안에 반영.
