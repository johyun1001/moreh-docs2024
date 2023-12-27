---
order: 100
icon: table
tags: [guide]
---

이 매뉴얼은 [Moreh API](https://dev-console.moreh.dev/api-docs/) 접속 및 호출 방법을 소개합니다.


### Moreh API 란

[Moreh API](https://dev-console.moreh.dev/api-docs/)는 오픈 소스 GRPC 기반 사용자 API 이며 KT Portal에서 REST로 호출됩니다.

### Moreh API 시작하기

Moreh API를 사용하기 위해서는 https://mcp.moreh.dev/ 에서 지정한 KTC 관리자용 아이디와 비밀번호를 입력하면 Moreh API 서비스를 이용할 수 있습니다. 

API 호출시 검증된 KTC 관리자용 아이디 및 이메일 주소가 확인이 되는 경우 API 접근 가능 token (access token)이 자동으로 인증됩니다.

## API 구성 요소

### **요청 (Request)**

먼저 API 요청을 제대로 하기 위해서는 특정 항목들을 일정 포맷에 따라 호출해야 합니다.
API 요청 규격을 구성하는 요소는 Method(GET, POST, PUT, DELETE)와 API를 요청하기 위한 **파라미터**가 있습니다.

**Method**

- GET
- POST
- PUT
- DELETE

### **응답 (Response)**

응답은 API 요청에 대한 결과값을 의미합니다. 예를 들어 특정 사용자 정보(사용자 고유 Key)를 불러올 때 정상적으로 불러왔는지 결과를 확인할 수 있습니다.
요청한 API의 메서드에 따라 응답 형태는 달라질 수 있는데요. `POST` 요청 값을 Body에 실어 보낼 때는 해당 값이 잘 저장되었는지, 전달되었는지를 나타내는 성공여부를 나타내기도 하고, `GET` 요청처럼 특정 정보를 조회하거나 받아올 때는 값들을 코드로 확인할 수 있거나 자동적으로 다운로드 되기도합니다.

- 요청 성공 시: HTTP 상태 코드 및 API별 성공 응답 필드 반환
- 요청 실패 시: HTTP 상태 코드 및 JSON 형식의 에러 응답 필드 반환, 에러 응답 필드에 에러 코드 및 메시지 포함

### **파라미터(Query Parameter)**

파라미터는 요청 처리에 필요한 데이터를 전달하는 데 사용합니다. 키와 값의 쌍으로 구성되며, 쿼리 스트링(Query string) 또는 바디(Body)를 통해 전달합니다.
각 파라미터는 자료형(Data type)과 필수 전달 여부가 지정돼 있습니다.
이 문서에는 API 메소드 당 전달해야하는 파라미터 type과 필수 여부 설명 등이 제공됩니다. 간혹 Element가 없는 요청도 있는데 정보를 불러올 때 사용하는 GET 메서드에서 Element가 없는 요청이 나타나기도 합니다.

## **Moreh Cloud API(ver 2) Information**

**Check**

API 와 DB 상태 및 gRPC 서버와 클라이언트의 통신 상태가 정상적인지 확인합니다.

- `GET /api/check` - API, IPMI, DB, gRPC 상태 체크. API가 에러일 경우 모두 에러로 표시됨.

**Backend**

사용자 툴(moreh-smi)에서 넘어오는 backend 정보(SDA 및 token, 학습 process 정보)들을 관리합니다.

- `GET /api/v2/backend` - Backend 정보를 모두 불러옵니다.
- `POST /api/v2/backend` - Backend 정보를 생성합니다.
- `PUT /api/v2/backend` - Backend 정보를 수정하거나 전원 원격 제어를 위해 IPMI 명령어를 실행합니다.
- `DELETE /api/v2/backend` - Backend 정보를 삭제합니다.
- `GET /api/v2/backend/group` - Backend의 group 정보를 불러옵니다.
- `POST /api/v2/backend/group` - Backend group 정보를 생성합니다.
- `PUT /api/v2/backend/group` - Backend group 정보를 수정합니다.
- `DELETE /api/v2/backend/group` - Backend group 정보를 삭제합니다.
- `PUT /api/v2/backend/device/status` - Backend ID를 지정하여 Device들의 Status를 변경합니다.
- `POST /api/v2/backend/grouping` - Backend ID를 지정하여 Device들의 Status를 변경합니다.
- `PUT /api/v2/backend/grouping` - Backend로 이루어진 Group들 간에 관계를 수정합니다.
- `DELETE /api/v2/backend/grouping` - Backend의 Grouping 된 것을 해제합니다.

**SDAModel**

사용 가능한 AI 가속기 디바이스(SDAModel)를 관리합니다.

- `GET /api/v2/sdamodel` - SDA Model 목록(micro, Small, Large, xLarge 등)을 불러옵니다
- `POST /api/v2/sdamodel` - SDA Model 을 추가합니다.
- `DELETE /api/v2/sdamodel` - SDA Model을 삭제합니다.
- `POST /api/v2/sdamodel/grouping` - SDA Model의 Grouping을 생성합니다.
- `DELETE /api/v2/sdamodel/grouping` - SDA Model의 Grouping을 해제합니다.
- `GET /api/v2/sdamodel/group` - SDA Model 그룹 정보를 불러옵니다.
- `POST /api/v2/sdamodel/group` - SDA Model 그룹 정보를 생성합니다.
- `PUT /api/v2/sdamodel/group` - SDA Model 그룹 정보를 수정합니다.
- `DELETE /api/v2/sdamodel/group` - SDA Model 그룹 정보를 수정합니다.

**SDA**

Token 별 사용 가능한 AI 가속기 디바이스(SDA)를 관리합니다.

- `GET /api/v2/sda` - SDA 정보를 모두 불러옵니다. 할당된 SDA가 존재한다면 할당된 device와 backend 또한 출력합니다.
- `POST /api/v2/sda` - SDA Model, Token, 고정할당유무, 별칭을 지정하면 SDA를 생성합니다.
- `PUT /api/v2/sda` - Token 값을 지정하고 SDA Model ID를 선택하면 Token의 SDA Model이 지정된 값으로 수정합니다.
- `DELETE /api/v2/sda` - Token 값을 지정하면 해당 SDA를 삭제합니다.
- `GET /api/v2/sda/utilizations`- SDA의 할당 정보(메모리 사용량, 프로세스 정보)를 불러옵니다.

**Token**

Token 및 Group 정보를 관리합니다.

- `GET /api/v2/token` - Token 정보를 모두 불러옵니다.
- `POST /api/v2/token` - Token 별칭을 입력하면 고유한 값을 가진 Token을 생성합니다.
- `PUT /api/v2/token` - Token이 가지고 있는 고유한 값을 입력하면 Token을 수정합니다.
- `DELETE /api/v2/token` - Token이 가지고 있는 고유한 값을 입력하면 Token을 삭제합니다.
- `POST /api/v2/token/grouping` - Token (user) Grouping을 생성합니다.
- `DELETE /api/v2/token/grouping` - Token (user) Grouping을 해제합니다.
- `GET /api/v2/token/group` - Token (user) 그룹 정보를 불러옵니다.
- `POST /api/v2/token/group` - Token (user) 그룹 정보를 생성합니다.
- `PUT /api/v2/token/group` - Token (user) 그룹 정보를 수정합니다.
- `DELETE /api/v2/token/group` - Token (user) 그룹 정보를 삭제합니다.

**Scheduler**

GPU 스케줄러의 대기상태(queue)와 할당 기록을 확인합니다.

- `GET /api/v2/scheduler/queue` - GPU 스케줄러의 큐(queue) 안의 정보를 불러옵니다.
- `PUT /api/v2/scheduler/queue` - 큐에서 대기중인 GPU 작업의 순서를 바꿀 때 사용합니다.
- `DELETE /api/v2/scheduler/queue` - 등록된 Job을 삭제합니다.
- `GET /api/v2/scheduler/history` - GPU 스케줄러의 기록 정보를 불러옵니다.

**Membership**

- `GET /api/v2/membership` - Membership 정보를 불러옵니다.
- `POST /api/v2/membership` - Membership 정보를 생성합니다. (Group ID와 Group ID간의 연결을 생성합니다.
- `DELETE /api/v2/membership` - Membership 정보를 삭제합니다. (Group ID와 Group ID간의 연결을 삭제합니다)

**Usage**

GPU 사용 기록을 확인합니다.

- `GET /api/v2/usage` - GPU 사용 기록을 불러옵니다.

**Log**

API Log를 관리합니다.

- `GET /api/v2/log/sdamanager/event` - SDAManager에 발생한 Event(SDA 생성, SDA 변경 등)를 불러옵니다.