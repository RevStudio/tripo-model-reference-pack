# 프롬프트 레시피와 이미지 검수

## 형태를 고정하는 짧은 설계 블록

모든 뷰에 동일한 identity block을 재사용한다. 모델 이름만 반복하면 뷰마다 새 디자인이 생기기 쉽다.

    Asset ID: {{id}}, {{subject}}.
    Target game dimensions: width X {{w_cm}} cm, depth Y {{d_cm}} cm,
    height Z {{h_cm}} cm. These dimensions describe the shape; DO NOT draw text.
    Silhouette and construction: {{large_masses_and_connections}}.
    Asymmetric landmarks in object coordinates: {{landmarks}}.
    Required negative spaces/openings: {{openings}}.
    Geometry details to retain: {{structural_details}}.
    Surface-only details to omit from clay: {{texture_only_details}}.
    Pivot/contact point: {{pivot_description}}.

빈 항목은 실제 모델에 맞춰 채우거나 제거한다. 버텍스 수를 프롬프트에 넣어도 정확한 토폴로지를 만들지는 못한다. 큰 덩어리·단순 단면·부품 개수로 시각적 복잡도를 제어하고 예산은 문서에 별도 기록한다.

## 축·시점 규약

기존 규약이 없으면 Z-up, 모델 정면 +Y, 모델 오른쪽 +X를 문서에 선언한다.

| 뷰 | 카메라 위치와 시선 | 보여야 하는 치수 |
| --- | --- | --- |
| front | +Y에서 -Y를 봄, 수평 | W(X)와 H(Z) |
| right | +X에서 -X를 봄, 수평 | D(Y)와 H(Z) |
| back | -Y에서 +Y를 봄, 수평 | W(X)와 H(Z) |

‘오른쪽’은 모델 기준이다. 이미지 화면 오른쪽과 혼동하지 않는다. 새 프로젝트가 다른 축을 쓰면 명세와 프롬프트 모두 변경한다. 이미지에 축 화살표를 그리지 않는다.

삼면도는 같은 캔버스/배경과 가능한 한 같은 투영 배율·바닥 기준선을 유지한다. 좁은 측면을 억지로 정면 너비에 맞춰 늘리지 않는다. 3장 모두에 전체 모델이 들어가는 여백을 확보한다. 실제 도구가 지원하는 해상도를 사용하고, 반환 크기를 측정한다.

## A. 정면 클레이

새 생성 요청에 identity block과 다음을 붙인다.

    Create ONE standalone front orthographic-style elevation of this asset.
    Camera is level at the front, no three-quarter rotation, no isometric view,
    no perspective convergence. Show the entire object including its contact
    points with clear margins, centered against a uniform light neutral backdrop.
    Simple matte medium-gray clay, broad economical low-poly masses,
    soft neutral studio lighting that reveals volume without dramatic shadows.
    No painted textures, wood-grain grooves, tiny modeled leaves or tile relief.
    Preserve functional openings and large silhouette-defining geometry.
    No wireframe, topology lines, text, measurements, arrows, panels, comparison
    sheet, labels, watermark, scenery, scale figure, or invented pedestal.

‘플레인’은 단순한 형태라는 뜻이다. 메시를 한 장의 plane으로 만들라는 의미가 아니다. 실제 모델 일부인 받침이나 기반은 허용하지만 임의 흙판/전시대는 추가하지 않는다.

## B. 오른쪽 클레이

채택 정면을 참조로 연결한다. identity block과 함께:

    Show the EXACT SAME asset from its object's RIGHT side, a genuine 90-degree
    camera change from the accepted front. Keep the object upright and camera
    level. The visible horizontal extent represents its DEPTH, not front width.
    Retain the same parts, heights, openings, connections, and asymmetry.
    Reveal the side structure described in the specification; do not redesign.
    Do not mirror, flatten, squeeze, or repaint the frontal image as a side view.
    Keep the clay material, background, framing scale and no-text restrictions.
    Output ONE standalone side elevation, not a combined sheet.

