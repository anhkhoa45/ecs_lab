## Lab 1: Cài đặt và chạy container Hello World

1. Install docker engine

https://docs.docker.com/engine/install/

2. Verify that Docker Engine is installed correctly by running the hello-world image:
```
sudo docker run hello-world

```
## Lab 2: Xem thư viện của docker sau khi cài đặt

```
cd /var/lib/docker
```

## Lab 3: Tìm kiếm một image và download image

```
docker search nginx
```
```
docker pull nginx 
```
```
docker image ls -a
``` 

## Lab 4: Tạo một Dockerfile và build docker image
- Nội dung Dockerfile
```
FROM ubuntu
CMD ["echo", "Hello AWS 03 Class!"]
```

- Build docker image từ docker image vừa tạo
```
docker build --tag testimage:var1 .
```

## Lab 5:  Chạy một container với docker image vừa tạo
```
docker run image_name:image_tag
```

## Lab 6: Tạo docker networking
```
docker network create -d bridge test-bridge
```
Check networking vừa tạo
```
docker network list
```
Khởi tạo mạng với driver bridge có subnet 10.10.0.0/16, ip gateway là 10.10.0.1
```
docker network create -d bridge  --subnet=10.10.0.0/16 --gateway=10.10.0.1  test-bridge1
```
Review network vừa tạo
```
docker network inspect test-bridge1
```

## Lab 7: Chạy một container trong network vừa tạo và kiểm tra
```
docker run --network=test-bridge1 -itd --name=container1 testimage:var1
``` 
```
docker inspect container1
```

## Lab 8: Chạy thêm 2 container cùng network và khác network để kiểm tra kết nối bằng ping
```
docker exec -it container_name /bin/bash
```

## Lab 9: Kiểm tra volume trong docker

```
docker volume list
```

Tạo một volume mới
```
docker volume create volume1 
```

```
docker volume ls
```

```
docker volume inspec volume1
```
 
## Lab 10: Chạy một container với volume vừa tạo

```
docker run -d -it --name test-container --volume "volum1":/tmp ubuntu:xenial
```

Kiểm tra mount point trong folder và exec vào container
```
docker exec -it container_name /bin/bash
```

## Lab 11: Mapping port của container và port của host

```
docker run -d -p 80:80 nginx
```

Check application chạy trên container http://host_ip:80

-------------------Advanced Lab----------------------------

## Lab 12: Xem lịch sử build một docker image

Tạo một Dockerfile mới
```
FROM ubuntu
RUN apt-get update && apt-get install python2 -y
RUN apt-get install python3-pip -y
RUN pip install flask flask-mysql
COPY . /opt/source-code
ENTRYPOINT FLASK_APP=/opt/source-code/app.py flask run
```

Build image từ Dockerfile vừa tạo
```
docker build -t python-image .
```

```
docker history image_name:tags
```

## Lab 13: Docker Compose

```
docker compose up
```