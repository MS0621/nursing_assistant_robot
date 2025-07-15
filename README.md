# 🏥 간호 어시스턴트 자율주행 로봇 시스템  

## 1. 📌 프로젝트 개요

병원 환경에서 간호사의 과중한 업무와 번아웃 문제를 해결하기 위해, **약 전달**과 **바이탈 사인(생체 신호) 모니터링**을 자동화하는 자율주행 로봇 시스템을 개발하였습니다.

본 시스템은 **두 대의 TurtleBot4 로봇**이 협력하여 병원 내 **약국 및 병동 구역**에서 물류와 환자 상호작용 작업을 수행합니다.

###  팀원 역할 분담
| 이름 | 역할 |
|------|------|
| 백홍하 | robot4 Vision, GUI |
| 이하빈 | robot4 Vision, ROS 통신 |
| 장연호 | robot4 Navigation, MQTT |
| 정찬원 | robot4 Navigation, 영상 편집 |
| 이경민, 최정호 | robot1 Vision |
| 문준웅 | robot1 Navigation, GUI |
| 정민섭 | robot1 Navigation, Vital Check Node |

### 시스템 아키텍처  
<img width="920" alt="image" src="https://github.com/user-attachments/assets/9201e11e-0466-4b7a-8aae-bde2ca33f71c" />

### 노드 아키텍처  
<img width="1177" alt="image" src="https://github.com/user-attachments/assets/a5c84d87-49c2-4d37-9e85-74c5bc908902" />

### 시스템 플로우  
<img width="393" alt="image" src="https://github.com/user-attachments/assets/0e439a5b-1d56-4238-9ec0-7aecfa4f4423" />

---

## 2. ⚙️ 주요 기능

### ✅ 자율주행 및 장애물 회피
- ROS 2 Nav2 기반 SLAM 자율주행
- 복잡한 병원 복도 및 병실 환경에서도 안정적으로 주행
- 동적 장애물(예: 사람) 감지 시 자동 정지 및 재개

<img width="506" height="252" alt="image" src="https://github.com/user-attachments/assets/5048a97d-15a6-47bf-ab3b-f94d8948e5e0" />


<img width="608" height="453" alt="image" src="https://github.com/user-attachments/assets/f1ede8d1-7cf5-4d47-b80f-00dc56e66451" />



---

