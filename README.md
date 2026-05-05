# Pi-Monitoring: Digital Twin Frontend
> **"Industrial Vibration Data to Real-time 3D Visualization"**

본 레포지토리는 산업용 장비의 상태를 실시간으로 모니터링하기 위한 디지털 트윈 대시보드(Frontend)입니다. 라즈베리 파이로부터 수집된 센서 데이터를 MQTT와 WebSocket을 통해 수신하고, 이를 Three.js 기반의 3D 모델로 시각화하여 장비의 안정성과 물리적 거동을 직관적으로 파악할 수 있게 돕습니다.

---

## Tech Stack

### **Core**
*   **Framework**: Next.js (App Router)
*   **Language**: TypeScript
*   **State Management**: React Hooks (useState, useEffect)
*   **3D Engine**: Three.js / React Three Fiber (R3F)

### **Communication & Infra**
*   **Real-time**: WebSocket (FastAPI와 실시간 통신)
*   **Deployment**: Docker

---

## Key Implementation (Frontend)

### 1. Real-time Digital Twin Synchronization
*   **Three.js(R3F)**를 활용하여 실제 하드웨어의 6축 센서 데이터(MPU-6050)와 3D 모델의 회전(Rotation) 및 진동 수치를 동기화했습니다.
*   고빈도 데이터 수신 시 발생할 수 있는 시각적 끊김을 방지하기 위해 프레임 보간 로직을 적용했습니다.

### 2. Type-Safe Data Handling
*   **TypeScript**를 사용하여 센서 데이터(Ax, Ay, Az, Gx, Gy, Gz)에 대한 엄격한 인터페이스를 정의했습니다.
*   하드웨어로부터 넘어오는 원시 데이터의 부정확성이나 타입 불일치로 인한 런타임 에러를 사전에 차단했습니다.

### 3. Fail-Safe Condition Monitoring (Engineering Logic)
*   **설계 및 안정성 분석 경험**을 바탕으로, 장비의 임계 진동 수치 초과 시 즉각적인 시각적 경고(UI 피드백)가 발생하도록 로직을 설계했습니다.
*   단순한 데이터 표시를 넘어, 시스템의 Fail-safe 상태를 모니터링하는 관점으로 대시보드를 구성했습니다.

---

## Architecture
```text
[Hardware] --- (MQTT) ---> [FastAPI] --- (WebSocket) ---> [Next.js (This Repo)]
                                                               |
                                                   +-----------+-----------+
                                                   |           |           |
                                              [3D Twin]   [Real-time]  [Alert System]
                                              (Three.js)    (Charts)
