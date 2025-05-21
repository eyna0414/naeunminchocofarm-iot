### 📌 프로젝트 개요

라즈베리파이를 기반으로 한 **스마트팜 환경 제어 시스템**

센서를 통해 수집된 데이터를 분석하고, 자동으로 **급수, 환기, 어닝, 조명 제어**

React 웹/모바일 앱, Spring 백엔드와 연동하여 실시간으로 **환경 데이터 모니터링 및 원격 제어** 기능을 제공

---

### 🛠 사용 기술

| 분류 | 기술 스택 |
| --- | --- |
| 프로그래밍 언어 | Python 3.x |
| 하드웨어 플랫폼 | Raspberry Pi (GPIO 기반 센서 제어) |
| 통신 프로토콜 | WebSocket (JSON 기반 커스텀 메시지), REST API |
| 센서 종류 | DHT (온습도), LDR (일조량), 토양수분 센서 등 |
| 액추에이터 | 펌프, LED, 팬, 어닝 모터 등 |
| 설정 파일 | `application.json`, `settings.json` 기반 동적 구성 |

---

### ✅ 주요 기능

### 🌡 환경 센서 수집

- `air_temp_humidity_sensor.py` → DHT 센서로 온도/습도 측정
- `adc_sensor.py` → 토양수분 센서 아날로그 값 수집
- `pir_sensor.py` → 동작 감지 센서 (야간 조명 연동 가능)
- `sensor_factory.py`로 다양한 센서 유형 동적 생성 가능

### 💧 자동 제어 기능

- `farm_supervisor.py`, `section_controller.py`에서 제어 로직 수행
- 특정 임계값 도달 시 자동으로 다음 액션 수행:
    - 펌프 ON → 급수
    - 팬 ON → 환기
    - 어닝 펼침 → 일조량 차단
- 모든 제어 장치는 `actuator_factory.py` 기반으로 동적 제어 가능

### 📡 서버 연동

- `ncf_api_server.py` → REST API 통해 환경값 주기적 업로드
- `ncf_subscriber.py` → WebSocket 수신 핸들러, 서버에서 명령 수신
- `ncf_frame.py` → 서버와 주고받는 프레임 정의 및 파싱

### 🧠 제어 관리자 구조

- `supervisor.py` → 전체 farm 단위 제어 담당
- `section_controller.py` → 구역별 환경 분석 및 액션 결정
- 제어 흐름: 센서 수집 → 임계값 판단 → 액추에이터 명령 → 서버 전송

---

### 🧠 담당 역할

- 전체 IoT 구조 설계 및 모듈화
- 센서 인터페이스 구현 및 실제 하드웨어 테스트
- 자동 제어 기준 로직 정의 및 소프트웨어 적용
- WebSocket 메시지 파싱 구조 구현 (`ncf_frame.py`)
- 설정 파일 기반 동적 제어 방식 설계 (`application.json`)
- 서버 API 연동 및 통신 테스트 (`ncf_api_server.py`)
- 각 actuator/sensor에 대한 공통 인터페이스 구조 정의

---

### 📂 주요 파일 요약

| 파일명 | 설명 |
| --- | --- |
| `main.py` | 앱 실행 진입점 |
| `sensor_factory.py`, `actuator_factory.py` | 센서/액추에이터 생성 로직 |
| `farm_supervisor.py` | 전체 제어 흐름 제어 |
| `ncf_subscriber.py` | 서버 WebSocket 수신 및 처리 |
| `ncf_api_server.py` | 서버로 데이터 전송 API 호출 |
| `settings.json`, `application.json` | 팜 구성 및 동작 기준 JSON 기반 설정 |
