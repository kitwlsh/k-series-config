# k-series-config

**K-시리즈 앱(KITWLSH) 공용 원격 설정 레포.** 각 앱이 실행 시 이 레포의 `family.json`을 읽어 '브랜드 & 자매앱' 카드를 **동적으로** 표시한다.

```
family.json          # 자매앱 레지스트리 (앱이 읽는 파일)
icons/*.png          # 자매앱 아이콘 (384×384 PNG)
```

## ⚠️ 규칙

- **Public 유지 / 브랜치 `main` 고정 / 파일 경로·이름 고정.** 아래 URL이 각 앱에 **컴파일타임 상수로 박혀 있어**, 바꾸면 모든 앱을 다시 배포해야 한다.
  ```
  https://raw.githubusercontent.com/kitwlsh/k-series-config/main/family.json
  ```
- **자매앱 추가 = `family.json`에 항목 1개 추가 + `icons/`에 PNG 업로드.** 앱 수정·재배포 없음. 각 앱은 최대 6시간 내(설정 화면 🔄로 즉시) 새 카드를 표시한다.
- **출시 상태 전환도 JSON만** 고친다: `active:false`(숨김) → `active:true, comingSoon:true`(🔜 출시 예정) → `comingSoon:false`(정상 카드).
- `id`는 **applicationId 대소문자 그대로**(KLotto = `com.kitwlshCom.klotto645`, 대문자 C 주의).
- `storeUrl`은 `https://play.google.com/`·`market://` 만, `iconUrl`은 https + `githubusercontent.com`/`github.io` 만 허용된다(앱이 그 외를 무시함).
- `_`로 시작하는 키는 주석이며 앱이 무시한다. 항목 상한 20개.
- 푸시 전 JSON 유효성 확인:
  ```bash
  python -c "import json;d=json.load(open('family.json',encoding='utf-8'));print('ok',len(d['apps']))"
  ```

## 📖 표준 문서

스키마·클라이언트 동작·보안 규칙·앱별 이식 절차는 각 앱 저장소의
`doc/KLOTTO_CONNECT_HANDOFF.md` **§8** (KDailyUtil · KLotto645 · KJangbu 동일 사본)에 있다.
