## 如果觉得还有点用，麻烦用一下我的邀请码631441，有加成卡15张，我也有推广收入。

### 迄今为止最小的甜糖星愿镜像

方法一：

打开混杂(这步可以省略,如果不能正常工作再打开)
```
ip link set eth0 promisc on
```
创建网络（自行替换网关以及网段）
```
docker network create -d macvlan --subnet=192.168.2.0/24 --gateway=192.168.2.88 -o parent=eth0 -o macvlan_mode=bridge macnet
```
运行容器（自行替换路径、IP以及可选替换dns）

```
docker run -itd \
  -v /mnt/data/ttnode:/mnts \
  --name ttnode \
  --net=macnet --ip=192.168.2.2 --dns=114.114.114.114 --mac-address C2:F2:9C:C5:B2:94 \
  --privileged=true \
  --restart=always \
  ericwang2006/ttnode
```
方法二： 直接主网络运行（替换路径）
```
docker run -itd \
  -v /mnt/data/ttnode:/mnts \
  --name ttnode \
  --net=host \
  --privileged=true \
  --restart=always \
  ericwang2006/ttnode
```
进入容器：
```
docker attach ttnode
or
docker exec -it ttnode /bin/bash 
```
查询UUID：
```
./usr/node/ttnode -p /mnts
or# 可能是东半球最小的甜糖星愿镜像

- 基于debian:stable-slim构建
- 去除了crontab任务，改用脚本监控ttndoe进程
- docker日志中直接查询UID
- 完全开源

# 食用方法

如果是arm架构（例如N1盒子），可直接使用，如果是x86平台，是不支持arm架构镜像，因此我们可以运行一个新的容器让其支持该特性。

```
docker run --rm --privileged multiarch/qemu-user-static --reset -p yes
```

## 方法一

打开混杂(这步可以省略,如果不能正常工作再打开)
```
ip link set eth0 promisc on
```
创建网络（自行替换网关以及网段）
```
docker network create -d macvlan --subnet=192.168.2.0/24 --gateway=192.168.2.88 -o parent=eth0 -o macvlan_mode=bridge macnet
```
运行容器（自行替换路径、IP以及可选替换dns）

```
docker run -itd \
  -v /mnt/data/ttnode:/mnts \
  --name ttnode \
  --net=macnet --ip=192.168.2.2 --dns=114.114.114.114 --mac-address C2:F2:9C:C5:B2:94 \
  --privileged=true \
  --restart=always \
  ericwang2006/ttnode
```

## 方法二： 直接主网络运行（替换路径）
```
docker run -itd \
  -v /mnt/data/ttnode:/mnts \
  --name ttnode \
  --net=host \
  --privileged=true \
  --restart=always \
  ericwang2006/ttnode
```

## 进入容器：

```
docker attach ttnode
or
docker exec -it ttnode /bin/bash 
```

## 查询UUID：

```
./usr/node/ttnode -p /mnts
or
#容器外执行
docker logs ttnode
```

# 已知问题

- 日志中会提示**cannot create /proc/sys/net/core/wmem_max: Directory nonexistent**，是因为在daocker中不能设置Linux内核参数，不影响使用
- docker中ttnode第一次启动后大约20秒后有自动退出的概率，不用理会，脚本会再次启动ttnode

```
[2020-11-18 10:25:12] ttnode进程不存在,启动ttnode,
/bin/sh: 1: cannot create /proc/sys/net/core/wmem_max: Directory nonexistent,
如果不能自动发现设备,请将此UID e1c8191de1e1e16a67e05ab3d7bc86ba 生成二维码并用甜糖客户端扫描添加,
[2020-11-18 10:25:34] ttnode启动失败,再来一次,
/bin/sh: 1: cannot create /proc/sys/net/core/wmem_max: Directory nonexistent,
```
# 如果觉得还有点用，麻烦用一下我的邀请码631441，有加成卡15张，我也有推广收入

#容器外执行
docker logs ttnode
```