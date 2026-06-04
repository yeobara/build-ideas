# Build Ideas

만들고 싶은 것들을 아카이빙하는 공간입니다.

## 아이디어 목록

| 상태 | 프로젝트 | 설명 |
|------|----------|------|
| 💡 | [LinkedIn + Instagram 자동 포스팅](#linkedin--instagram-자동-포스팅) | 아티클 읽고 대화 후 인사이트 자동 포스팅 |
| 💡 | [카드 이미지 자동 생성](#카드-이미지-자동-생성) | 대화 요약을 인스타 카드 이미지로 변환 |
| 💡 | [PPT 자동 생성](#ppt-자동-생성) | 목업/설명 기반으로 파워포인트 자동 생성 |
| 💡 | [인스타툰 제작](#인스타툰-제작) | AI로 캐릭터 생성 + 일관성 유지하며 인스타툰 제작 |
| 💡 | [Rust 하드웨어 친화적 프로그래밍 학습](#rust-하드웨어-친화적-프로그래밍-학습) | Rust를 이용한 Data, Locality, Cache 최적화 학습 및 실습 |

---

## 프로젝트 상세

### LinkedIn + Instagram 자동 포스팅

**아이디어 배경**
아티클을 읽고 Claude와 대화를 나눈 뒤, 단순 요약이 아닌 내가 새로 깨달은 것과 느낀 점 위주로 LinkedIn/Instagram에 자동 포스팅하는 CLI 도구.

**워크플로우**
1. 아티클 입력 (URL 또는 텍스트)
2. Claude와 대화 — 내용 토론, 질문, 관점 탐색
3. `post` 명령어 입력
4. Claude가 대화에서 인사이트 + 느낀 점 추출 → 글 초안 작성
5. 내가 확인/수정 후 승인
6. LinkedIn / Instagram에 자동 포스팅

**기술 스택**
- Python + Claude API
- LinkedIn API (ugcPosts)
- Instagram Graph API (이미지 필수 → 카드 이미지 자동 생성과 연동)
- CLI 인터페이스

**참고**
- LinkedIn은 텍스트만 포스팅 가능
- Instagram은 이미지 필수 → 카드 이미지 자동 생성 프로젝트와 연동 필요
- Instagram은 비즈니스/크리에이터 계정만 API 사용 가능

---

### 카드 이미지 자동 생성

**아이디어 배경**
대화 요약이나 인사이트를 인스타그램용 카드 이미지로 자동 변환. LinkedIn + Instagram 포스팅 프로젝트와 연동.

**워크플로우**
1. Claude API로 핵심 문장 3~5개 추출
2. HTML/CSS 템플릿에 자동 삽입
3. Playwright로 브라우저 렌더링 후 이미지 캡처
4. 파일 저장 또는 바로 포스팅

**기술 스택**
- Python + Claude API (핵심 문장 추출)
- HTML/CSS 템플릿 (디자인)
- Playwright (이미지 캡처)

**왜 HTML → 이미지 방식?**
- CSS로 디자인 자유도 최고
- 인스타 카드 퀄리티 확보 가능
- 템플릿만 만들면 완전 자동화

**기성 CLI 툴 참고**
- `carbon-now-cli` — 코드 스니펫 이미지화
- `ImageMagick` — 텍스트 → 이미지 변환 CLI
- 딱 맞는 기성 툴 없음 → HTML + Playwright로 직접 구현이 현실적

**채널 리서치 (주말에 더 찾아볼 것)**

API가 지원되는 뉴스레터/블로그 플랫폼 비교:

| 플랫폼 | API | 특징 |
|--------|-----|------|
| **Ghost** | ✅ REST API | 블로그/뉴스레터 둘 다, 자체 호스팅 가능 |
| **Beehiiv** | ✅ API | 뉴스레터 특화, 기술 커뮤니티에서 인기 |
| **Hashnode** | ✅ GraphQL API | 개발자 특화, 기술 독자 노출 유리 |
| **Dev.to** | ✅ REST API | 개발자 커뮤니티, 알고리즘 노출 있음 |
| **Buttondown** | ✅ API | 뉴스레터 특화, 심플 |
| **Substack** | ❌ 없음 | 자동 포스팅 불가 |

**현재 방향**
- LinkedIn (짧은 인사이트 포스트) + Hashnode 또는 Beehiiv (긴 글) 병행 고려 중
- 주말에 각 플랫폼 API 문서 및 요금제 확인 필요

---

### 인스타툰 제작

**아이디어 배경**
AI로 캐릭터를 만들고 일관성을 유지하면서 인스타툰 제작. 간결한 그림체, 배경 생략.

**워크플로우**
1. Midjourney Niji로 캐릭터 시트 생성 (정면, 옆면, 주요 표정)
2. `--cref [캐릭터 시트]` 로 매 컷마다 캐릭터 일관성 유지
3. `white background, no background` 프롬프트로 배경 제거
4. Canva에서 컷 배치 + 말풍선 + 텍스트 추가
5. Instagram 업로드

**스타일 키워드**
- `flat illustration, simple line art`
- `webtoon style, minimal character design`
- `2D cartoon, clean lines`
- `white background, no background`

**툴**
- Midjourney Niji (캐릭터 생성, 수동)
- `--cref` (Character Reference, 일관성 유지)
- Canva (컷 편집)

**참고**
- Midjourney 공식 API 없음 → 수동으로 운영
- 자동화 원할 경우 Stable Diffusion + Niji 스타일 LoRA로 전환 가능

---

### PPT 자동 생성

**아이디어 배경**
목업 이미지나 텍스트 설명을 주면 python-pptx로 파워포인트 파일을 자동 생성.

**기술 스택**
- Python + python-pptx
- Claude API (내용 구성)

---

### Rust 하드웨어 친화적 프로그래밍 학습

**아이디어 배경**
Brian Bailey의 "All Software Is Hardware-Dependent" 아티클을 바탕으로, 생산성 위주의 고수준 추상화 뒤에 숨겨진 하드웨어(CPU, RAM, Cache) 제약을 이해하고, Rust를 통해 성능을 극대화하는 프로그래밍 패러다임을 체득하는 프로젝트.

**DLC 구조화 상세**

* **Data (데이터 구조 및 정렬)**
  * 메모리 정렬(Alignment)과 구조체 패딩(Struct Padding) 동작 원리 학습
  * Rust의 자동 필드 재정렬 최적화 분석 및 `#[repr(C)]`, `#[repr(packed)]` 등을 활용한 미세 레이아웃 제어
* **Locality (데이터 지역성)**
  * 범용 힙 할당자의 단편화 문제를 해결하기 위한 메모리 풀(Memory Pool) 및 아레나 할당자(Arena Allocator) 설계
  * 연속된 메모리 배치(`Vec<T>`)를 활용한 공간적/시간적 참조 지역성 극대화
* **Cache (캐시 효율화)**
  * 캐시 라인(Cache Line, 64B) 단위 탐색 효율성 극대화 (행 우선 vs 열 우선 비교 벤치마크)
  * 멀티스레드 환경에서 캐시 일관성 병목을 유발하는 거짓 공유(False Sharing) 문제 및 `CachePadded` 최적화 구현

**기술 스택**
- Rust (Cargo)
- Criterion.rs (벤치마크 측정용)
- Linux Perf / Valgrind (프로파일링 및 캐시 미스 관찰용)