### ✅ 물체 및 환자 인식
- YOLOv8, YOLOv11을 활용하여 약품(Tylenol, 붕대 등) 실시간 감지

  ![250627_YOLO turn](https://github.com/user-attachments/assets/025b827b-0cea-40c9-8565-37c37f36c835)

- ArUco 마커 및 얼굴 인식을 통해 환자 식별

  ![face](https://github.com/user-attachments/assets/c7c89e95-f906-4512-b23b-c57c82a9576b)
  
- ArUco 마커 인식을 통한 로봇 자세 제어



- 깊이 카메라 기반 위치 추정 및 TF2를 통한 3D 위치 변환

  ![250627_marker turn](https://github.com/user-attachments/assets/f3ea4790-9497-4c3c-9367-df301f5fd89a)

---

### ✅ 비접촉 생체 신호 모니터링
- rPPG(영상 기반 PPG)를 이용한 심박수, SpO2, 혈압 추정

#### < rPPG란? >

<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/f0cc3c06-ee91-4de3-96d9-45d34bc1ce38" />

rPPG는 RGB 카메라를 이용한 비접촉 방식 생체 신호 측정 기술로, 혈액량 변화에 따라 얼굴 피부 색상이 미세하게 변하는 것을 분석하여 생리학적 신호를 추정합니다.

1. 원거리에서 심박수 비접촉 측정  
2. 얼굴 영상의 피부 색 변화 분석  
3. 측정 가능 항목: 심박수, 심박수 변이(HRV), 산소포화도, 호흡률, 스트레스 지수, 혈압, 피부 온도 등

- 얼굴 추적 및 필터 기반 신호 증폭 기술과 통합됨

<img src="https://github.com/user-attachments/assets/ca3a3ef4-64a4-4456-9228-52b35cdbcfaa" width="400"/>

📄 [rPPG 기반 산소포화도 측정 성능 비교 논문.pdf](https://github.com/user-attachments/files/21120109/Comparison.of.rPPG-based.Oxygen.Saturation.Measurement.Performance.by.Face.Area.with.Simple.Signal.Processing.pdf)

---

### ✅ 클라우드 기반 로봇 통신
- EMQX 클라우드를 이용한 MQTT 메시징으로 다중 로봇 안정적 통신

  <img width="379" alt="image" src="https://github.com/user-attachments/assets/c6ff258c-b111-43d3-be72-e0dd564d2fff" />

- 분산형 태스크 할당 및 랑데뷰 지점 설정 (amcl_pose/pose/position/x, y 사용)

  ![녹음 2025-07-08 194028](https://github.com/user-attachments/assets/c9592713-b85c-4ec3-b4cc-932662d9f80e)

---

### ✅ GUI 통합 제어 패널
- 실시간 약물 요청 및 로봇 상태 모니터링
- 로봇 위치, 생체 정보 등을 시각적으로 표시

---

## 3. 🧠 기술 스택

| 구분 | 사용 기술 |
|------|-----------|
| **로봇 플랫폼** | TurtleBot4, ROS 2 Humble, Nav2 |
| **비전 시스템** | OAK-D 카메라, YOLOv8/YOLOv11, OpenCV |
| **통신** | MQTT, EMQX Cloud |
| **AI/알고리즘** | rPPG, 얼굴 인식, KCF 트래킹, CHROM, TF2 |
| **개발 환경** | Ubuntu 22.04, Python3, RViz2, Roboflow |
| **협업 도구** | GitHub, Google Docs, 발표 도구 등 |

<img width="727" alt="image" src="https://github.com/user-attachments/assets/82cc495a-b436-4a73-a29b-a479adc2bb34" />

---

## 4.  프로젝트 시나리오
### 개별 시나리오


### 1) 🏥 제조실  
![시나리오 1](https://github.com/user-attachments/assets/f46c4487-bd00-44d8-a1ff-8cf17a8d720c)


#### 상세 동작 흐름

**① 약품 탐지 및 위치 추정**  
- 요청 수신 → Nav2로 선반 앞 도착  
- YOLOv8 모델을 통해 약품 탐지  
- Depth 카메라로 거리 측정 → TF2 변환을 통해 map 좌표 추출  

**② 약품 위치로 이동 및 전달 준비**  
- 추정된 좌표로 로봇 이동  
- MQTT를 통해 robot1과 위치 정보 공유  
- 랑데부 포인트에서 전달 대기  

---

### 2) 🛏 병실  
![시나리오2](https://github.com/user-attachments/assets/72cff4be-17c5-457c-a431-aeaebe92f2b5)

#### 상세 동작 흐름

**① 환자 ID 인식**  
- 병실 도착 후 회전 → ArUco 마커 탐지로 환자 ID 확인  
- 마커 거리 1m 이내 도달 시 정지  

**② 환자 얼굴 감지 및 바이탈 측정**  
- 얼굴 감지 (Face Detection)  
- rPPG 기반 Vital signal 추정: 심박수, 산소포화도, 혈압 추정  
- GUI로 결과 전송  

---

### 3) 🤖 로봇 협업  
![시나리오 3](https://github.com/user-attachments/assets/359776c8-ef37-49c6-985e-9f082ad1503d)

#### 상세 동작 흐름

**① 좌표 공유 및 동기화**  
- robot1: 현재 좌표 → MQTT Publish  
- robot4: 해당 좌표 Subscribe → 이동

**② 랑데부 지점 도착 및 약품 전달**  
- 두 로봇 모두 도착 시 flag 전송  
- robot4 → 약품 전달  
- robot1 → 병실로 출발, robot4 → 도킹 위치 복귀  

---

## 5. 🌟 결과 및 기대 효과

- 병원 내 물류와 환자 상호작용을 위한 **자율 로봇 전체 파이프라인 시연 성공**
- 자율주행, 물체 인식, 환자 인식, 생체 신호 측정 등을 통합한 **실시간 작동 시스템 구축**
- 클라우드 기반 아키텍처로 **대규모 병원 확장 가능성 확보**
- 반복 업무를 로봇이 대신함으로써 간호사는 전문적 진료에 집중 가능
- **스마트 병원 인프라 구축의 시범 모델 제공**
- Manipulator와 협업시 **완전 자동화 가능성 시사**
<img width="1059" height="549" alt="Image" src="https://github.com/user-attachments/assets/64e8267a-c8ae-4368-bb05-0ffcc7f60ae9" />

---

## 6. 🎥 데모 영상

[![시연 영상 썸네일](https://img.youtube.com/vi/engfuoJjMBw/0.jpg)](https://www.youtube.com/watch?v=engfuoJjMBw)

👉 클릭 시 YouTube에서 전체 영상 시청


---

## 7. More about Project

[▶️PDF로 보기](https://drive.google.com/file/d/1io5YXrv59YGzz9mFVwZFr9w5tfyfv3y-/preview)

[▶️PPT로 보기](https://docs.google.com/presentation/d/1M3GEA6Gc1wiV9HGT6Sjt1-zfXWkuzGvD/edit?usp=sharing&ouid=100435134823954159263&rtpof=true&sd=true/preview)


---
