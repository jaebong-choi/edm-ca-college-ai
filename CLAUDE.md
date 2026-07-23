# CLAUDE.md — 캐나다 공립 컬리지 진학 안내 사이트

## 프로젝트 개요
- 기존 호주 진학 안내 페이지(edm-au-ai, https://jaebong-choi.github.io/edm-au-ai/)의 구조·디자인을 그대로 유지한 채, **내용과 진단 로직만 캐나다 공립 컬리지용으로 교체**하는 프로젝트다.
- 정적 사이트(GitHub Pages 배포). 백엔드 없음.
- 상세 기능 명세는 `BUILD_SPEC.md`, 데이터는 `data/canada_colleges_data.json`, 근거 자료는 `docs/캐나다_공립컬리지_리서치_보고서.md`에 있다.

## 절대 규칙
1. **디자인·레이아웃·CSS는 변경하지 않는다.** 색상, 폰트, 섹션 배치, 애니메이션 모두 호주판 그대로. 텍스트·데이터·로직만 교체한다.
2. 작업 시작 전 반드시 기존 코드베이스(HTML/CSS/JS 구조, 진단 플로우 구현 방식, 결과 공유 링크 방식)를 먼저 분석하고 같은 패턴을 재사용한다.
3. 학비 데이터는 아직 검증 전이다. `tuition_intl: null`인 항목은 임의 금액을 넣지 말고 "상담 시 안내" 문구로 처리한다.
4. 이민·취업허가 관련 문구에 보장성 표현("영주권 보장", "100% 취업") 금지. 항상 "2026년 기준, 변동 가능" 단서를 유지한다.
5. PGWP 적격 여부 표기는 `data/canada_colleges_data.json`의 `major_categories[].pgwp_non_degree` 값만 근거로 사용한다. 임의 판단 금지.

## 브랜드 설정 (교체 지점 한 곳으로 모을 것)
JS 상단에 BRAND_CONFIG 객체를 두고, 로고·전화·상담 링크·카카오 링크를 여기서만 참조하게 리팩터링한다.
- 기본값: 클론한 호주판(edm)의 기존 값 유지
- 종로유학원 적용 시 교체값 예시: 상담 링크 `https://www.coei.com/info/consult/reserve.php`, 로고·카카오는 별도 전달 예정

## 파일 구조 (이 킷 기준)
```
/ (edm-au-ai를 복제한 새 리포 루트)
├── CLAUDE.md              ← 이 파일
├── BUILD_SPEC.md          ← 기능·카피·로직 상세 명세 (필독)
├── data/
│   └── canada_colleges_data.json   ← 권역·컬리지·전공·정책 데이터 (단일 소스)
├── docs/
│   ├── 캐나다_공립컬리지_리서치_보고서.md  ← 모든 수치·주장 근거
│   └── sources.jsonl
└── (기존 호주판 파일들: index.html, css, js, images ...)
```

## 작업 순서 (BUILD_SPEC.md 9절과 동일)
Phase 1 기존 코드 분석 → Phase 2 데이터 치환(JSON 연결) → Phase 3 진단 로직 구현 → Phase 4 카피 교체·검수 → Phase 5 로컬 확인 후 커밋. 각 Phase 완료 시 변경 파일 목록을 보고할 것.

## 커밋 컨벤션
- 한국어 커밋 메시지, Phase 단위로 커밋 (예: `Phase 2: 캐나다 컬리지 데이터 연결`)
- 이미지 등 대용량 에셋 추가 시 사전 확인 요청
