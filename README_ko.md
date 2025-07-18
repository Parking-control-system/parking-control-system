# [parking-control-system]()

<div align="center">

![Light Mode Logo](assets/logo_white.png#gh-light-mode-only)
![Dark Mode Logo](assets/logo_black.png#gh-dark-mode-only)

</div>

이 프로젝트의 README는 한국어와 일본어로 제공됩니다.
<br>
このプロジェクトの README は日本語と韓国語で提供いたします。

- [한국어 (Korean)](README_ko.md)
- [日本語 (Japanese)](README.md)

<br><br>

# 목차

[1. 프로젝트 소개](#프로젝트-소개)

[2. 프로젝트 멤버](#프로젝트-멤버)

[3. 핵심 기능](#핵심-기능)

[4. 기술 스택](#기술-스택)

[5. 성과](#성과)

[6. 리포지토리](#리포지토리)

<br><br>

# 프로젝트 소개

**Parking Control System**은 **야외 대형 주차장**에서 **카메라**를 이용하여 차량을 효율적으로 관리하여 혼잡을 줄이고 사용자에게 최적의 주차 경험을 제공하는 시스템입니다.

### 기존의 시스템과의 비교

| 항목     | 매설식 센서 시스템                                   | 카메라 기반 시스템                                               |
| -------- | ---------------------------------------------------- | ---------------------------------------------------------------- |
| 설치     | 각 주차 공간마다 복잡한 설치 필요                    | 비교적 설치가 간단하며 여러 공간을 동시에 관리 가능              |
| 비용     | 초기 설치 비용이 높고 주차 공간이 늘어나면 비용 증가 | 여러 공간을 커버하여 주차 공간 확장에 따른 추가 비용 부담이 적음 |
| 유지보수 | 유지보수가 어렵고 비용이 많이 듦                     | 소프트웨어 업데이트로 유지보수가 간단                            |
| 기능성   | 차량 존재 여부만 감지 가능                           | 경로 안내 등 고급 기능 제공 가능                                 |
| 확장성   | 주차 공간마다 추가 센서 설치 필요                    | 카메라로 여러 공간을 커버하여 확장성이 뛰어남                    |

### 목표

이 시스템은 **카메라 기반 기술**을 통해 **실시간 차량 위치 탐지**, **번호판 인식**, **경로 최적화** 등의 기능을 제공하여, 주차 공간이 늘어날수록 경제성과 효율성을 극대화하여 보다 스마트한 주차 관리 환경을 조성하는 것을 목표로 합니다.

### 📽️ **소개 영상（YouTube）**

[![YouTube](https://img.shields.io/badge/Watch%20on%20YouTube-%23FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://youtu.be/VlooaDZfzCg)

<br><br>

# 프로젝트 멤버

|                                                [김규민](https://github.com/kyumin1227)                                                 |                                                 [김민석](https://github.com/kms8032)                                                 |                                                 [김성식](https://github.com/Gapsick)                                                 |                                             [오오이 아야메](https://github.com/ohiayame)                                              |                                             [카와이 사츠키](https://github.com/Saaatsuki)                                              |
| :------------------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------------------------------------------------------: | :------------------------------------------------------------------------------------------------------------------------------------: |
| <a href="https://github.com/kyumin1227"><img src="https://avatars.githubusercontent.com/u/68456336?v=4" width=400px alt="김규민"/></a> | <a href="https://github.com/kms8032"><img src="https://avatars.githubusercontent.com/u/166794112?v=4" width=400px alt="김민석"/></a> | <a href="https://github.com/Gapsick"><img src="https://avatars.githubusercontent.com/u/171534789?v=4" width=400px alt="김성식"/></a> | <a href="https://github.com/ohiayame"><img src="https://avatars.githubusercontent.com/u/166793391?v=4" width=400px alt="아야메"/></a> | <a href="https://github.com/Saaatsuki"><img src="https://avatars.githubusercontent.com/u/166793481?v=4" width=400px alt="사츠키"/></a> |

<br>

- **김규민 (팀장)**: 프로젝트 관리, 메인 프로그램 개발, 모니터링 페이지 및 Socket 서버 개발

- **김민석**: 3D 프린터로 주차장 모델 제작, 도트 매트릭스와 아두이노 배선 및 코드 작성

- **김성식**: Jetson Nano와 Orin Nano 간 UART 통신 구축, 환경 설정 및 입출차기 모터 제어

- **오오이 아야메**: OCR을 이용한 번호판 인식 모델 데이터셋 수집 및 학습

- **카와이 사츠키**: 모니터링 페이지 기획 및 디자인, 프로젝트 문서 정리 및 발표 자료(PPT) 작성

- **공동 작업**: 차량 인식 모델 학습을 위한 데이터셋 수집 및 라벨링

<br><br>

# 핵심 기능

### 번호판 인식

YOLO를 이용하여 번호판을 탐지하고 Easy OCR을 이용하여 글자를 읽습니다.

<details>

- 실행: Jetson Nano
- 목적: 차량 입출차기 동작
- 흐름: Jetson Nano -> Jetson Orin Nano
- 흐름2: Jetson Nano -> Motor

---

차량의 번호판이 인식 될 경우 인식된 번호를 uart를 통해 메인프로그램이 도는 Jetson Orin Nano로 전달한다.

</details>

<img src="assets/numberplate_ocr.gif" alt="Demo Video" width="500px">

### 차량 트래킹

YOLO를 통해 인식한 차량 객체를 DeepSORT를 이용하여 트래킹 합니다.

<img src="assets/car_tracking.gif" alt="Demo Video" width="500px">

### 경로 안내

트래킹 한 차량의 위치를 바탕으로 구역의 혼잡도를 계산하여 경로를 안내합니다.

<img src="assets/cal_route.gif" alt="Demo Video" width="500px">

### 모니터링 페이지

카메라를 통해 계산한 정보를 바탕으로 정보를 표시합니다.

<img src="assets/monitoring.gif" alt="Demo Video" width="1000px">

<br><br>

# 최종 사용 모델

[yolo 모델](https://drive.google.com/file/d/1IWR1UjIvDJyXaY_xoT0IfF2XsE14R15A/view?usp=share_link)

# 기술 스택

### 하드웨어

- **Jetson Nano**: 번호판 인식 및 입출차 프로그램 실행
- **Orin Nano**: 객체 탐지, 추적 및 메인 프로그램 실행
- **Arduino**: 주차장 내 도트 매트릭스 제어
- **서보 모터**: 차단기 제어
- **3D 프린터**: 주차장 모델 제작
- **도트 매트릭스**: 주차 공간 방향 안내 표시

### 소프트웨어 및 라이브러리

- **YOLO (You Only Look Once)**: 차량 및 번호판 탐지 모델
- **OpenCV**: 이미지 처리 및 차량 위치 추적
- **EasyOCR (Optical Character Recognition)**: 번호판 글자 인식
- **DeepSORT**: 차량 트래킹
- **Flask**: 서버 구축 및 클라이언트 데이터 통신
- **Socket.IO**: 실시간 통신을 통한 모니터링 페이지 업데이트
- **React**: 모니터링 페이지 프론트엔드 개발

### 프로그래밍 언어

- **Python**: 메인 프로그램 및 서버, 입출차기 개발
- **TypeScript**: 모니터링 페이지 개발
- **C**: Arduino 통신 및 제어

### 통신 프로토콜

- **UART**: Jetson Nano와 Orin Nano, Orin Nano와 Arduino 간 통신
- **Socket.IO**: 프로그램, 서버, 클라이언트 간 실시간 데이터 전송

<br><br>

# 성과

### 전시 (2024 산학연 협렵 EXPO)

<p>
    <img width="45%" src="assets/expo-4.png">
    <img width="48%" src="assets/expo-2.jpeg">
</p>

### 수상

<p>
    <img width="30%" src="assets/award-1.png">
    <img width="30%" src="assets/award-2.jpeg">
</p>

# 리포지토리

- [Hardware](https://github.com/Parking-control-system/Parking-control-system-Python-Hardware) - 메인 프로그램, 입출차기, 아두이노 제어
- [Frontend](https://github.com/Parking-control-system/Parking-control-system-Frontend) - 모니터링 페이지
