---
icon: passkey-fill
tags: [guide]
---
# HAC 관리하기 (Admin Only)


## Admin Documentation 

KTC 관리자가 HAC 서버를 효과적으로 관리하고 사용할 수 있도록 SMclient 및 Web Console의 사용을 돕는 것을 목표로 합니다.



HAC Web Console: KT Cloud 관리자를 위한 GPU 관리 도구로, GPU 리소스 상태를 실시간으로 모니터링하여 현재 할당된 AI 가속기의 작업 상태와 클러스터 내부의 문제를 빠르게 감지하고 관리할 수 있는 플랫폼입니다.

Moreh SMClient: HAC 환경에서 backnode에 실행되는 worker에 대해서 버전 확인, 토큰 설정 등의 관리를 위한 API입니다.

Moreh API: 오픈 소스 GRPC 기반 API 입니다.

[Moreh SMClient 사용하기 문서](http://localhost:5000/moreh/moreh-docs2024/settings/pages/hac-%EA%B4%80%EB%A6%AC%ED%95%98%EA%B8%B0/smclient-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0/#smclient-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0): moreh_smclient의 기본 사용법을 기술합니다.

[HAC Web Console 사용 가이드](http://localhost:5000/moreh/moreh-docs2024/settings/pages/hac-%EA%B4%80%EB%A6%AC%ED%95%98%EA%B8%B0-(admin-only)/web-console/)는 HAC Web Console로 GPU 자원 모니터링 및 관련 작업 등을 위한 가이드입니다. KTC 관리자가 HAC 클러스터의 자원 사용을 최적화하고 발생 가능한 문제를 빠르게 대응하는데 도움을 줍니다.

 Moreh API 접속 및 호출 방법을 소개합니다.