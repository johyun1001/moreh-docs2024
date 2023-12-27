---
icon: note
tags: [guide]
---
### **SMClient 란?**

KT HAC 서비스의 SMClient는 SDAManager API를 호출하는 관리자 tool입니다. 대표적인 기능으로 (1) HAC 서비스 사용 현황 조회, (2) 토큰에 대한 관리, (3)user group, SDAModel group, Backend group 및 멤버쉽에 대한 관리가 있습니다.

## 1. SMClient 실행하기

SDAManager 의 클라이언트인 moreh_smclient 는 다음과 같이 실행할 수 있습니다. 현재 SDAManager 의 상태나 정보를 체크할 때 사용하게 됩니다. moreh_smclient를 실행하려면 SDAManager에 연결할 수 있도록 ip, port의 환경 설정이 필요합니다.

```bash
# hac-bastion에서 master노드로 접근
ssh master01

# moreh_smclient명령어 실행
moreh_smclient

# 만일 moreh_smclient 명령어 실행이 안될경우엔 아래와같이 실행
kubectl exec -it -n maf deploy/sdamanager-api-deployment -- /app/bin/moreh_smclient
```

## 2. 사용 현황 조회

### A. 전체 노드 및 디바이스 사용 현황 조회

`show backend` 명령어를 사용하여 moreh_smclient로 해당 클러스터에서 사용되는 노드와 디바이스 정보를 조회할 수 있습니다.

출력되는 조회 정보는 다음과 같습니다. - `Name` : 노드의 이름 - `IP` : 노드의 ip address - `Status` : 노드의 상태 정보 - `SHUTDOWN` : 노드 사용 불가 - `ACTIVE` : 노드 사용 가능 - `Device` : 디바이스(GPU)의 갯수와 상태 정보 - `SHUTDOWN` : 디바이스 사용 불가한 상태 - `IDLE` : 디바이스 사용 가능 - `PREPARING` : 할당 된 디바이스 사용 준비 - `PROCESSING` : 디바이스 사용 - `CLEANING` : 사용된 디바이스 정리

**사용 예시**

```bash
>show backend
    +-----------------------------------------------------------------------------------------------------+
    |  ID  |   Name   |        Ip        |  Group  |   Status   |       Device       |       Device       |
    +=====================================================================================================+
    |  1   |  back01  |  192.168.110.0   |         |  ACTIVE    |  0  |  PROCESSING  |  1  |  PROCESSING  |
    |      |          |                  |         |            |  2  |  PROCESSING  |  3  |  PROCESSING  |
    |      |          |                  |         |            |  4  |  PROCESSING  |  5  |  PROCESSING  |
    |      |          |                  |         |            |  6  |  PROCESSING  |  7  |  PROCESSING  |
    |  2   |  back02  |  192.168.110.1   |         |  ACTIVE    |  0  |  PROCESSING  |  1  |  PROCESSING  |
    |      |          |                  |         |            |  2  |  PROCESSING  |  3  |  PROCESSING  |
    |      |          |                  |         |            |  4  |  PROCESSING  |  5  |  PROCESSING  |
    |      |          |                  |         |            |  6  |  PROCESSING  |  7  |  PROCESSING  |
    |  3   |  back03  |  192.168.110.2   |         |  ACTIVE    |  0  |  PROCESSING  |  1  |  PROCESSING  |
    |      |          |                  |         |            |  2  |  PROCESSING  |  3  |  PROCESSING  |
    |      |          |                  |         |            |  4  |  PROCESSING  |  5  |  PROCESSING  |
    |      |          |                  |         |            |  6  |  PROCESSING  |  7  |  PROCESSING  |
    |  ... |          |                  |         |            |     |              |     |              | 
    |  ... |          |                  |         |            |     |              |     |              | 
    |  ... |          |                  |         |            |     |              |     |              | 
    |  57  |  back57  |  192.168.110.56  |         |  ACTIVE    |  0  |  IDLE        |  1  |  IDLE        |
    |      |          |                  |         |            |  2  |  IDLE        |  3  |  IDLE        |
    |      |          |                  |         |            |  4  |  IDLE        |  5  |  IDLE        |
    |      |          |                  |         |            |  6  |  IDLE        |  7  |  IDLE        |
    |  58  |  back58  |  192.168.110.57  |         |  ACTIVE    |  0  |  IDLE        |  1  |  IDLE        |
    |      |          |                  |         |            |  2  |  IDLE        |  3  |  IDLE        |
    |      |          |                  |         |            |  4  |  IDLE        |  5  |  IDLE        |
    |      |          |                  |         |            |  6  |  IDLE        |  7  |  IDLE        |
    |  59  |  back59  |  192.168.110.58  |         |  ACTIVE    |  0  |  IDLE        |  1  |  IDLE        |
    |      |          |                  |         |            |  2  |  IDLE        |  3  |  IDLE        |
    |      |          |                  |         |            |  4  |  IDLE        |  5  |  IDLE        |
    |      |          |                  |         |            |  6  |  IDLE        |  7  |  IDLE        |
    |  60  |  back60  |  192.168.110.59  |         |  ACTIVE    |  0  |  IDLE        |  1  |  IDLE        |
    |      |          |                  |         |            |  2  |  IDLE        |  3  |  IDLE        |
    |      |          |                  |         |            |  4  |  IDLE        |  5  |  IDLE        |
    |      |          |                  |         |            |  6  |  IDLE        |  7  |  IDLE        |
    +-----------------------------------------------------------------------------------------------------+
```

