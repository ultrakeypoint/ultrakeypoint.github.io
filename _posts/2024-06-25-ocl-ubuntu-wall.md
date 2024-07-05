---
layout: post
title: 오라클 클라우드 우분투 기본 설정
date: 2024-06-26
image: /assets/images/blog/2024-06-26/1.png
author: ultrakeypoint
tags: [dev, 우분투, 방화벽]
---

오라클 클라우드 컴퓨터 인스턴츠 관리 관련 기본적으로 해야될 설정을 메모합니다. 설정하지 않으면 SSH 사용 시 멈추거나 서버가 다운되는 현상이 있기 때문에 필수사항은 반드시 적용해서 안정적인 서버 운영에 도움되세요

##### 포트 설정

```bash
# 80번 포트 개방 http
sudo iptables -I INPUT 1 -p tcp --dport 80 -j ACCEPT

# 443번 포트 개방 https
sudo iptables -I INPUT 1 -p tcp --dport 443 -j ACCEPT

# 재부팅시에도 적용 되도록 저장
sudo netfilter-persistent save

# 리로드
sudo netfilter-persistent reload

```

##### 메모리 스왑 설정

```bash
#fallocate 명령을 이용한 더미 파일 생성
sudo fallocate -l 4G /swapfile

#dd 명령을 이용한 더미 파일 생성
sudo dd if=/dev/zero of=/swapfile bs=1M count=4096

#권한 설정
sudo chmod 600 /swapfile

#스왑파일 생성
sudo mkswap /swapfile

#스왑메모리 활성화
sudo swapon /swapfile

#메모리 확인
free -m

#재부팅 자동 추가
sudo vi /etc/fstab

# 내용 추가
/swapfile swap swap defaults 0 0

```

##### 백그라운드 프로세스 실행/종료

```bash

pm2 start all
pm2 delete all


```
