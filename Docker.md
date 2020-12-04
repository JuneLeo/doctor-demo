#Docker
* 配置加速器
  ```
  # 第一种方法：
  curl -sSL https://get.daocloud.io/daotools/set_mirror.sh | sh -s http://f1361db2.m.daocloud.io

  # 第二种方法
  vi /etc/docker/daemon.json
  # add info:"registry-mirrors": [ "https://registry.docker-cn.com" ]
  ```
* docker重启
    ```
    # docker servcie启动
    sudo service docker start
    # docker启动
    sudo systemctl start docker
    # 重载所有修改过的配置文件
    sudo systemctl daemon-reload
    # 重启docker
    sudo systemctl restart docker
    ```
* 常用命令
      ```
      # 查看images列表
      docker images
      # 查看版本信息
      docker version
      # 查看docker信息
      docker info
      # 查看docker进程列表
      docker ps
      # 开机启动
      docker sudo systemctl enable docker
      # 重启docker
      sudo systemctl restart docker
      ```
* 创建分组
        ```
        # 创建docker分组
        sudo groupadd docker
        # 把当前用户加入docker分组
        sudo usermod -aG docker $USER
        ```
* 容器操作
          ```
          # 拉取centos系统
          docker pull centos
          # 运行centos系统
          # -it: 交互式终端
          # --rm: 容器退出后将其删除，避免空间浪费
          docker run -it --rm centos bash
          # 查看当前系统版本
          cat /etc/os-release
          # 查看容器列表
          docker container ls
          # 查看容器输出
          docker container logs containerID
          # 查看镜像、容器、数据卷所占用的空间
          docker system df
          # 展示无标签镜像（虚悬镜像）
          docker image ls -f dangling=true
          # 删除无标签
          docker image prune
          ```
* 容器获取
      ```
      # 拉取镜像
      sudo docker pull ubuntu
      # 通用镜像名拉取
      sudo docker pull openresty/openresty:1.13.6.2-alpine
      # 查看images
      sudo docker images
      # 搜索某个镜像
      sudo docker search ubuntu
      # 查看镜像详细信息
      sudo docker inspect redis:3.2
      # 根据id中前几个字母查询镜像
      sudo docker inspect 2da
      # 删除镜像(后可跟多个id)
      sudo docker rmi ubuntu:latest redis:4.0
      ```
* 运行、管理容器
        ```
        # 创建容器
        sudo docker create nginx:1.12
        # 【通过重命名】创建容器
        sudo docker create --name nginx nginx:1.12
        # 启动容器
        sudo docker start nginx
        # 使用run替代（create + start）合并为一步，【-d/--detach：后台运行】
        sudo docker run --name nginx -d nginx:1.12
        # 罗列docker容器（在运行的）
        sudo docker ps
        # 罗列docker容器（所有的）
        sudo docker ps -a/--all
        # 停止容器
        sudo docker stop nginx
        # 删除容器
        sudo docker rm nginx
        # 强制删除容器
        sudo docker rm -f/--force nginx

        # ========== 进入容器 start ==============
        # 查看容器主机名定义
        sudo docker exec nginx more /etc/hostname
        # 进入控制台
        # -i: 保持输出流
        # -t: 启用一个伪终端【查看程序运行的过程】
        sudo docker exec -it nginx bash
        ```
* 容器互联
          ```
          # 两个容器互联
          sudo docker run -d --name mysql -e MYSQL_RANDOM_ROOT_PASSWORD=yes mysql
          sudo docker run -d --name webapp --link mysql webapp:latest
          # 数据库连接地址如下：
          String url = "jdbc:mysql://mysql:3306/webapp";

          ```
* docker用户
  * sudo groupadd docker    #添加docker用户组
  * sudo gpasswd -a $USER docker    #将登陆用户加入到docker用户组中
  * newgrp docker    #更新用户组
* 下载镜像
  * docker pull ubuntu:18.04
* 列出镜像
  * docker image ls
* 删除镜像
  * docker image rm
* 运行镜像
  * docker run --name webserver -d -p 80:80 nginx
  * docker exec -it webserver bash
  * docker diff webserver
*   
