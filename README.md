#  Pi-Monitoring: Industrial Digital Twin Dashboard

> **"물리적 기구 장치의 움직임을 데이터화하고 실시간으로 시각화하는 디지털 트윈 시스템"**
> 기구설계 엔지니어로서의 도메인 지식과 소프트웨어 엔지니어링 기술을 결합한 모니터링 프로젝트입니다.

---

##  Tech Stack

### **Frontend & Interface**
*   **Framework**: Next.js (App Router)
*   **Language**: TypeScript
*   **3D Engine**: Three.js / React Three Fiber (R3F) -> 아직 고민중...
*   **Communication**: WebSocket (for Real-time Data Streaming)

### **Infrastructure**
*   **Deployment**: Docker (Containerized Build)
*   **Communication Protocol**: MQTT (Edge-to-Server)

---

##  Key Features

### 1. 실시간 디지털 트윈 동기화
*   **Three.js(R3F)**를 활용하여 실제 장비의 6축 센서 데이터(MPU-6050)를 3D 모델의 회전 및 진동 수치와 실시간 동기화합니다.
*   산업용 표준 프로토콜인 **MQTT**와 **WebSocket**을 연동하여 지연 시간을 최소화한 데이터 흐름을 구현했습니다.

### 2. TypeScript 기반의 엄격한 데이터 타입 관리
*   하드웨어 센서에서 들어오는 로우 레벨 데이터(Ax, Ay, Az 등)를 TypeScript Interface로 정의하여, 데이터 흐름 전반에서 타입 안정성을 확보하고 런타임 에러를 방지했습니다.

### 3. 기구학적 인사이트 기반 UI/UX
*   약 2년간의 기구설계 실무 경험을 바탕으로, 기계 장치의 진동 및 상태 모니터링 시 엔지니어에게 필요한 핵심 지표를 시각화하는 데 집중했습니다.

---

##  System Architecture

```text
[Edge Device] --- (MQTT) ---> [FastAPI Server] --- (WebSocket) ---> [Next.js Dashboard]
      |                                                                    |
  MPU-6050 센서                                                     Three.js 3D Rendering
