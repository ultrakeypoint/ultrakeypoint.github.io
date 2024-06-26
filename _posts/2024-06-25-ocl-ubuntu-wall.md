---
layout: post
title: OCI 우분투 서버 방화벽 설정
date: 2024-06-26
image: /assets/images/blog/2024-06-26/1.png
author: ultrakeypoint
tags: [dev, 우분투, 방화벽]
---

오라클 클라우드 우분투 서버 방화벽 설정

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
