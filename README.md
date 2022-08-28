# 리눅스 마스터 1급 연습

## CentOS7 docker container 
```
docker run --privileged -d --name centos7-practice centos:7 /sbin/init

docker exec -it centos7-practice bash
```