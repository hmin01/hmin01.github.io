---
layout: post
title: 우분투에서 Bitcoin core 실행
category: [blockchain]
---

## 일반 네크워크
---

#### 1. 빌드된 블록체인 서비스 서버 실행

Port : 8332

```
cd ~/bitcoin/src

./bitcoind -daemon
( -daemon은 백그라운 실행 옵션 )
```
<div class="twin_blank"></div>

#### 2. 동기화된 블록 수 확인

```
./bitcoin-cli getblockchaininfo
```
<div class="twin_blank"></div>

#### 3. 종료

백그라운드로 실행되고 있는 bitcoin-d의 프로세스 번호 확인

<div class="blank"></div>

```
pre -ef | grep bitcoin
```
<div class="blank"></div>

확인된 프로세스 종료

<div class="blank"></div>

```
kill [Process_number]
```
<div class="third_blank"></div>

## 테스트 네트워크
---

#### 0. 테스트 모드
1. Testnet (Port : 18442)
 
    + 인터넷상에서 동작하는 테스트 네트워크로 테스트용 BTC를 사용하지만 처음 시작할 때, Testnet에 있는 모든 블럭을 동기화해야 함
    
2. Regtest (Port : 18443)

    + 로컬 PC내에서 작동하는 테스트 네트워크로 개인 PC 내에서만 계정을 만들거나 채굴할 수 있으며 블록체인 초기화도 쉽게 할 수 있음

#### 0.1. Regtest 명령어 help

```
./bitcoin-cli -regtest help
```
<div class="blank"></div>

#### 1. 서버 실행

```
./bitcoind -regtest -daemon
( -daemon은 백그라운 실행 옵션 )
```
<div class="blank"></div>

#### 2. 블록 생성

block_count만큼의 블록을 테스트 서버 내에 생성

블록이 100개를 넘지 않으면 송금 등에 이용할 수 없기 때문에 초기에 101개의 블록을 생성
<div class="half-blank"></div>

```
./bitcoin-cli -regtest generate [block_count]
```
<div class="blank"></div>

v0.19.0부터 generate 기능은 더 이상 지원하지 않음

이전 버전에서 `error code: -32` 발생 시, 테스트 서버 실행 명령에 `-deprecatedrpc=generate` 옵션 추가 다시 실행
<div class="half-blank"></div>

```
./bitcoind -regtest -daemon -deprecatedrpc=generate
```
<div class="blank"></div>

#### 3. 생성된 블록 확인

```
./bitcoin-cli -regtest getblockcount
```
<div class="blank"></div>

#### 4. 타 계좌 생성

Account_name이라는 이름을 가진 계좌 생성

```
./bitcoin-cli -regtest getnewaddress [Account_name]
```
<div class="blank"></div>

기본 잔고 확인

```
./bitcion-cli -regtest getbalance
```
<div class="blank"></div>

Account_name이라는 이름을 가진 계좌의 잔고 확인

```
./bitcoin-cli -regtest getbalance [Account_name]
```
<div class="twin_blank"></div>

#### 5. 송금

송금처와 송금액을 지정하여 트랜잭션을 발생시킴, 결과로 트랜잭션의 식별번호(txid)가 반환
```
./bitboin-cli -regtest sendtoaddress [계좌번호] [송금액]
```
<div class="blank"></div>


#### 6. 트랜잭션 확인
```
./bitcoin-cli -regtest listunspent
```
<div class="blank"></div>

#### 7. 미확정된 트랜잭션을 확인
```
./bitcoin-cli -regtest listunspent 0
```
<div class="blank"></div>

#### 8. 블록 생성

트랜잭션을 확정하고 체인에 추가하기 위해 블록을 생성 (채굴)

```
./bitcoin-cli -regtest generate 1
```
<div class="blank"></div>