### B. 현재 실행 또는 대기 중인 작업 조회

`show job` 명령어를 실행하여 moreh_smclient로 실행 중 또는 대기중인 작업 정보를 조회할 수 있습니다.

출력되는 조회 정보는 다음과 같습니다.

- `FeID` : Job의 id
- `Token`: 실행한 Token
- `PRY` : Job의 우선순위 값 (기본값 : 0)
- `Status` : Job의 상태정보
- `PID` : 해당 vm에서의 pid
- `Process Name` : 실행한 process 및 매개변수 정보

**사용 예시**

```bash

    >show job
    +----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
    |  FeID   |            Token           |  PRY  |  Status   |   PID   |                                                                                                                                                                                      Process Name                                                                                                                                                                                      |        Start Time        |
    +========================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+
    |  24622  |          token_1           |    0  |  RUNNING  |   9330  |  python train.py --dataset inat --load-checkpoint ./checkpoint/162 --save-model model.pt                                                                                                                                                                                                                                                                                               |  2023-09-14 23:14:10.14  |
    |  26197  |          token_2           |    0  |  RUNNING  |   4109  |  python main_train_pmlffnet_v1_sat_ms_comp_pan_comp.py                                                                                                                                                                                                                                                                                                                                 |  2023-09-15 21:53:19.07  |
    |  26428  |          token_3           |    0  |  RUNNING  |  20906  |  python train.py --model-cfg ./models/yolov5x6.yaml --save-model model.pt -b 128 -e 300 --img 1280 --num-workers 6                                                                                                                                                                                                                                                                     |  2023-09-16 01:39:56.34  |
    |  27541  |          token_4           |    0  |  RUNNING  |  16874  |  python train_imagenet.py                                                                                                                                                                                                                                                                                                                                                              |  2023-09-19 09:54:49.83  |
    |  27772  |          token_5           |    0  |  RUNNING  |  27034  |  python train_tudl_non_ddp.py --cls=dragon                                                                                                                                                                                                                                                                                                                                             |  2023-09-19 16:32:53.13  |
    |  27823  |          token_6           |    0  |  RUNNING  |  24802  |  python train.py --workers 8 --device 0 --batch-size 256 --data data/coco.yaml --img 640 640 --cfg cfg/training/yolov7.yaml --weights  --name yolov7 --hyp data/hyp.scratch.p5.yaml                                                                                                                                                                                                    |  2023-09-19 17:50:33.25  |
    |  27910  |          token_7           |    0  |  RUNNING  |  11775  |  python train.py --save-model model.pt -b 64 -e 100                                                                                                                                                                                                                                                                                                                                    |  2023-09-20 10:19:57.81  |
    |  27913  |          token_8           |    0  |  RUNNING  |  31688  |  python train.py -b 128 --num-workers 4                                                                                                                                                                                                                                                                                                                                                |  2023-09-20 10:49:12.78  |
    |  27991  |          token_9           |    0  |  RUNNING  |  28849  |  python ./reference/train.py --save-model /mnt/addvol/workspace/gpt/model/first_model.pt -b 32 --train-dataset /mnt/addvol/workspace/gpt/data/train_dataset_downsized.txt --val-dataset /mnt/addvol/workspace/gpt/data/valid_dataset_downsized.txt --vocab-file-path /mnt/addvol/workspace/gpt/tokenized/vocab.json --merges-file-path /mnt/addvol/workspace/gpt/tokenized/merges.txt  |  2022-09-20 13:15:05.64  |
    |  28123  |          token_10          |    0  |  RUNNING  |  11171  |  python train.py --save-model bart.pt -b 32 -e 1                                                                                                                                                                                                                                                                                                                                       |  2023-09-20 16:38:03.62  |
    +----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
```

