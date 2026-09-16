# HANGULO_PACKAGE

HANGULO 배포 저장소. 앱 소스코드는 포함하지 않는다.

## 구조

- `feed/app.json` — 앱 업데이트 피드 (`version`, `url`, history[0]이 변경 내용)
- `feed/algo.json` — 알고리즘 업데이트 피드 (`version`, `url`, history[0]이 변경 내용)
- `feed/extra.json` — 추가기능용 URL·멘트 (`musicUrl`, `helpUrl`. 앱이 클릭 시 읽음)
- `feed/partner1.json`, `partner2.json`, `partner3.json` — 파트너 정보 3건 (아래 참조)
- Releases — 실제 배포 파일 (zip)

## 배포 파일

| 파일 | 내용 | 조건 |
|---|---|---|
| `Hangulo-v2.0.0-win64.zip` | 셀프컨테인드 (런타임 포함, ~72MB) | 그냥 실행 |
| `hangulo-algo-v1.0.0.zip` | 알고리즘 DLL + 사전 (`manifest.json` 포함) | 앱 내 업데이트로 적용 |

앱은 `feed/*.json`을 읽어 업데이트를 확인한다. 새 버전이 나오면 `version`·`url`을 갈아끼우고,
변경 내용은 `history` 맨 앞 항목의 `notes`에 적는다 (최상위 `changelog`는 쓰지 않음 — history 하나로 통일).
앱은 모르는 필드를 무시하므로 안전.

## 파트너 홍보 (partner1~3.json)

파트너 정보 버튼을 누르면 3개 파일을 병렬로 읽어 카드로 보여준다 (24시간 디스크 캐시).
각 파일 형식:

```json
{
  "ko": { "name": "이름", "url": "https://...", "desc": "설명" },
  "en": { "name": "Name", "url": "https://...", "desc": "Description" },
  "start": "2026-10-01T00:00:00+09:00",
  "end": "2026-10-31T23:59:59+09:00",
  "default": false
}
```

- `start`/`end`: 홍보기간 (ISO8601, KST `+09:00` 권장). `null` 또는 생략 = 무제한.
- 기간 안에 든 항목만 표시된다 (시작 전·종료 후 자동 숨김).
- 활성 항목이 하나도 없으면 `default: true`인 항목을 대신 보여준다 (텅 비는 일 없음 — 최소 1개는 `default: true` 권장).
- 3개 파일을 각각 수정하면 홍보 3건을 따로 관리할 수 있다.
