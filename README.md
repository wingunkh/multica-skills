# multica-skills

[Multica](https://multica.ai) 에이전트로 MSP(Managed Service Provider) 운영 업무를 처리하는 스킬 모음.

## 스킬

| 스킬 | 설명 |
|---|---|
| [msp-work-record](skills/msp-work-record/SKILL.md) | MSP 업무 메일 원문을 추적 가능한 업무 기록으로 정리 |
| [xlsx-work](skills/xlsx-work/SKILL.md) | 에이전트가 엑셀 파일을 망가뜨리지 않게 — 수식, 서식, 차트, 매크로 |

## msp-work-record

담당자가 고객사와 주고받은 메일 원문을 에이전트 채팅에 붙여 넣으면, 에이전트가 **요약, 요청, 발생, 확인, 조치, 후속** 여섯 개 레이블로 구조화한 기록을 만든다.

설계 원칙:

- **요약이 아니라 정리.** 정보 손실 없이, 모든 사실이 한 자리에만 들어간다.
- **식별자 보존.** IP, 경로, 계정, 에러 메시지는 원문 그대로 두고 자격증명은 마스킹한다.
- **Google SRE 포스트모템 템플릿 참고.** 원인 확정과 추정의 구분, 임시 조치, 후속 작업 주체, 경과 타임라인을 기존 레이블 구조 안에서 반영한다.

> 고객별 컨텍스트(기관명과 판단 단서)는 별도의 비공개 `org-context` 스킬에 있으며 이 저장소에 포함하지 않는다. 모든 예시는 가상 값이다.

## xlsx-work

LLM은 스프레드시트 작업에서 반복되는 몇 가지 방식으로만 실패한다. 수식 자리에 계산된 값을 박아 넣고, 계산된 적 없는 수식을 넘기고, 파일을 열고 저장하는 것만으로 차트·이미지·매크로를 지운다.

설계 원칙:

- **수식이 우선.** 계산 결과를 쓰지 않고, 값이 아니라 참조 범위를 검증한다.
- **저장 후 다시 연다.** 엑셀의 "복구된 레코드" 경고는 생성된 파일에서 가장 흔한 증상이다.
- **작업 전후로 센다.** 차트·이미지·피벗·병합·매크로를 원본과 비교하고, 사라진 것이 있으면 결과물을 버린다.

> 근거는 Anthropic의 [xlsx 스킬](https://github.com/anthropics/skills/blob/main/skills/xlsx/SKILL.md), openpyxl 공식 문서, LLM 스프레드시트 에이전트 벤치마크다.

## 구조

```
CHANGELOG.md
skills/
├── msp-work-record/
│   └── SKILL.md
└── xlsx-work/
    └── SKILL.md
```

## 버전 관리

각 스킬은 [Semantic Versioning](https://semver.org/)을 독립적으로 따르며, 저장소 전체 버전은 두지 않는다. 현재 버전은 각 `SKILL.md` 상단에 적혀 있고, 변경 내용은 [CHANGELOG.md](CHANGELOG.md)에 스킬별로 기록한다.