### C. 작업 상세 조회

moreh_smclient를 이용하여 실행 또는 대기중인 작업에 대해서 상세한 조회할 수 있습니다.

명령어는 `get job feid {id}` 또는 `get job token {token}` 이며 조회되는 정보는 다음과 같습니다.

- `Frontend ID` : Job의 id
- `Token`: 실행한 Token
- `Token Name` : Token 정보
- `SDA` : Token에 별도로 지정된 SDA ID 정보
- `Priority` : Job의 우선순위 값 (기본값 : 0)
- `Status` : Job의 상태정보
- `Client` : 해당 vm에서 사용하는 moreh 솔루션 버전
- `Client PID` : 해당 vm에서의 pid
- `Process Name` : 실행한 process 및 매개변수 정보
- `Backend Group` : 해당 vm이 속한 backend group 이름
- `Request Time` : 작업 요청 시간
- `Start Time` : 작업 시작 시간 (대기 및 준비 시간을 제외한 실제 GPU 연산시작 시간)
- `Version` : 해당 vm의 클라이언트 버전
- `Device Count` : GPU 갯수
- `Device Information` : 연결된 노드 및 디바이스 정보 (출력 예 - back10 | 0,1,2,3,4,5,6,7)

**사용 예시**

```bash

    >get job feid 24622
    +-----------------------------------------------------------------+
    |      Name       |                     Value                     |
    +=================================================================+
    |  Frontend ID    |  24622                                       |
    |  Token          |  your_toekn                                   |
    |  Token name     |  user@gmail.com_promo-vm-16                   |
    |  SDA            |  5257                                         |
    |  Priority       |  0                                            |
    |  Status         |  RUNNING                                      |
    |  Client         |  pytorch-1.13.1+cu116.moreh23.9.2             |
    |  Client PID     |  2917519                                      |
    |  Process name   |  python train_moreh.py --cfg moreh.reduce_en  |
    |  Backend Group  |  default_backend_group                        |
    |  Request time   |  2023-09-13 00:57:15.59                       |
    |  Start time     |  2023-09-13 00:57:21.78                       |
    |  Version        |  23.9.2                                       |
    |  Device count   |  8                                            |
    |  back01         |  0,1,2,3,4,5,6,7                              |
    +-----------------------------------------------------------------+

```

### D. 대기중인 작업에 대한 우선순위 변경

`update job priority {id} {value}` 명령어를 사용하여 대기중인 작업의 우선순위를 변경할 수 있습니다.

입력시 사용되는 매개변수는 다음과 같습니다.

- `id` : 작업의 id
- `value` : 변경하고자 하는 우선순위 값

```bash
>update job priority 28150 -1
```

### E. 실행 또는 대기 중인 작업에 대한 강제 취소

`release {id}` 또는 `release {token}` 명령어를 사용하여 실행 또는 대기 중인 작업에 대한 강제 취소가 가능합니다.

입력시 사용되는 매개변수는 다음과 같습니다.

- `id` : 작업의 id
- `token` : 사용자 token 값

```bash
  >release 24622
```

## 3. Token 및 SDA 관리하기

### A. Token 및 SDA 생성하기

기본적인 Token 생성(발급) 및 삭제 방법은 moreh-smclient에서 명령어 `help` 를 입력하면 다음과 같이 출력됩니다.

```bash
[root@Master01-4B0806u18cj1-hacgpu ~]$ moreh_smclient 
    SDAManager's Client. Connect to 127.0.0.1:30105
    Moreh Corporation Copyright (c) 2020-. All rights reserved.

    >help
    create sda             : Create new SDA or add SDA to registered Token
                          (usages: create sda {Token} {SDAModelID} {description})

    create token           : Create new Token
                          (usages: create token {description} {priority : optional})

    delete sda             : Delete all SDAs using requested Token or delete specified SDA using Token, SDA's ID
                          (usages: delete sda {Token} {SDA's ID : optional})

    delete token            : Delete Token
                            (usages: delete token {Token})
```

