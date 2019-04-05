---
layout: post
title: 맥북에 프라이빗 블록체인 구축 (using Ethereum Wallet)
category: [blockchain]
---

## 준비 과정
---

#### 1. Ethereum Wallet 설치

https://github.com/ethereum/mist/release에서 Ethereum Wallet(MacOS version) 다운로드

마운트 후, /Applications 내로 Ethereum Wallet.app를 이동
<div class="third_blank"></div>

#### 2. Geth 설치

https://geth.ethereum.org/downloads에서 geth.tar.gz 다운로드

압축 해제 후, /usr/local/bin에 geth를 복사

명령어 : `cp 압축_해제된_geth경로/geth /usr/local/bin`
<div class="third_blank"></div>

#### 3. genesis.json

아래의 내용과 같이 genesis.json 생성 (생성 위치 : ~/Library/Ethereum)

```
{
"config": {
        "chainId": 원하는 고유ID (숫자, 1~30은 제외),
        "homesteadBlock": 0,
        "eip155Block": 0,
        "eip158Block": 0
          },
"difficulty" : "0x20000",
"gasLimit"   : "0x2fefd8",
"alloc"      : {},
"coinbase"   : "0x0000000000000000000000000000000000000000",
"extraData"  : "",
"nonce"      : "0x0000000000000000",
"mixhash"    : "0x0000000000000000000000000000000000000000000000000000000000000000",
"parentHash" : "0x0000000000000000000000000000000000000000000000000000000000000000",
"timestamp"  : "0x00"
}
```
<div class="blank"></div>

#### 4. Data 디렉터리 생성

```
geth -datadir 디렉터리_이름 init genesis.json
```
<div class="blank"></div>

#### 5. 구축을 위한 설정

```
geth —networkid 설정한_ID —datadir 생성한_디렉터리_이름 —rpc —rpcport 8545 —rpccorsdomain “*” —rpcapi “admin,db,eth,debug,miner,net,shh,txpool,personal,web3” console
```
<div class="blank"></div>

#### 6. 설정을 기반으로 Ethereum Wallet 실행

```
"/Applications/Ethereum Wallet.app/Contents/MacOS/Ethereum Wallet" --rpc //.pipe/geth.ipc
```