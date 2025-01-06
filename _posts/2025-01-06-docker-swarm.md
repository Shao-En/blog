---
layout: post
title: docker swarm
date: 2025-01-06 11:30 +0800
---
### docker swarm
```
# manager node 
docker swarm init
# worker node join
docker swarm join --token <TOKEN> <MANAGER-IP>:2377
# service
docker service ps
docker service update --force <service_name>
```

### Service層
docker swarm的service層提供了Load Balancing 和 Service Discovery
Load Balancing
* 自動在多個container內分配流量，RR算法，不可自己更改
* 流量通過Virtual IP或DNS RR機制轉發

Service Discovery
* container訪問方式簡單，可用service_name直接訪問，不用關心具體IP

### Stack
docker swarm使用Stack部屬 docker-compose.yml
```
docker stack deploy -c <compose file> <stack_name>
```

### Service高可用
一般service可以直接增加replicas數量
```
docker service update --replicas <number> <service_name>
```
有主從架構的SQL、mongodb、redis、emqx、elasticsearch需要配置mamager、worker node，並且配置fillover/fillback機制，保障高可用和資料一致性。

Cluster模式補充在各自章節