create token 이라는 명렁어로 token을 생성할 수 있는데 이때 {description} 으로 되어 있는 부분이 token name 입니다.

**Token 생성 및 SDA 설정 예시**

Token을 먼저 생성하고 반환 받은 token으로 SDA를 생성합니다. SDA를 생성할 때는 model 값을 함께 주어야 합니다. SDA 생성시 넣는 숫자는 model의 id입니다.

```bash

    [root@Master01-4B0806u18cj1-hacgpu ~]$ moreh_smclient
    SDAManager's Client. Connect to 192.168.64.103:50052
    Moreh Corporation Copyright (c) 2020-. All rights reserved.

    >create token user@gmail.com_moreh-test-for-doc
    Create SDA Success (Token : YmFidTE2NjcyOTE2NTI0MjU=)

    >create sda YmFidTE2NjcyOTE2NTI0MjU= 1 sda_name
    Create SDA success.

    >get sda your_token
    +---------------------------------------------------------------------------------------+
    |   ID   |            Token           |  SDAModel  |  Reserved  |  Be_ID  |  Device_ID  |
    +=======================================================================================+
    |  1542  |          your_token        |  1         |  False     |         |             |
    +---------------------------------------------------------------------------------------+
```

sdamodel 의 ID는 show sdamodel 이라는 명령어로 확인할 수 있습니다.

```bash

    >show sdamodel
    +---------------------------------------+
    |  ID  |        Name        |  Devices  |
    +=======================================+
    |   1  |  Small.64GB        |        1  |
    |   2  |  Medium.128GB      |        2  |
    |   3  |  Large.256GB       |        4  |
    |   4  |  xLarge.512GB      |        8  |
    |  52  |  1.5xLarge.768GB   |       12  |
    |   5  |  2xLarge.1024GB    |       16  |
    |   6  |  3xLarge.1536GB    |       24  |
    |   7  |  4xLarge.2048GB    |       32  |
    |   8  |  6xLarge.3072GB    |       48  |
    |   9  |  8xLarge.4096GB    |       64  |
    |  10  |  12xLarge.6144GB   |       96  |
    |  11  |  24xLarge.12288GB  |      192  |
    |  12  |  48xLarge.24576GB  |      384  |
    +---------------------------------------+
```

**Tip**

모든 명령어는 한줄 명령으로 실행 가능합니다.

```bash

  $ moreh_smclient --command 'create token babukk89@gmail.com_moreh-test-for-doc'
  Create SDA Success (Token : your_token)

  $ moreh_smclient --command 'create sda your_token 1 sda_name'
  Create SDA success.

  $ moreh_smclient --command 'get sda your_token'
  +---------------------------------------------------------------------------------------+
  |   ID   |            Token           |  SDAModel  |  Reserved  |  Be_ID  |  Device_ID  |
  +=======================================================================================+
  |  1543  |          your_token        |  1         |  False     |         |             |
  +---------------------------------------------------------------------------------------+
```

### B. Token 삭제하기

Token을 삭제하기 위해서는 먼저 SDA를 삭제해야 합니다.

**명령어**

- `delete sda` : SDA 삭제 (usages: delete sda {Token})
- `delete token` : Token 삭제 (usages: delete token {Token})

```bash

    [root@Master01-4B0806u18cj1-hacgpu ~]$ moreh_smclient
    SDAManager's Client. Connect to 192.168.64.103:50052
    Moreh Corporation Copyright (c) 2020-. All rights reserved.

    >delete sda your_token
    Delete SDA success.
    >delete token your_token
    Delete Token success.
```

**Tip**

한줄 명령으로 실행 가능합니다.

```bash

    $ moreh_smclient --command 'delete sda your_token'
    Delete SDA success.

    $ moreh_smclient --command 'delete token your_token'
    Delete Token success.
```

### C. Token의 우선순위 변경

`update token priority {token} {priority}` 명령어를 사용하여 고객사 token의 우선순위를 변경할 수 있습니다. 예를 들어 작업 Queue에 A고객(48노드), B고객(0.5노드), C고객(0.5노드), etc. 가 있을 때 대형 고객 A가 가장 앞에 있을 경우에는 B와 C고객은 못 들어가게 됩니다. 이때 대형 고객 A의 Token 자체의 priority를 낮게 조정해두고, B, C 고객 priority를 높게 해 두면 항상 B, C 고객이 수행하는 작업은 대형 고객 A가 만든 job 보다 항상 먼저 들어갈 수 있게 됩니다.

