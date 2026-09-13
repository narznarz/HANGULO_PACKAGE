# HANGULO_PACKAGE

HANGULO 배포 저장소. 앱 소스코드는 포함하지 않는다.

## 구조

- `feed/app.json` — 앱 업데이트 피드 (`version`, `url`, `changelog`)
- `feed/algo.json` — 알고리즘 업데이트 피드 (`apiVersion`, `url`)
- Releases — 실제 배포 파일 (zip)

## 배포 파일

| 파일 | 내용 | 조건 |
|---|---|---|
| `Hangulo-v2.0.0-win64.zip` | 셀프컨테인드 (런타임 포함, ~72MB) | 그냥 실행 |
| `Hangulo-v2.0.0-win64-fd.zip` | 프레임워크 종속 (~2MB) | .NET 9+ 필요 |
| `hangulo-algo-v2.zip` | 알고리즘 DLL + 사전 (`manifest.json` 포함) | 앱 내 업데이트로 적용 |

앱은 `feed/*.json`을 읽어 업데이트를 확인한다.
