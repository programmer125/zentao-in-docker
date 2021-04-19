# zentao-in-docker
在docker中运行禅道，禅道官网地址 https://www.zentao.net/

## 部署
### 克隆代码到本地
```bash
git clone https://github.com/programmer125/zentao-in-docker.git
```

### 下载禅道一键安装包
```bash
wget https://www.zentao.net/dl/zentao/15.0.rc3/ZenTaoPMS.15.0.rc3.zbox_64.tar.gz -O zentao-in-docker/zentao.tar.gz
```

### 构建docker镜像
```bash
docker build -t zentao zentao-in-docker/.
```

### 启动容器
```bash
docker run -it -p 80:80 zentao /bin/bash
```

### 在容器中启动服务
```bash
/opt/zbox/zbox start
```

### 浏览器访问 http://127.0.0.1:80
```
账号：admin 密码：123456
```

## 迁移
如果需要迁移已经部署的禅道，按以下步骤。
```bash
# 从现有容器中拷贝mysql数据
docker cp {容器名称或id}:/opt/zbox/data/mysql/zentao .
# 从现有容器中拷贝附件
docker cp {容器名称或id}:/opt/zbox/app/zentao/www/data/upload/1 .
# 挂在到新的容器
docker run -v zentao/:/opt/zbox/data/mysql/zentao -v 1/:/opt/zbox/app/zentao/www/data/upload/1 ...
```