priority 값이 높은 token의 작업이 먼저 할당되며, priority 가 동일할 경우에는 먼저 요청된 token이 수행됩니다.

입력시 사용되는 매개변수는 다음과 같습니다.

- `token` : 실행한 Token 정보
- `priority` : 변경하고자 하는 우선순위 값

```bash
>update token priority your_token 0
```

### D. Token 환경 변수 추가하기

토큰에 환경 변수를 추가하는 경우`get token {token}` 으로 현재 토큰에 반영된 환경 변수를 확인합니다.

```bash
> get token your_token
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|            Token           |                Description                |  Cur SDA  |  Max SDA  |  Duplicable  |  Priority  |  Access Level  |  Worker Execute Info  |  ENV value  |
+===================================================================================================================================================================================+
|          your_token        |                  test...                  |  4732     |  5        |  off         |  0         |  USER          |                       |   여기 추가   |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
```

`add token env {token} {env_key} {env_value}` 명령어를 사용하여 토큰에 환경 변수를 추가 할 수 있습니다.

입력시 사용되는 매개변수는 다음과 같습니다.

- `token` : 추가 할 대상의 token 정보
- `env_key` : 환경 변수
- `env_value` : 환경 변수 설정에 필요한 값

```
> add token env your_token MOREH_WHOLE_SYSTEM_PROFILING_MODE 1
> add token env your_token MODNN_SEND_RECV_PIPE 1
```

### E. Token 환경 변수 삭제하기

`remove token env {token} {env_key}` 명령어를 사용하여 토큰에 환경 변수를 삭제 할 수 있습니다.

입력시 사용되는 매개변수는 다음과 같습니다.

- `token` : 추가 할 대상의 token 정보
- `env_key` : 환경 변수

```bash
> remove token env your_token MOREH_WHOLE_SYSTEM_PROFILING_MODE
> remove token env your_token MODNN_SEND_RECV_PIPE
```

### F. Token에서 multi SDA 최대 개수 설정하기

multi SDA를 사용 시, 동시에 사용할 수 있는 multi sda 개수의 최댓값을 설정할 수 있습니다.

`update token sda max {token} {max}` 명령어를 사용하여 토큰에 multi sda 개수의 최댓값을 설정합니다.

입력시 사용되는 매개변수는 다음과 같습니다.

- `token` : 대상의 token 정보
- `max` : sda 최대 개수

```
> update token sda max your_token 4
> get token your_token
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|            Token           |                Description                |  Cur SDA  |  Max SDA  |  Duplicable  |  Priority  |  Access Level  |  Worker Execute Info  |  ENV value  |
+===================================================================================================================================================================================+
|          your_token        |                  test...                  |  4732     |  4        |  off         |  0         |  USER          |                       |           |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
```

### G. Token에서 dupicable SDA 설정하기

Duplicable SDA를 사용하는 경우, 우선 multi sda 개수의 최댓값을 1로 설정해야 합니다.

`update token sda max {token} {max}` 명령어를 사용하여 토큰에 sda 개수의 최댓값을 설정합니다.

입력시 사용되는 매개변수는 다음과 같습니다.

- `token` : 대상의 token 정보
- `max` : sda 최대 개수

```
> update token sda max your_token 1
```

이후, `update token duplicable {token} {value}` 명령어를 사용하여 토큰에 dupicable SDA 사용 여부 및 중복하여 사용할 수 있는 sda의 개수를 선택 할 수 있습니다.

입력시 사용되는 매개변수는 다음과 같습니다.

- `token` : 대상의 token 정보
- `value` : 복하여 사용할 수 있는 sda의 개수

```
> update token duplicable your_token 1
Update Token Duplicable success.
> get token your_token
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|            Token           |                Description                |  Cur SDA  |  Max SDA  |  Duplicable  |  Priority  |  Access Level  |  Worker Execute Info  |  ENV value  |
+===================================================================================================================================================================================+
|          your_token        |                  test...                  |  4732     |  4        |  off         |  0         |  USER          |                       |           |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
> update token duplicable your_token 4
Update Token Duplicable success.
> get token your_token
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
|            Token           |                Description                |  Cur SDA  |  Max SDA  |  Duplicable  |  Priority  |  Access Level  |  Worker Execute Info  |  ENV value  |
+===================================================================================================================================================================================+
|          your_token        |                  test...                  |  4732     |  4        |  4           |  0         |  USER          |                       |           |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
```

