# Kubernetes-minikube installation process on ubuntu20.04


# k8s minikube+docker的安装

## **安装前准备**

Container 容器本地为docker；

## **docker的安装** 

1.  如果之前有安装过docker，可以先卸载：

```
apt-get remove docker docker-engine [http://docker.io](https://link.zhihu.com/?target=http%3A//docker.io) 
```

2.  更新apt安装包索引

```
apt-get update 
```

3.  安装软件包以允许apt通过HTTPS

```
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common 
```

4.  添加Docker官方的GPG密钥

```
curl -fsSL [https://download.docker.com/linux/ubuntu/gpg](https://link.zhihu.com/?target=https%3A//download.docker.com/linux/ubuntu/gpg) | sudo apt-key add - 
```

5.  安装稳定版仓库

```
sudo add-apt-repository "deb \[arch=amd64\] [https://download.docker.com/linux/ubuntu](https://link.zhihu.com/?target=https%3A//download.docker.com/linux/ubuntu) $(lsb_release -cs) stable" 
```

6.  安装docker

```
apt-get install [http://docker.io](https://link.zhihu.com/?target=http%3A//docker.io) 
```

7.  启动docker服务

```
systemctl start docker 
```

修改daemon配置文件/etc/docker/daemon.json来使用加速器：

```
cd /etc/docker #在daemon.json文件末尾追加如下配置： sudo tee /etc/docker/daemon.json <<-'EOF' {  "registry-mirrors": ["https://dhx52mku.mirror.aliyuncs.com"] } EOF ​ # 重启docker sudo systemctl daemon-reload sudo systemctl restart docker 
```

## **安装minikube**

## **安装步骤**

1.  直接安装minikube

```
curl -Lo minikube [https://kubernetes.oss-cn-hangzhou.aliyuncs.com/minikube/releases/v1.23.1/minikube-linux-amd64](https://link.zhihu.com/?target=https%3A//kubernetes.oss-cn-hangzhou.aliyuncs.com/minikube/releases/v1.23.1/minikube-linux-amd64) && chmod +x minikube && sudo mv minikube /usr/local/bin/ 
```

2.  启动minikube

```
# 默认会使用docker容器。 minikube start 
```

3.  让minikube下载kubectl客户端命令工具

```
minikube kubectl -- get po -A 
```

## **开启控制台**

```
minikube dashboard 
```

### 访问服务器dashboard 

通过`kubectl proxy`方式：

```
kubectl proxy --port=12345 --address='192.168.8.x' --accept-hosts='^.*' 
```

## **直接使用** 

minikube的命令 alias：

```
alias kubectl="minikube kubectl --" 
```

```
$ kubectl kubectl controls the Kubernetes cluster manager. ​  Find more information at: https://kubernetes.io/docs/reference/kubectl/overview/ ​ Basic Commands (Beginner):  create        Create a resource from a file or from stdin expose        Take a replication controller, service, deployment or pod and expose it as a new Kubernetes service  run           在集群中运行一个指定的镜像 set           为 objects 设置一个指定的特征 ​ Basic Commands (Intermediate):  explain       Get documentation for a resource get           显示一个或更多 resources edit          在服务器上编辑一个资源 delete        Delete resources by file names, stdin, resources and names, or by resources and label selector ... 
```

Step 5: Install Rancher

```
docker run -d --restart=unless-stopped -p 8080:8080 rancher/server:stable 
```

## Addon 组件

```
minikube addons list 
```
