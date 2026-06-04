# Build Ideas

만들고 싶은 것들을 아카이빙하는 공간입니다.

## 아이디어 목록

| 상태 | 프로젝트 | 설명 |
|------|----------|------|
| 💡 | [LinkedIn + Instagram 자동 포스팅](#linkedin--instagram-자동-포스팅) | 아티클 읽고 대화 후 인사이트 자동 포스팅 |
| 💡 | [카드 이미지 자동 생성](#카드-이미지-자동-생성) | 대화 요약을 인스타 카드 이미지로 변환 |
| 💡 | [PPT 자동 생성](#ppt-자동-생성) | 목업/설명 기반으로 파워포인트 자동 생성 |

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

---

### PPT 자동 생성

**아이디어 배경**
목업 이미지나 텍스트 설명을 주면 python-pptx로 파워포인트 파일을 자동 생성.

**기술 스택**
- Python + python-pptx
- Claude API (내용 구성)