## 5. 그룹(Group) 관리하기

### Group 개념

Moreh 솔루션을 이용하는 고객들에게는 사용자 자신을 식별하기 위해 암호화된 token을 받게 됩니다. 이 token은 “`/etc/moreh/{토큰값}`” 형식으로 가상 머신(VM) 내에 저장됩니다. 각 고객의 VM은 해당 토큰을 사용하여 마스터로 GPU 리소스를 요청하게 됩니다. Moreh Cloud Platform은 토큰을 기반으로 동작하는 클라우드 시스템이므로, 토큰이 없으면 GPU 연산 및 PyTorch 실행이 제한됩니다.

그룹 기능은 고객의 토큰에 따라 사용할 수 있는 AI 가속기 디바이스와 그 수를 제어하는 기능입니다. 예를 들어, A 고객은 Small과 Medium만 사용하도록 설정된 SDAModelGroupA에 연결됩니다. B 고객은 Medium부터 Large와 xLarge까지 옵션을 선택할 수 있도록 제한을 설정됩니다. 이렇게 그룹 기능을 통해 유연하게 GPU 자원을 조절할 수 있게 됩니다. KT Cloud 관리자분들께서는 Group기능으로 고객들의 GPU 자원 관리를 보다 원활하게 수행하실 수 있습니다.

[]()

예를들어 위와 같이 Group 관계가 형성된 경우 UserGroupA의 Token이 할당된 고객은 Small과 Medium 디바이스만을 사용 가능하며 Large와 xLarge는 사용이 불가능합니다.

마찬가지로 UserGroupB의 TokenB, TokenC, TokenD가 할당된 고객은 Medium, Large, xLarge만을 사용 가능하고 Small 디바이스는 사용이 불가능합니다.

### Group 구성

사용자의 Token, SDA Model, Backend가 각각 group으로 존재하며 Membership이 User Group과 SDAModel 간에 관계를 형성합니다.

### A. User Group

SDAManager에서의 사용자 token으로 이루어진 그룹

- 하나의 token이 여러 user group에 포함될 수 있습니다.
- `moreh_smclient` 명령어 : 자세한 파라미터는 smclient에서 확인

```bash
    > show usergroup
    +---------------------------------------------------------------+
    |  ID  |   Name    |  Description  |           Childs           |
    +===============================================================+
    |   1  |  group_A  |               |                            |
    |  19  |  group_B  |               |         your_token_1       |
    +---------------------------------------------------------------+
```

**사용 예시**

1. 새로운 그룹을 만들어서 해당 그룹에 토큰을 집어넣고 싶은 경우

```bash
    > create usergroup group_C TEST dGFlczE2NzY2MDAwNDAzMTk=
    Create Group Success (id : 25)
    > show usergroup
    +---------------------------------------------------------------+
    |  ID  |   Name    |  Description  |           Childs           |
    +===============================================================+
    |   1  |  group_A  |               |                            |
    |  19  |  group_B  |               |         your_token_1       |
    |  25  |  group_C  |  TEST         |         your_token_2       |
    +---------------------------------------------------------------+
```

1. group_B에 속한 토큰을 group_C로 옮기고 싶은 경우

```bash

    > update usergroup list 19 Null
    Update UserGroup Token list success.
    > show usergroup
    +-----------------------------------------------------------------------------------------+
    |  ID  |   Name    |  Description  |                        Childs                        |
    +=========================================================================================+
    |   1  |  group_A  |               |                                                      |
    |  19  |  group_B  |               |                                                      |
    |  28  |  group_C  |  TEST         |       your_token_2                                   |
    +-----------------------------------------------------------------------------------------+

    > add usergroup 28 your_token_1
    Add Token to User Group success.
    > show usergroup
    +-----------------------------------------------------------------------------------------+
    |  ID  |   Name    |  Description  |                        Childs                        |
    +=========================================================================================+
    |   1  |  group_A  |               |                                                      |
    |  19  |  group_B  |               |                                                      |
    |  28  |  group_C  |  TEST         |              your_token_1, your_token_2              |
    +-----------------------------------------------------------------------------------------+
```

또는 다음과 같은 방법으로도 사용 가능

