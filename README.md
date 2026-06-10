# 20419-2
# WRC (World Repair Championship) — Map Flag Subscription & Discovery System

<p align="center">
  <img src="https://img.shields.io/badge/React-18.x-61DAFB?style=flat-square&logo=react&logoColor=black" alt="React">
  <img src="https://img.shields.io/badge/Leaflet-1.9.4-199900?style=flat-square&logo=leaflet&logoColor=white" alt="Leaflet">
  <img src="https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?style=flat-square&logo=javascript&logoColor=black" alt="JavaScript">
  <img src="https://img.shields.io/badge/UI_Design-Sharp_Rectangular-ff69b4?style=flat-square" alt="UI">
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" alt="License">
</p>

> **수행평가 제출용 소프트웨어 요구사항 명세서 (SRS) 기반 프로젝트 레포지토리**
> 본 프로젝트는 소비자의 수리기사에 대한 접근성을 극대화하기 위해, 수리기사가 글로벌 지도에 구독 기반 깃발(마커)을 배치하여 자신을 실시간으로 홍보할 수 있는 **'위치 기반 수리기사 지도 구독 시스템'**의 기획 및 요구사항 정의서입니다.

---

##  목차 (Table of Contents)
1. [프로젝트 정보](#-프로젝트-정보-project-information)
2. [시스템 개요](#-시스템-개요-system-overview)
3. [주요 기능적 요구사항](#-주요-기능적-요구사항-functional-requirements)
4. [비기능적 요구사항 및 UI 제약](#-비기능적-요구사항-및-ui-제약-non-functional-requirements)
5. [유사 서비스 비교 분석](#-유사-서비스-비교-분석-competitive-analysis)
6. [사용자 시나리오](#-사용자-시나리오-user-scenarios)
7. [제한적 요소 및 리스크 관리](#-제한적-요소-및-리스크-관리-constraints--limitations)
8. [디렉토리 구조](#-디렉토리-구조-directory-structure)

---

##  프로젝트 정보 (Project Information)

* **학교/학과:** `[학교명 및 학과 입력 (예: OO고등학교 정보과학과)]`
* **개발자/기획자:** `[본인 이름 입력]`
* **문서 버전:** v1.3 (GitHub 배포판)
* **관련 법률 가이드라인 준수:** 개인정보 수집 및 동의 체계 포함 (GDPR · CCPA · PIPEDA 지원)

---

##  시스템 개요 (System Overview)

WRC 플랫폼의 **'지도 깃발 구독 및 탐색 시스템'**은 기술자와 소비자 간의 직거래 매칭을 유도하는 플랫폼 서비스입니다. 
* **수리기사(Technician):** 복잡한 입찰이나 광고비 경쟁 없이 **월 $19의 합리적인 가시성 구독료(Visibility Subscription)**만으로 글로벌 지도 상에 고유한 색상의 '깃발(Flag)'을 세우고 비즈니스를 홍보합니다.
* **소비자(Consumer):** 중개 플랫폼의 대기 시간 없이, 지도를 직관적으로 줌인/아웃하며 내 주변 수리기사의 깃발을 클릭하여 프로필을 확인하고 **즉시 전화를 걸어 다이렉트로 소통**합니다.

---

##  주요 기능적 요구사항 (Functional Requirements)

### 1. 구독 및 결제 제어 모듈
* **REQ-F-01 (결제 팝업):** 수리기사가 지도 노출 권한을 구매할 수 있도록 결제 수단을 선택하는 전용 **결제 모달(Payment Modal)** 창을 제공한다.
* **REQ-F-02 (권한 실시간 연동):** PG사 결제가 성공하면 데이터베이스의 `Flags Owned`(보유 깃발) 수치를 즉시 갱신하고 화면 우측 하단 HUD에 동기화한다.
* **REQ-F-03 (구독 만료 유효성 검사):** 1달(30일) 구독 기간 만료 시 자동으로 지도에 배치된 깃발 마커를 숨김(De-render) 처리한다.

### 2. 깃발 배치 및 프로필 등록 시스템
* **REQ-F-04 (지도 우클릭 이벤트):** 깃발을 보유한 기사가 Leaflet 지도 위 특정 지점을 **마우스 우클릭(Right-Click)** 하면 깃발 배치 인터페이스가 트리거된다.
* **REQ-F-05 (커스터마이징):** 수리기사는 전문 분야 구분을 위해 깃발의 색상(파랑, 빨강, 초록, 하양 등)을 커스텀 선택할 수 있다.
* **REQ-F-06 (홍보 리소스 업로드):** 상세 정보를 위해 최소 1장 이상의 사진 파일 업로드 기능과 텍스트 기반 소개글(Bio) 입력 폼을 제공한다.

### 3. 소비자 탐색 및 정보 출력 (TechPanel)
* **REQ-F-07 (위치 기반 필터링):** 소비자가 보고 있는 현재 지도 뷰포트(Viewport Bound)의 위도/경도 좌표 범위 내에 위치한 활성화된 깃발 마커들만 실시간으로 호출해 화면에 렌더링한다.
* **REQ-F-08 (TechPanel 슬라이드 구현):** 소비자가 특정 깃발을 클릭하면, 화면 측면에서 수리기사 정보 패널(`TechPanel`)이 슬라이드인 형태로 출력된다.
* **REQ-F-09 (정보 노출 범위):** 패널에는 수리기사 이름, 매장 사진 슬라이더, 평균 별점, 리뷰 개수, 소개글(Bio), **즉시 연락 버튼(전화번호/이메일)**이 반드시 포함되어야 한다.

---

##  비기능적 요구사항 및 UI 제약 (Non-Functional Requirements)

* **REQ-NF-01 [엄격한 UI/UX 제약]:** WRC 브랜드 아이덴티티 확립을 위해 시스템 전반의 모든 버튼, 모달, 입력 폼, 정보 패널은 둥근 모서리가 전혀 없는 **'완전한 직사각형(Sharp Rectangular UI)'**으로만 구현한다. (`css: border-radius: 0px` 필수)
* **REQ-NF-02 [초고속 지도 렌더링]:** 지도를 드래그하거나 축소/확대할 때, 영역 내의 새로운 깃발 데이터를 서버로부터 수신해 마커로 뿌려주는 시간은 **0.5초(500ms) 이내**여야 한다.
* **REQ-NF-03 [기술 스택의 경량화]:** 별도의 플러그인 설치 없이 브라우저에서 실행되어야 하며, 오픈소스 자바스크립트 지도 라이브러리인 **Leaflet.js**와 **React(v18)** 스택을 결합하여 가벼운 싱글 페이지 애플리케이션(SPA) 구조로 개발한다.

---

##  유사 서비스 비교 분석 (Competitive Analysis)

| 비교 항목 | **WRC 지도 깃발 구독 (본 프로젝트)** | **일반 지도 (구글맵 등)** | **견적 중개 플랫폼 (숨고 등)** |
| :--- | :--- | :--- | :--- |
| **비즈니스 모델** | **월 $19 고정 정액 구독제** | CPC 입찰 광고 (자본가 유리) | 견적서 발송당 차감 수수료 |
| **매칭 프로세스** | 지도 위 깃발 직관적 클릭  **즉시 직거래** | 검색어 입력 후 업체 리스트 나열 | 요청서 작성 전문가 견적 대기 |
| **매칭 속도** | **즉시 가능** (긴급 수리에 최적) | 보통 (영업 정보 확인 위주) | **느림** (평균 10분~수시간 대기) |
| **기사 수수료 부담** | **없음** (추가 인입에 따른 수수료 제로) | 매우 높음 (광고 상위 노출 경쟁) | 높음 (매칭이 실패해도 비용 발생) |

---

## 사용자 시나리오 (User Scenarios)

### Scenario 1: 수리기사의 비즈니스 홍보 및 깃발 배치
1. 스마트폰 수리 업자 '홍길동'은 WRC 앱 로그인 후 결제 모달을 통해 **월 $19 가시성 구독**을 결제한다.
2. 결제 완료 즉시 화면 우측 하단 HUD에 `Flags Owned: 1`이 반영된다.
3. 홍길동 기사는 지도 탭으로 가 매장 위치 좌표에 **마우스 우클릭**을 한다.
4. 설정 창에서 **'파란색 깃발'**을 고르고, 매장 사진과 *"아이폰 당일 액정 수리 15분"*이라는 Bio를 작성한 뒤 `Deploy`를 누른다.
5. 지도 상에 홍길동 기사의 깃발이 실시간으로 등록된다.

### Scenario 2: 소비자의 긴급 수리점 탐색 및 컨택
1. 대학생 '이영희'는 길을 걷다 노트북 화면이 깨지는 긴급 상황이 발생한다.
2. WRC 지도 웹페이지를 열고 현재 내 위치 주변을 확대(Zoom-in)한다.
3. 도보 50m 거리에 꽂힌 수리기사의 파란색 깃발을 발견하고 클릭한다.
4. 화면 우측에 `TechPanel`이 슬라이드 아웃되며 홍길동 기사의 평점(4.9), 리뷰 수, 매장 사진이 노출된다.
5. 이영희는 패널 속 **'Call'** 버튼을 눌러 기사님과 통화 후 즉시 매장으로 방문해 수리를 완료한다.

---

## 제한적 요소 및 리스크 관리 (Constraints & Limitations)

* **CON-01 (외부 PG 의존성):** 결제는 외부 API 연동이 필수적이므로 PG사 서버 장애 시 구독 결제 및 깃발 획득 기능이 마비될 수 있다.
* **CON-02 (데이터 과밀집 및 UI 파편화):** 서울, 뉴욕 등 중심 상가 지역에 수백 개의 깃발이 집중될 경우 마커가 겹쳐 클릭이 어려워지는 UX 저하 리스크가 존재한다. 향후 축소 레벨에 따라 마커를 묶어주는 **'클러스터링(Clustering) 알고리즘'** 고도화가 요구된다.
* **CON-03 (무료 지도 타일 서버 한계):** 오픈스트리트맵(OSM) 무료 타일을 사용할 경우 일일 트래픽 초과 시 지도가 깨질 수 있으므로, 상용화 단계에서는 Mapbox 등 유료 API 인프라 전환이 강제된다.

---

## 디렉토리 구조 (Directory Structure)

본 명세서가 구현될 실제 소스코드의 권장 디렉토리 아키텍처는 다음과 같습니다.

```text
wrc-map-flag-system/
├── public/
│   └── index.html          # Leaflet 및 React Script 로드 CDN 포함
├── src/
│   ├── components/
│   │   ├── MapContainer.jsx # Leaflet 지도 제어 및 우클릭 이벤트 바인딩
│   │   ├── TechPanel.jsx    # 슬라이드인 수리기사 상세 정보 패널 (Sharp UI 적용)
│   │   ├── PaymentModal.jsx # 월 $19 구독 결제 모달 인터페이스
│   │   └── StatusBarHUD.jsx # 우측 하단 Flags Owned 상태 표시줄
│   ├── styles/
│   │   └── global.css       # border-radius: 0px 등 공통 직각형 UI 스타일 정의
│   ├── App.jsx              # 전체 상태 관리 (Flags 상태, 패널 열림 상태 등)
│   └── main.jsx
├── README.md               # 본 프로젝트 문서
└── package.json
