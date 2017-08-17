
# 使用 ``docker-compose`` 快速部署 Jenkins + SonarQube

## Version
- CentOS Linux release 7.2.1511 (Core)
- Linux version 3.10.0-327.4.5.el7.x86_64
- Docker 17.05.0-ce
- Docker-compose 1.13
- MySQL 5.7
- Sonarqube 6.4 
- Jenkins 2.6

## 目录结构

```
├── mysql
│   └── docker-compose.yml
│
├── jenkins-sonarqube
│   │
│   ├── docker-compose.yml
│   ├── jenkins_home
│   ├── sonarqube_home
│ 
└── README.md
```

## 部署流程

docker & docker-compose 的安装步骤请自行 Google


``git clone https://github.com/slowlog/docker-jenkins-sonarqube.git``



### Step 1、创建网关
``docker network create internal``

### Step 2、构建 MySQL

```
cd mysql

#构建
docker-compose up -d

#创建数据库
create database sonar;

#授权
grant all privileges on sonar.* to sonar@'%' identified by 'yy123456';

#刷新
FLUSH PRIVILEGES;

```
### Step 3、构建 Jenkins 和 SonarQube
```
cd jenkins-sonarqube

#修改挂载目录的权限
chown -R 1000.1000 jenkins_home/

#构建
docker-compose up -d

```
### Done
- Jenkins 访问 ``http://your ip:8092``
- SonarQube 访问 ``http://your ip:8093`` 默认 admin admin

> 注: up 不起来的话可通过 ``docker-compose logs`` 查看构建日志排查错误







