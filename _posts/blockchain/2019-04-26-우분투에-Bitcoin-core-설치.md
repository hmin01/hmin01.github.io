---
layout: post
title: 우분투에 Bitcoin core 설치
category: [blockchain]
---

## 준비 과정
---

#### 1. System update

```
sudo apt-get update
```
```
sudo apt-get upgrade
```
<div class="twin_blank"></div>

#### 2. Install package

```
ssudo apt-get install build-essential libtool autotools-dev autoconf pkg-config libssl-dev
```
```
sudo apt-get install libboost-all-dev
```
```
sudo apt-get install libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler
```
```
sudo apt-get install libqrencode-dev autoconf openssl libssl-dev libevent-dev
```
```
sudo apt-get install libminiupnpc-dev
```
<div class="twin_blank"></div>

#### 3. Download bitcoin core source

Git이 설치되어 있지 않을 경우, `sudo apt-get install git` 명령으로 Git 설치

<div class="blank"></div>

```
git clone https://github.com/bitcoin/bitcoin.git
```
<div class="third_blank"></div>

## 설치
---

#### 4. Install berkeley DB

Wallet을 사용하려면 요구되는 DB로 Wallet을 사용하지 않을 경우, 설치하지 않아도 됨
<div class="blank"></div>

##### 4.1. Create directory
```
cd ~
mkdir bitcoin/db4
cd bitcoin/db4
```
<div class="blank"></div>

##### 4.2. Download berkeley DB
```
wget 'http://download.oracle.com/berkeley-db/db-4.8.30.NC.tar.gz'

or

./contrib/install_db4.sh `pwd`
```
<div class="blank"></div>

##### 4.3. Decompress berkeley DB
```
tar -xzvf db-4.8.30.NC.tar.gz
```
<div class="blank"></div>

##### 4.4. Move Decompressed directory
```
cd db-4.8.30.NC
```
<div class="blank"></div>

##### 4.5. Create directory and move
```
mkdir build-unix
cd build-unix
```
<div class="blank"></div>


##### 4.6. Set configure and install berkeley DB
```
../dist/configure --enable-cxx --disable-shared --with-pic --prefix=/home/[username]/bitcoin/db4/
```
<div class="blank"></div>

##### 4.7. install berkeley DB
```
make install
```
<div class="twin_blank"></div>

#### 5. Configure
```
cd ~/bitcoin

./configure LDFLAGS="-L/home/[Username]/bitcoin/db4/lib/" CPPFLAGS="-I/home/[Username]/bitcoin/db4/include/"
```
<div class="twin_blank"></div>

#### 6. Compile bitcoin, berkeley DB 4.8

```
make -s -j5
```
<div class="twin_blank"></div>

#### 7. Successful if file below exists

```
cd ~/bitcoin

./src/bitcoin-cli
./src/bitcoind
./src/qt/bitcoin-qt
```
<div class="third_blank"></div>