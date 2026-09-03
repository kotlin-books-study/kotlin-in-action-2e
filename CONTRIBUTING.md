# 참여 가이드

매주 **Pull Request**로 문제와 답변을 올립니다.
<br />
파일 양식은 [TEMPLATE.md](./TEMPLATE.md)를 참고하세요.

| 시점         | 무엇을                    |
|------------|------------------------|
| 스터디 **전**  | 내 파일에 문제 2개 작성하고 PR 열기 |
| 스터디 **시간** | 미리 생각해온 답을 발표·토론       |
| 스터디 **후**  | 내 파일에 답변 채우고 Merge     |

- 각자 **자기 파일 하나**만 작성합니다 (`chapter-02/hyunjung.md`)
- 그 파일에 내 문제 + 모든 문제에 대한 내 답을 적습니다 (상대 문제 답도 내 파일에)
- 상대 문제는 상대의 **PR 페이지에서 미리 읽고** 답을 준비합니다
- 브랜치·파일명은 영문(로마자)으로 통일합니다

## 스터디 전 — 문제

```bash
git checkout main && git pull
git checkout -b ch02-hyunjung
# chapter-02/hyunjung.md 에 내 문제 2개 작성 (답변 섹션은 비워둠)
git add . && git commit -m "docs: 2장 문제 - 현정"
git push origin ch02-hyunjung
```

그다음 GitHub에서 **Compare & pull request**로 PR을 엽니다. (제목 예: `[2장] 현정`)
<br />
해당 PR에서 문제를 읽고 답을 준비합니다.

## 스터디 후 — 답변

```bash
git checkout ch02-hyunjung
# chapter-02/hyunjung.md 의 '내 답변' 섹션 채우기 (내 문제 + 상대 문제 전부)
git add . && git commit -m "docs: 2장 답변 - 현정"
git push origin ch02-hyunjung
```

push하면 열려 있던 PR에 자동으로 추가됩니다.
<br />
확인 후 PR을 **Merge**하면 회차가 끝납니다.