```bash

    > remove usergroup list 19 your_token_1
    Remove UserGroup Token list success.
    > show usergroup
    +-----------------------------------------------------------------------------------------+
    |  ID  |   Name    |  Description  |                        Childs                        |
    +=========================================================================================+
    |   1  |  group_A  |               |                                                      |
    |  19  |  group_B  |               |                                                      |
    |  28  |  group_C  |  TEST         |       your_token_2                                   |
    +-----------------------------------------------------------------------------------------+

    > update usergroup list 28 your_token_1,your_token_2
    Update UserGroup Token list success.
    > show usergroup
    +-----------------------------------------------------------------------------------------+
    |  ID  |   Name    |  Description  |                        Childs                        |
    +=========================================================================================+
    |   1  |  group_A  |               |                                                      |
    |  19  |  group_B  |               |                                                      |
    |  28  |  group_C  |  TEST         |              your_token_1, your_token_2              |
    +-----------------------------------------------------------------------------------------+
```

### B. SDAModel Group

SDAModel들로 이루어진 그룹입니다.

- 하나의 token이 여러 sda model group에 접근할 수 있습니다.
- user group의 token들이 쓸 수 있는 sda model을 제한합니다.
- 하나의 backend group과 관계되어 해당 sda model group에 속해있는 sda model을 사용해 sda를 만들면 그 sda는 해당하는 backend group안의 backend들만 사용
- moreh-switch-model로 봤을때 어떤 그룹에 해당하는 sda model인지 확인가능
- moreh_smclient 명령어 : 자세한 파라미터는 smclient에서 확인

```bash
    > show sdamodelgroup
    +--------------------------------------------------------------------+
    |  ID  |  Name  |        Backend Group       |        Childs         |
    +====================================================================+
    |   1  |  mg1   |  default_backend_group(0)  |      small, large     |
    |   2  |  mg2   |  bg1(1)                    |                       |
    +--------------------------------------------------------------------+

    $ moreh-switch-model
    Current Moreh SDA: small at mg1

    1. small mg1 *
    2. large mg1

    Selection (1-2, q, Q):
```

### C. Backend Group

backend들로 이루어진 그룹입니다.

- 하나의 backend는 하나의 그룹에만 들어갈 수 있습니다.
- 기본 그룹[id : 0]이 있어서 처음에는 다 기본그룹에만 들어가 있습니다.
- sda model group과 관계되며 sda 들이 쓸 수 있는 backend를 제한합니다
- moreh_smclient 명령어 : 자세한 파라미터는 smclient에서 확인

```bash

    > show backendgroup
    +---------------------------------------------+
    |  ID  |          Name           |   Childs   |
    +=============================================+
    |   0  |  default_backend_group  |  rx6900-7  |
    |   1  |  bg1                    |            |
    +---------------------------------------------+
```

### D. Relation

user group부터 시작되는 모든 group들간의 전체적인 관계를 보여줍니다.

- moreh_smclient 명령어 : 자세한 파라미터는 smclient에서 확인

```bash
    > show relationship
    +----------------------------------------------------------------------+
    |  User Group(id)  |  SDAModel Group(id)  |      Backend Group(id)     |
    +======================================================================+
    |  ug1(1)          |  mg1(1)              |  default_backend_group(0)  |
    |                  |  mg2(2)              |  bg1(1)                    |
    |  ug2(2)          |  mg1(1)              |  default_backend_group(0)  |
    |                  |  mg2(2)              |  bg1(1)                    |
    +----------------------------------------------------------------------+
```

## 6. 멤버쉽(Membership) 관리하기

user group과 sdamodel group간의 관계를 형성합니다.

- N:M관계이므로 어느 한쪽에 종속될 수 없습니다.
- moreh_smclient 명령어 : 자세한 파라미터는 smclient에서 확인

```bash
  > show membership
  +----------------------------+
  |  ID  |  Name  |   Childs   |
  +============================+
  |   1  |  ug1   |  mg1, mg2  |
  |   2  |  ug2   |  mg1, mg2  |
  +----------------------------+
  > add membership 1 1      # 1은 UserGroupA의 id & 1은 SDAModelGroupA의 id
  Add Membership between User Group and SDAModel group success.
  > remove membership 1 1   # 1은 UserGroupA의 id & 1은 SDAModelGroupA의 id
  Remove Membership between User Group and SDAModel group success.
```