# {{asset_id}} · {{model_name}}

용도: {{role_and_level}}

상태: {{accepted_or_needs_review}} · 버전: {{version}} · 날짜: {{date}}

## 제작 이미지

### 정면 — 회색 형태 참고

![정면 클레이](front.png)

### 오른쪽 측면 — 회색 깊이 참고

![오른쪽 클레이](right.png)

### 후면 — 회색 구조 참고

![후면 클레이](back.png)

### 텍스처 정면 — 같은 형상의 표면 완성 목표

![텍스처 정면](textured_front.png)

네 이미지는 별도 파일입니다. textured_front.png는 UV 텍스처/PBR 맵이나 실제 완성 메시의 렌더가 아닙니다. 근사 개념도이므로 제작 치수는 아래 숫자를 우선합니다.

## 게임 크기와 제작 예산

| 항목 | 명세 |
| --- | --- |
| W(X) × D(Y) × H(Z), 게임 cm | {{w_cm}} × {{d_cm}} × {{h_cm}} |
| 플레이어/주변 에셋 비교 기준 | {{scale_context}} |
| 원본 디자인 단위와 게임 환산 | {{unit_conversion_or_already_game_cm}} |
| 축/정면 규약 | {{axes_and_front_direction}} |
| 피벗/접지 기준 | {{pivot}} |
| 별도 기능 부품/연결점 | {{functional_parts_or_none}} |
| 원본 버텍스 V 목표 | {{source_v_min}}–{{source_v_max}} |
| Quad Q 목표 | {{quad_min}}–{{quad_max}} |
| 게임 삼각형 T 상한 목표 | {{game_tri_max}} |
| 예산 선정 이유 | {{budget_rationale}} |
| BaseColor 권장 해상도, 목표 | {{texture_resolution}} |
| 대칭 활용/별도 변형 | {{symmetry_and_variants}} |

위 폴리곤 수는 제작 목표이며 이미지에서 측정한 값이 아닙니다. 엔진 render V는 UV·노멀 분리로 원본 V와 달라질 수 있습니다. Quad+삼각형 메시의 렌더 T는 2Q+원래 삼각형 수입니다.

## 반드시 유지할 큰 형상

{{large_shapes_counts_connections_and_landmarks}}

## 텍스처로만 표현할 디테일

{{texture_only_details_and_palette}}

## Tripo 제작 요청

회색 front/right/back는 같은 모델의 형태 참고이고 textured_front는 색·표면 참고입니다. 사용 중인 Tripo의 입력 방식에 맞춰 구분해 사용해 주세요. 간단한 저폴리 형상을 유지하고, 위의 표면 디테일 때문에 새로운 돌출부를 추가하지 마세요.

{{asset_specific_notes_openings_supports_no_invented_base}}

반환 요청: .blend 또는 Quad 유지 FBX/OBJ, 텍스처링 후 BaseColor PNG(추가 맵은 생성한 경우에만), 사용 단위·실제 W/D/H·V/Q/T 수·피벗 정보를 함께 주세요. GLB만으로는 Quad 보존을 확인할 수 없습니다. 원본 삼각형이나 열린 경계가 있다면 숨기지 말고 표시해 주세요.

## 검수와 남은 항목

- 시점·뷰 일치: {{view_qa}}
- 측면 깊이·실루엣·주요 구조: {{volume_qa}}
- 텍스처 전후 형상 일치: {{texture_geometry_qa}}
- 실제 파일 열기/크기: {{file_qa}}
- 생성/교정 시도와 남은 문제: {{attempts_and_open_issues}}

이미지 단계에서는 메시의 실제 버텍스, UV, 노멀, Quad 보존, 콜리전, 엔진·모바일 성능을 검수하지 않았습니다. 모델 반환 후 별도 확인이 필요합니다.
