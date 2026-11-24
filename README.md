# tripo-model-reference-pack

Tripo(이미지 → 3D)에 넣을 레퍼런스 이미지를 매번 같은 규격으로 만들게 하는 에이전트 스킬입니다.
모델 하나에 이미지 4장과 명세 문서 한 장이 나옵니다.

| 파일 | 내용 |
| --- | --- |
| `front.png` `right.png` `back.png` | 회색 클레이 정면·오른쪽·후면. 뷰마다 따로 생성 |
| `textured_front.png` | 정면과 같은 형태에 색과 표면만 입힌 그림 |
| `spec.md` | 게임 cm 크기, 버텍스·Quad·삼각형 예산, 형태·텍스처 메모, 검수 결과 |

## 설치

에이전트의 skills 폴더 안에 이 저장소를 그대로 받습니다.

```
# Claude Code
git clone https://github.com/RevStudio/tripo-model-reference-pack ~/.claude/skills/tripo-model-reference-pack

# Codex
git clone https://github.com/RevStudio/tripo-model-reference-pack ~/.codex/skills/tripo-model-reference-pack
```

이미지를 새로 만들고, 기존 이미지를 참조해 편집할 수 있는 도구가 그 에이전트에 있어야 합니다.
도구가 없으면 스킬은 문서와 프롬프트까지만 준비하고 이미지 생성은 하지 않습니다.

## 쓰는 법

```
tripo-model-reference-pack 스킬로 이 모델의 회색 삼면도 3장과 같은 형상의 텍스처 정면 1장을 만들고,
게임 크기와 권장 버텍스 예산을 문서로 정리해 줘.
모델: 낡은 저수조, 153×172×215cm, 저폴리, 녹슨 철판 질감
```

## 들어 있는 것

- `SKILL.md` — 산출물 규칙, 작업 순서(정면 → 측면·후면 → 텍스처 정면), 최종 검수 항목, 폴더 구성
- `references/prompt-recipes.md` — 뷰별 프롬프트, 축·시점 규약, 결함별 교정 문장
- `references/scale-budget-and-art.md` — 크기·폴리곤 예산을 적는 기준과 프리셋 **예시**. 자기 프로젝트 값으로 바꿔 쓰세요
- `assets/model-spec-template.md`, `assets/vertex_budgets.csv` — 명세 문서 틀과 예산 표 머리글

## 알아 둘 점

- 세 뷰는 같은 3D를 투영한 그림이 아니라 따로 생성한 근사치입니다. 치수가 어긋나면 문서의 숫자가 우선입니다.
- 버텍스·Quad·삼각형 수는 제작 목표입니다. Tripo가 그 수를 맞춰 준다는 뜻이 아닙니다.
- Tripo 생성·업로드, Blender 메시 정리, 엔진 임포트는 이 스킬의 범위가 아닙니다.
