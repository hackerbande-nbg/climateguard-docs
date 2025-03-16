# Service Setup

| Service Name | Port | Description | URL |
| ------------ | ---- | ----------- | --- |
| quantum stage web |8001| quantum stage web server hosted in docker | https://api-stage.quantum.hackerban.de/ |
| quantum stage db |8003| quantum stage postgres db hosted in docker |
| quantum prod web |8000| quantum prod web server hosted in docker | https://api.quantum.hackerban.de/ |
| quantum prod db |8000| quantum prod postgres db hosted in docker |
| nginx reverse proxy |80:81:443| nginx reverse proxy in docker | http://quantum.hackerban.de:81 |

# Server

IP: 138.199.221.22

Firewall (Hetzner cloud): allowed port 80, 81, 443, 22, ICMP

Working dir: /opt/quantum/

github user with github action runner in /home/github (according to andi, this is best practice *eyeroll*)

User:Group for services: quantum:quantumgrp