나무에는 필요 시 다음 구조 제약을 추가한다.

    The crown consists of thick closed low-poly volumes distributed around the
    trunk in depth, with distinct forward and rear branches. The right elevation
    must read as a full tree with specified front-to-back depth, not a thin disk,
    a fan in one plane, or edge-on foliage cards. Tiny leaves are texture detail.

## C. 후면 클레이

정면과 구조 판단에 필요한 채택 측면을 참조로 연결한다.

    Show the EXACT SAME asset from its BACK, a genuine 180-degree camera change
    from the accepted front, level camera. Preserve the same silhouette family,
    dimensions and connected parts. Respect the stated object-coordinate
    landmarks and which parts are occluded from behind.
    Do not paste front-only doors/windows onto the back. Do not treat a horizontal
    flip as proof of a rear view. Use the same neutral clay presentation.
    Output ONE standalone back elevation with no labels or other views.

정확히 대칭인 모델은 두 뷰가 비슷할 수 있다. 실제 구조를 유지하기 위해 대칭/비대칭 여부를 명세로 판단하며, 차이를 만들려고 장식을 새로 추가하지 않는다.

## D. 텍스처 정면

채택 front.png를 편집 대상으로 지정한다. 스타일 참조는 필요할 때만 추가하고, 어느 것이 형상 기준인지 명시한다.

    Edit the accepted FRONT clay reference into a textured appearance target.
    Its geometry is LOCKED: preserve the outline, framing, camera, proportions,
    openings, part count, visible surfaces, contact points and object orientation.
    Change only surface colors and painted material detail, following {{art_style}}.
    Represent {{texture_only_details}} as painted texture information without
    extrusions or new silhouette geometry. Preserve the plain neutral background.
    Soft neutral illumination, restrained highlights, readable midtones; no
    cinematic cast shadows, bloom haze, scene background, text or extra panels.
    This is one textured FRONT reference illustration, NOT a UV atlas or PBR map.

현대 HD2D 스타일 문구는 scale-budget-and-art.md의 예시 프리셋을 사용한다. 다른 프로젝트나 사용자 지정 스타일에 그 프리셋을 강제하지 않는다.

## 결함 기반 교정 예

교정에는 결함과 유지할 요소만 덧붙인다. 전체 디자인을 다시 발명하는 프롬프트로 바꾸지 않는다.

- 측면 나무가 납작함: “The side crown has collapsed into a thin plate. Restore the specified depth with forward/rear branches and thick crown volumes; keep the approved front design and total height.”
- 삼면도 합본 생성: “Return only the requested right elevation as ONE object on ONE canvas. Remove every other view, panel and label.”
- 텍스처에서 입체 기와가 생김: “Restore the smooth approved roof silhouette and planes. Paint tile seams on those planes; remove added tile extrusions and all new roof geometry.”
- 사선 정면이 측면으로 나옴: “The front face is still visible as a three-quarter view. Move to the exact object-right axis at level elevation; show depth versus height.”

수정 후 원래의 전체 QA도 다시 적용한다. 수정 한도를 넘겨 반복 생성하지 않는다.

## 실패를 숨기지 않는 기준

완전히 같은 3D 모델을 투영한 이미지가 아니므로 픽셀 정합이나 보이지 않는 구조를 보증하지 않는다. 눈에 띄는 부품 불일치·잘못된 시점·얇은 수관·텍스처 단계의 형상 변화는 needs_review다. 투영의 미세한 오차는 근사도임을 명시하되, 실제 제작을 오도하는 차이를 그 문구로 덮지 않는다.

Tripo에 제출할 때 각 파일의 역할을 구분한다. 사용 중인 제품이 지원하는 멀티뷰 입력 방식은 당시 UI/공식 문서로 확인하고, 네 이미지를 같은 종류의 생성 입력으로 무조건 함께 넣으라고 안내하지 않는다. textured_front.png는 별도 색·표면 참고이며 실제 텍스처링 UI나 API 지원을 가정하지 않는다.
