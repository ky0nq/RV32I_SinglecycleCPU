# RV32I Single-Cycle CPU

RISC-V **RV32I Base Integer Instruction Set**을 기반으로 구현한 Single-Cycle CPU RTL 프로젝트입니다.

## Overview

각 명령어를 한 Clock Cycle 안에서 Fetch → Decode → Execute → Memory → Write Back까지 수행하도록 Datapath와 Control Logic을 설계합니다.

```text
Instruction Fetch
       ↓
Instruction Decode
       ↓
Register File
       ↓
ALU / Branch
       ↓
Data Memory
       ↓
Write Back
```

## Architecture

```text
        +-------------+
PC ---->| Instruction |
        |   Memory    |
        +------+------+
               |
               v
        +------+------+
        |  Decoder /  |
        | Control Unit|
        +------+------+
               |
       +-------+-------+
       |               |
       v               v
+------+-----+    +----+----+
| Register   |--->|   ALU   |
|   File     |    +----+----+
+------+-----+         |
       ^               v
       |         +-----+------+
       +---------| Data Memory|
                 +------------+
```

## Main Modules

| Module | Role |
|---|---|
| Program Counter | 현재 Instruction Address 저장 |
| Instruction Memory | Instruction Fetch |
| Control Unit | Opcode 기반 Control Signal 생성 |
| Immediate Generator | Immediate 확장 |
| Register File | `x0` ~ `x31` Register |
| ALU | Arithmetic / Logic Operation |
| Branch Logic | Branch Condition 판정 |
| Data Memory | Load / Store |
| Write-back MUX | Register Write Data 선택 |
| CPU Top | 전체 Datapath 연결 |

## RV32I Instruction Groups

- R-Type Arithmetic / Logic
- I-Type Arithmetic
- Load
- Store
- Branch
- Jump
- Upper Immediate

> 실제 구현한 Instruction 범위에 맞게 목록을 갱신해 주세요.

## Single-Cycle Datapath

Single-Cycle 구조에서는 모든 주요 동작이 하나의 Clock Period 안에 완료됩니다.

장점:

- 구조가 직관적
- Instruction Datapath 학습에 적합
- Control Logic 추적이 쉬움

제약:

- 가장 긴 Critical Path가 Clock Frequency를 제한
- 복잡한 명령도 한 Cycle 안에 처리해야 함

## Verification

- Register Arithmetic
- Immediate Arithmetic
- Load / Store
- Branch Taken / Not Taken
- Jump
- `x0` Register 고정
- Signed / Unsigned Operation
- ALU Control
- PC Update
- Program-level Simulation

## Development Environment

- SystemVerilog
- RISC-V RV32I
- RTL Simulation
- FPGA / Vivado
