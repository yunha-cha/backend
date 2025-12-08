# 🌏 Jupging - 환경 보호와 건강을 위한 플로깅 플랫폼

**나와 지구가 함께 건강해지는 시간**

[![React Native](https://img.shields.io/badge/React%20Native-0.80.1-61DAFB?logo=react)](https://reactnative.dev/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.4-6DB33F?logo=springboot)](https://spring.io/projects/spring-boot)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.116.1-009688?logo=fastapi)](https://fastapi.tiangolo.com/)
[![Python](https://img.shields.io/badge/Python-3.13-3776AB?logo=python)](https://www.python.org/)

---

## 📋 프로젝트 개요

### 🌟 서비스 소개
"플로깅(Plogging)을 통해 환경 보호와 건강을 동시에 실천하는 플랫폼"
- 플로깅은 **조깅(Jogging)** 과 **줍다(Plocka upp)** 의 합성어로, 조깅하면서 쓰레기를 줍는 친환경 운동입니다.


### 📈 배경 및 필요성
- **환경 문제 심각성**: 한강공원 쓰레기 2달새 892톤 수거, 제주시 클린올레 수거 현황 증가 추세
- **사회적 책임**: 산책로 쓰레기 증가로 인한 처리 비용 및 환경 부담 증대  
- **건강한 습관**: 플로깅을 통한 신체 활동 증진 및 환경 의식 향상

### 👤 서비스 대상
환경 보호에 관심있는 모든 시민, 플로깅 참여자, 건강한 운동 문화를 실천하고자 하는 사용자

### 🎯 서비스 목표
- 플로깅 전문 트래킹 기록 서비스 제공
- 근처 쓰레기통 위치 정보 제공으로 편의성 증대
- 사용자 맞춤형 플로깅 코스 추천
- AI 기반 쓰레기 제보 및 구글맵 매핑으로 데이터 가공 및 서비스 구현

---

## 📅 개발 일정

**총 개발 기간: 2025년 7월 18일 ~ 8월 20일 (약 5주)**

| 기간 | 단계 | 주요 활동 |
|------|------|-----------|
| 07.14 - 07.18 | 🎯 프로젝트 주제 선정 및 계획 | 주제 선정<br/>개발 환경 선정 |
| 07.18 - 07.29 | 🛠️ 프로젝트 분석 및 설계 | 요구사항 분석 및 정의<br/>API 명세서 작성<br/>ERD 설계<br/>화면 설계 |
| 07.29 - 08.15 | 🚀 프로젝트 구현 및 배포 | Spring Boot 백엔드 API<br/>React 프론트엔드 개발<br/>AI 이미지 학습<br/>공공데이터 API 가공<br/>CI/CD 적용 |
| 08.15 - 08.20 | 🎬 프로젝트 마무리 | 통합 테스트 QA<br/>PPT 제작<br/>시연 영상 제작 |

---

## 🚀 핵심 기능

### 🗺️ 플로깅 활동
- **이동 경로 표시**: Geolocation API를 활용한 GPS 좌표 수집 및 실시간 경로 생성
- **지도에 나타나는 정보**: React Native Animated API를 활용한 동적 마커로 내 위치와 주변 쓰레기통 위치 확인
- **지나온 길 기록**: TakeSnapshot API를 이용해 플로깅 종료 후 사용자가 이동한 최종 경로가 포시된 지도를 이미지로 캡쳐

### 🗑️ 쓰레기 제보
- **쓰레기 개수 및 종류 탐지**: YOLO V8 기반 쓰레기 객체 탐지 및 분류
- **쓰레기 위치 자동 입력**: 제보자의 좌표값을 입력 받아 쓰레기 정보를 구글맵에 매핑해 플로깅 이용자에게 제공

### 🏔️ 산책로 맞춤형 검색 & 추천
- **산책로 맞춤형 검색**: 산책로 이름, 지역, 난이도 맞춤형 제공
- **산책로 추천**: 사용자의 니즈에 맞는 산책로 추천
- **마이 페이지**: 플로깅 기록 저장 및 확인

### 🤖 AI 핵심 기술

#### 🎯 쓰레기 분류 AI 모델
- **모델**: YOLO V8 (객체 탐지)
- **학습 데이터**: AI-hub 생활 폐기물 데이터 (어플리케이션 기반 약 12만장)
- **데이터 전처리**: 12가지 클래스로 통합 후 학습 및 언더샘플링 진행
- **학습 결과**: 
  - Precision ≈ 0.94~0.95
  - Recall ≈ 0.94~0.95  
  - mAP50 ≈ 0.95
  - mAP50-95 ≈ 0.94~0.95
  - 목표치인 mAP50 0.95 달성
- **모델 배포**: pt파일 추출 및 이 모델 기반 API 생성

#### 🗺️ 산책로 추천 시스템
- **형태소 분석**: Kiwi (한국어 형태소 분석)
- **토큰화**: 사용자 사연을 명사/고유명사/용언(NNG/NNP/VV/VA) 중심으로 정제해 검색 퀴리 토큰 생성
- **추천 알고리즘**: BM25 기반 1차 검색(후보 생성) + 재정렬(Re-ranking) 파이프라인
  - 특정 스코어에 기반한 검색어와 위치적 가깝기(보검색, IR)에 기반한 보정
  - 역의 가중치: length 3.0, difficulty 2.5, distance 3.0, trash_can_count 1.0, store 1.0
  - 결과: 점수 합산으로 TOP 3 도출 + 자연어 reason 생성 (상대 지표, 만점 없음)

---

## 🏗️ 시스템 아키텍처

### 기술 스택

#### Frontend
- React Native 0.80.1
- React Native Seoul 5.4.1
- React Native Maps 1.25.0
- React Native Async Storage 2.2.0
- React Native Geolocation Service 5.3.1
- Axios 1.11.0
- Zustand 5.0.6
- Node.js 20.13.1
- HTML5 / CSS3 / JavaScript

#### Backend (API 서버)
- Java 17.0.12
- Spring Boot 3.5.4
- Spring Data JPA
- Lombok
- MyBatis 3.0.4
- Swagger 2.5.0
- Gradle 8.14.3

#### AI 서버
- Python 3.13
- FastAPI 0.116.1
- Kiwi (형태소 분석) / NNP 0.20.0
- Pillow 11.3.0
- Rank-BM25 0.2.2
- YOLOv8

#### 인프라 & 데브옵스
- Nginx 1.29.0
- Certbot 4.2.0
- Docker
- GitHub Actions
- Ubuntu 24.04
- AWS EC2
- AWS S3
- AWS ECR

#### 데이터베이스
- Oracle
- Redis 8.2.0

#### 협업 및 디자인
- GitHub
- Discord
- Figma
- Jira

### 아키텍처 구조

<img width="3648" height="1821" alt="image" src="https://github.com/user-attachments/assets/705ea63c-c33c-462b-aa06-1a2ee57f2aa3" />

---

## 📊 ERD
### 주요 테이블
- **회원 (MEMBER)**: 회원 정보 관리
- **플로깅 (PLOGGING)**: 플로깅 활동 기록
- **산책로 (TRAIL)**: 산책로 정보 및 난이도
- **제보 (REPORT)**: 쓰레기 제보 정보
- **쓰레기통 (TRASH_CAN)**: 쓰레기통 위치 정보

---

## 📹 화면 구성 및 시연

### 산책로 맞춤형 검색 & 추천
- 산책로 이름, 지역, 난이도 맞춤형 제공
- 사용자의 니즈에 맞는 산책로 추천

| | | |
|:---:|:---:|:---:|
| <img src="https://github.com/user-attachments/assets/ae8471fd-73c8-45cf-81ba-9ff5015614af" width="270"/> |<img src="https://github.com/user-attachments/assets/5ef0b391-33e5-4525-916f-62c626a78906" width="270"/> | <img src="https://github.com/user-attachments/assets/c3c54205-9d2d-4217-8ef1-78d74520ee2a" width="270"/> |
| 산책로 맞춤형 검색 | 산책로 추천 | 산책로 상세 |

---

### 플로깅 활동
- Geolocation API를 활용해 사용자의 GPS 좌표를 수집하고, 이동 경로의 기반 데이터를 생성
- 수집된 좌표들을 Polyline으로 연결하여 지도 위에 사용자의 이동 경로를 시각적으로 구현
- React Native Animated API를 활용한 동적 마커
- 지도 성능 최적화를 위해 React.memo를 활용해 상위 컴포넌트가 리렌더링 되어도 구글맵은 리렌더링 되지않도록 구현

| | | |
|:---:|:---:|:---:|
| <img src="https://github.com/user-attachments/assets/a09ee0c8-87e2-4b84-890d-1d8c4c91a72a" width="250"/> |<img src="https://github.com/user-attachments/assets/06478173-8e08-4a5c-b431-f8b9ace17716" width="310"/> | <img src="https://github.com/user-attachments/assets/be33094a-2d35-4dbd-8756-b7ce53a20d49" width="250"/> |
| 내 위치 정보 | 이동 경로 표시 | 플로깅 경로 기록 |

---

### 쓰레기 제보 페이지
**쓰레기 개수 및 종류 탐지**:
- YOLO V8 기반 쓰레기 객체 탐지 및 분류

**쓰레기 위치 자동 입력**:
- 제보자의 좌표값을 입력 받아 쓰레기 정보를 구글맵에 매핑해 플로깅 이용자에게 제공

| | |
|:---:|:---:|
| <img src="https://github.com/user-attachments/assets/c1168dab-08e3-4a92-9f77-1764efc0921a" width="360"/> | <img src="https://github.com/user-attachments/assets/bfddc2df-c893-4ad2-ac6c-ded91ebd494d" width="290"/> |
| 쓰레기 개수 및 종류 탐지 | 쓰레기 위치 자동 입력 |

---

**쓰레기통 위치 제공 & 마이 페이지**:
- 사용자 현재 위치 기반 근처 쓰레기통 위치 및 정보 제공
- 플로깅 기록 저장·확인

---

## 📈 프로젝트 성과

### ✅ 완료된 핵심 기능들
- 플로깅 경로 트래킹 및 기록
- AI 기반 쓰레기 탐지 및 분류
- 쓰레기통 위치 정보 제공
- 산책로 맞춤형 검색 및 추천
- 실시간 GPS 기반 이동 경로 시각화
- 구글맵 기반 쓰레기 제보 시스템

### 🎯 기대 효과

**지자체의 플로깅에 대한 관심 증가**
- 제주 플로깅 참여 후 기후·환경 관련 의식 및 행동 변화 여부
- "그렇지 않다" 전체 0.7% / "그렇다" 전체 69.3%

**플로깅 참여 후 기후·환경 관련 의식 및 행동 변화**
- 그렇지 않다: 0.7%
- 그렇지 않다: 0%  
- 보통이다: 30%
- 그렇다: 41.7%
- 매우 그렇다: 27.6%

출처: 한국중앙사회복지센터

---

## 📊 산책로와 쓰레기통 데이터 수집

**공공데이터 포털 API를 통해 쓰레기통 위치 및 산책로 데이터 확보**

- 필요한 데이터 추출 및 변환하여 서비스 맞춤형 가공
- 코스명, 위도, 경도, 소요 시간, 난이도 등
- 가공된 데이터를 기반으로 유저의 좌표와의 실시간 거리 계산, 산책로 위치 제공 등 서비스 구현

---

## 👥 팀원 소개 및 역할

## Team JUP

| 이름 | 역할 | 주요 담당 |
|------|-----------|------------|
| **이정원** | Frontend / AI | Yolo 모델 학습, 자연어 처리, 데이터 추천 모델 개발 |
| **차윤하** | Backend / DB | Open API 데이터 수집 및 가공, 위치·정보 기반 필터링, REST API 설계 및 구현 |
| **엄윤호** | Frontend / UI | 플로깅 관리 기능 구현, UI/UX 설계, 형상 관리 |
| **김승환** | DevOps | CI/CD 구축, HTTPS 적용, 서버 배포 환경 구성 |
| **오정재** | Backend / Documentation | 쓰레기 제보 기능 구현, 회원 기능 구현 |

---

## 🙏 감사의 말

Jupging 프로젝트는 환경 보호와 건강한 라이프스타일을 함께 실천하는 플랫폼입니다. 

**"한 명이라도 더 플로깅을 알고, 한 명이라도 더 플로깅에 참여하길 기대합니다."**

---

© 2025 Team JUP. All rights reserved.

**"🌍 환경을 지키는 가장 똑똑한 습관 JUPGING 🌍"**
