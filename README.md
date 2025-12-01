# 🗺️ Playce (플레이스) - 스포츠 중계 식당 탐색 지도 서비스

> **PLAY + PLACE = PLAYCE**
>
> **사용자 주변의 스포츠 중계 식당을 쉽게 탐색하고, 식당 운영자에게는 새로운 마케팅 기회를 제공하는 지도 기반 웹 서비스**

![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=Node.js&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=flat-square&logo=Express&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=MySQL&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=React&logoColor=black)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=TypeScript&logoColor=white)
![AWS EC2](https://img.shields.io/badge/AWS%20EC2-FF9900?style=flat-square&logo=Amazon%20EC2&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=Redis&logoColor=white)



<br>

<details>
  <summary><strong>목차</strong></summary>
  
1. <a href="#-1-프로젝트-개요">📌 프로젝트 개요</a><br>
&nbsp;&nbsp;1.1 <a href="#11-기획-의도">기획 의도</a><br>
&nbsp;&nbsp;1.2 <a href="#12-프로젝트-소개">프로젝트 소개</a><br>

2. <a href="#-2-주요-기능">🚀 주요 기능</a><br>

3. <a href="#️-3-기술-스택-및-아키텍처">🛠️ 기술 스택 및 아키텍처</a><br>
&nbsp;&nbsp;3.1 <a href="#31-기술-스택">기술 스택</a><br>
&nbsp;&nbsp;3.2 <a href="#32-아키텍처">아키텍처</a><br>

4. <a href="#️-4-erd--api-명세">🗂️ ERD & API 명세</a><br>
&nbsp;&nbsp;4.1 <a href="#41-erd">ERD</a><br>

5. <a href="#-5-내-역할-백엔드-상세">👨‍💻 내 역할 - 백엔드 상세</a><br>
&nbsp;&nbsp;5.1 <a href="#51-성능-최적화-및-부하-테스트-redis-k6">성능 최적화 및 부하 테스트 (Redis & k6)</a><br>
&nbsp;&nbsp;5.2 <a href="#52-기술적-접근-방식">기술적 접근 방식</a><br>

6. <a href="#-6-주요-트러블-슈팅-및-해결">🔥 주요 트러블 슈팅 및 해결</a><br>
&nbsp;&nbsp;6.1 <a href="#61-redis-캐싱-도입-후-서버-cpu-병목-해결">Redis 캐싱 도입 후 서버 CPU 병목 해결</a><br>
&nbsp;&nbsp;6.2 <a href="#62-express-기반-spa-배포-중-라우팅정적-파일-문제-해결">Express 기반 SPA 배포 중 라우팅/정적 파일 문제 해결</a><br>
&nbsp;&nbsp;6.3 <a href="#63-복합-지역-필터-로직-구현">복합 지역 필터 로직 구현</a><br>

7. <a href="#-7-프로젝트-회고-kpt">💡 프로젝트 회고 (KPT)</a><br>
</details>

<br>

---

## 📌 1. 프로젝트 개요

### 1.1 기획 의도
대중적인 지도 서비스에는 **스포츠 중계 필터**가 존재하지 않아, 스포츠 팬들은 원하는 경기를 함께 즐길 수 있는 장소를 찾는 데 어려움을 겪습니다. 또한, 경기를 중계하는 식당들도 이를 효과적으로 알릴 방법이 부족합니다. **PLAYCE**는 이러한 정보 불일치를 해소하기 위해 기획되었습니다.

### 1.2 프로젝트 소개
> **PLAYS + PLACE = PLAYCE**

PLAYCE는 **PLAY(스포츠 경기)**와 **PLACE(장소)**의 합성어로, 사용자 주변의 **스포츠 중계 식당을 쉽게 탐색**할 수 있도록 돕는 지도 서비스입니다. 식당 위치, 경기 종목, 팀 등을 바탕으로 최적의 장소를 검색할 수 있으며, 기존 서비스에는 없던 스포츠 경기 중계 일정을 확인할 수 있습니다.

### 1.3 활용 방안 및 기대 효과
* **스포츠 팬의 장소 검색 도구**: 경기 일정과 위치를 기반으로 편리하게 관람 장소 탐색 가능.
* **식당의 마케팅 활용**: 스포츠 중계 일정을 등록하여 새로운 고객 유입 및 매출 극대화 가능.
* **스포츠 문화 활성화**: 함께 응원하며 경기를 시청하는 문화를 활성화하고, 지역 기반 스포츠 커뮤니티 플랫폼으로 확장 가능.

| 항목 | 내용 |
| :--- | :--- |
| **개발 기간** | 2025.06.18 ~ 2025.07.18 (4주) |
| **팀 구성** | 6인 팀 프로젝트 (Frontend 3명, Backend 3명) |
| **담당 역할** | 백엔드: 중계 일정 / 검색 API 개발, **k6 부하 테스트 & Redis 캐싱 전략 수립 및 구현** |

<br>

---

## 🚀 2. 주요 기능
| 기능 분류 | 설명 | 스크린샷 |
| :---: | :--- | :---: |
| **지도 및 검색** | - **카카오맵 API**로 지도 서비스 제공. <br> - 마커 클릭 시 식당 기본 정보 확인 가능. <br> - **필터링**: 식당 이름, 지역, 경기(종목, 리그)별 검색 지원. <br> - **정렬**: 거리순, 날짜순 정렬 제공. |  |
| **식당 상세 정보** | - 지도 마커 또는 검색 결과 클릭 시 진입.<br> - 기본 정보, 메뉴, 사진, **중계 일정** 등 상세 정보 확인. |  |
| **식당/일정 관리** (Admin) | - **식당 등록**: 사업자등록번호, 주소 등 유효성 검사 진행. <br> - **중계 일정 관리**: 날짜별 탭 리스트 및 캘린더를 통한 일정 등록, 수정, 삭제. | 

[Image of broadcast management page]
 |
| **마이페이지** | - 즐겨찾기 목록 조회 및 삭제.<br> - 등록 식당/중계 일정의 목록 조회 및 관리. |  |

<br>

---

## 🛠️ 3. 기술 스택 및 아키텍처

### 3.1 기술 스택
| 구분 | 기술 스택 |
| :--- | :--- |
| **프론트엔드** | **TypeScript**, React, **Zustand** (상태 관리), **Tailwind CSS** |
| **백엔드** | **TypeScript**, Node.js, Express, **MySQL**, **TypeORM** (ORM) |
| **주요 서비스** | **카카오맵 API**, **AWS S3** (이미지 서버), **Redis** (캐싱), **k6** (성능 테스트), **AWS CloudWatch** (모니터링), **AWS EC2** (배포) |

### 3.2 아키텍처
안정적인 서비스 제공을 위해 AWS EC2 인스턴스에 백엔드를 배포하고, Redis를 캐시 계층으로 두어 데이터베이스 부하를 분산했습니다.


<br>

---

## 🗂️ 4. ERD & API 명세

### 4.1 ERD
서비스의 핵심 도메인인 **User, Store, Broadcast, Region**을 중심으로 관계형 데이터베이스를 설계했습니다.


<br>

---

## 👨‍💻 5. 내 역할 - 백엔드 상세

### 1. DB 설계 및 구축
- 서비스 핵심 테이블(중계 일정, 식당 정보, 사용자 정보) 설계 및 구축.
- **TypeORM**을 활용하여 관계형 데이터 구조 기반으로 구현.

### 2. 중계 일정 및 검색 관련 API 개발
- 식당 중계 일정 등록, 수정, 삭제 API 개발.
- **반경 기반 위치 검색, 필터 기반 검색, 다중 조건 검색 API** 구현.

### 5.1 성능 최적화 및 부하 테스트 (Redis & k6)

잦은 조회와 복잡한 필터링이 필요한 **중계 일정** 및 **통합 검색** API에서 성능 병목을 확인하고, **Redis 캐싱 전략**을 도입하여 문제를 해결했습니다.

| API | 요청 수 증가 | 평균 응답 시간 감소 | 95% 응답 시간 감소 |
| :--- | :--- | :--- | :--- |
| **중계 일정 조회** | 26,053건 → **266,000건** (10배↑) | 12.49초 → **1.16초** (90%↓) | 41.27초 → **2.41초** |
| **통합 검색 API** | 131,705건 → **656,230건** (5배↑) | 1.52초 → **504ms** | 3.53초 → **1.03초** |

### 5.2 기술적 접근 방식
- **Redis 캐싱 계층 도입**: 데이터베이스 조회 전단에 Redis를 배치하여 자주 조회되는 중계 일정 및 검색 결과를 캐싱.
- **TTL(Time-To-Live)** 설정: 데이터의 최신성을 유지하며 캐시 활용.
- **캐시 미스 대응**: 미스 발생 시 DB 조회 후 Redis에 데이터 갱신.

<br>

---

## 🔥 6. 주요 트러블 슈팅 및 해결

### 6.1 Redis 캐싱 도입 후 서버 CPU 병목 해결
**문제 상황**: Redis 캐싱 도입 후 DB 부하는 감소했지만, **Node.js 서버의 CPU 사용률이 급증**하여 평균 응답 속도 증가 및 서버 응답 지연 발생 (k6 부하 테스트 확인).

**원인 분석**:
1. 캐시된 데이터 처리 과정에서 발생하는 **JSON 역직렬화 비용** 및 **조건 필터링 로직**으로 인한 CPU 사용량 증가.
2. Node.js의 **단일 스레드** 환경에서 병목 발생.
3. Redis 인증 처리 시 `userId` 타입 불일치로 인한 반복 인증 실패.

**해결 방안**:
1. **JWT 사용자 인증 캐싱 적용**: Redis를 통한 JWT 사용자 인증 캐싱으로 반복 인증 시 **DB 쿼리 제거**.
2. **타입 통일**: `storedUserId.toString() === decoded.userId.toString()` 비교로 **타입 불일치 문제 해결**.
3. **K6 최적화**: K6 테스트 시 사전 로그인 처리(Pre-login)로 최초 로그인 쿼리 제거.

**성과**: 평균 응답 속도 **200ms → 80ms**로 개선, **DB 호출 횟수 평균 78% 감소**.

### 6.2 Express 기반 SPA 배포 중 라우팅/정적 파일 문제 해결
**문제 상황**: SPA 클라이언트 새로고침 시 **404 Not Found 에러** 발생 및 정적 파일(JS, CSS) 로드 실패. Express 5 버전에서 와일드카드 사용 오류 발생.

**원인 분석**:
1. 정적 파일 경로 지정 오류 (`__dirname` 기준 상대 경로 문제).
2. 클라이언트 라우터 핸들러 (`app.get("*")`)가 **404 핸들러보다 뒤에 위치**.
3. Express 5에서 와일드카드 파라미터 명시 필수 (`:paramName`).

**해결 방안**:
1. **절대 경로 명확화**: `path.resolve(__dirname, "../../public")`을 사용하여 정적 경로 명확화.
2. **라우팅 순서 조정**: 클라이언트 라우터 핸들러를 404 핸들러보다 **먼저 배치**.
3. **Express 5 대응**: `app.get("/{*any}")`로 변경하여 와일드카드 오류 해결.

### 6.3 복합 지역 필터 로직 구현
**문제 상황**: 통합 검색 시 `big_regions` (서울, 경기)와 `small_regions` (중구) 조합 조건 처리가 복잡하여, 단순 `IN` 조건으로는 의도한 필터링 불가 (예: 서울 중구 + 경기 전체를 조회해야 하는데, 서울 중구 + 경기 중구만 조회됨).

**고민 포인트**:
- `small_region`이 있는 경우, 해당 `big_region`도 함께 고려해야 하는 다층적 조건.

**해결 방법**:
1. **TypeORM Brackets 사용**: 복잡한 **OR (A AND B)** 또는 **OR C**와 같은 논리 조합을 처리하기 위해 **TypeORM의 `Brackets`** 활용.
2. **조건 분기**: `small_region`이 주어진 경우와 아닌 경우를 분기하고, `smallRegion`에 해당하지 않는 나머지 `bigRegion`은 `OR` 조건으로 포함하여 원하는 **조합 조건**을 정확히 구현.

**배운 점**: 단순 DB 조건으로는 해결하기 어려운 복합 필터링 문제에 대한 **다층적 접근** 및 **ORM Brackets** 활용 능력 습득.

<br>

---

## 💡 7. 프로젝트 회고 (KPT)

| 구분 | 내용 |
| :--- | :--- |
| **Keep** (유지할 점) | **피그마**를 이용한 통합 설계 및 방향성 확립. **Git Flow** 기반의 이슈, 브랜치, PR 적극 활용으로 협업 효율성 극대화. **k6, Redis** 도입 과정을 통한 실제 서비스 성능 병목 해결 연습. |
| **Problem** (개선할 점) | Redis 캐싱 도입 후 발생한 **Node.js 서버 CPU 병목 현상** (단일 스레드 환경의 한계 인지 및 인증 캐싱으로 해결). |
| **Try** (시도할 점) | 프로젝트 기간이 촉박하여 적용하지 못한 **CI/CD 자동 배포 시스템** 구축 시도. |

<br>

---

## 🔗 배포 및 설치 정보

* **배포 서버 주소**: `http://3.35.146.155:3000`
* **GitHub 주소**: `https://github.com/hwanga12/Playce.git`

### 💻 서버 실행 요약
프로젝트를 로컬에서 실행하려면 프론트엔드와 백엔드 서버를 각각 실행해야 합니다.

```bash
# 1. Repository Clone
git clone [https://github.com/hwanga12/Playce.git](https://github.com/hwanga12/Playce.git)
cd Playce

# 2. Frontend 실행 (새 터미널)
cd frontend
npm install
npm run dev

# 3. Backend 실행 (다른 새 터미널)
cd backend 
npm install
npm run dev
# 상세 가이드는 각 폴더 내 README 파일 참조
