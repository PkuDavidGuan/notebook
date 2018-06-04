# ubuntu安装docker

```shell
sudo apt-get remove docker docker-engine docker-ce docker.io #先卸载可能存在的旧版本
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install -y docker-ce
apt-cache madison docker-ce #这会列出可用的版本，第二列是版本字符串，第三列是存储库名称
sudo apt-get install docker-ce=<VERSION> #从选出的版本中选择一个安装

systemctl status docker #查看docker服务是否启动
sudo systemctl start docker #启动docker
sudo docker run hello-world #成功！
```

> 参考：https://blog.csdn.net/bingzhongdehuoyan/article/details/79411479