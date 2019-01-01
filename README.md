# 自行车共享网络 <img src="https://github.com/vonbenjamin/hello-world/blob/master/sysu.jpg" alt="图片说明" width="110" height="100" align='right'>
![final](https://img.shields.io/badge/完成-final-green.svg)
![BlockChain](https://img.shields.io/badge/BlockChain-519dd9.svg)
![Hyperledger Fabraic](https://img.shields.io/badge/Fabric-1.1.0-519dd9.svg)
# 搭建环境
## 开发环境
Ubuntu 16.04 LTS 64-bit
## 安装Node.js,npm,Docker,Docker Composer,Python
``` 
$curl -O https://hyperledger.github.io/composer/latest/prereqs-ubuntu.sh
$ chmod u+x prereqs-ubuntu.sh
$ ./prereqs-ubuntu.sh
```
## 安装Hyperledger Composer
Hyperledger Composer 是一个开放的开发框架、工具集，可以帮助人们更容易地开发、部署区块链应用。它支持 Fabric，并提供 Javascript SDK。我们可以通过 npm 来安装它的一系列组件.
#### 1.安装Composer命令行CLI
```$ npm install -g composer-cli```

许多操作（安装、部署、管理）都将通过 Composer CLI 完成.
#### 2.安装Composer REST Server
```$ npm install -g composer-rest-server```

Composer REST server 可以根据我们开发、部署的区块链应用自动生成一些 RESTful API 接口，以方便通过浏览器、curl 等工具对之进行访问。
#### 3.安装Yeoman
```$ npm install -g yo```

Yeoman 能根据定义好的 generator 迅速生成我们所需要的项目、应用的框架.
#### 4.安装Hyperledger Fabric Runtime
```
$ curl -O https://raw.githubusercontent.com/hyperledger/composer-
tools/master/packages/fabric-dev-servers/fabric-dev-servers.tar.gz
$ tar -xvf fabric-dev-servers.tar.gz
$ ./downloadFabric.sh
```

我们就非常迅速、方便的完成了 Fabric 的下载，及部署环境的安装，得益于 Docker Container 技术，并不需要我们做复杂的配置。





## 区块链本地部署：
#### 1.启动Fabric
```./startFabric.sh```
#### 2.生成并导入PeerAdmin Card
```./createPeerAdminCard.sh```
#### 3.准备业务网络
```yo hyperledger-composer:businessnetwork```
#### 4.进入bikesharing-blockchain目录
#### 5.生成.bna文件
```composer archive create --sourceType dir --sourceName .```
#### 6.部署业务网络bikesharing-network
```composer network install --card PeerAdmin@hlfv1 --archiveFile bikesharing-network@0.0.1.bna```
#### 7.启动业务网络
```composer network start --networkName bikesharing-network --networkVersion 0.0.1 --networkAdmin admin --networkAdminEnrollSecret adminpw --card PeerAdmin@hlfv1 --file admin.card```
#### 8.导入tutorial-network管理员Card
```composer card import --file admin.card```
#### 9.确认 tutorial-network 安装成功
``` composer network ping -c admin@bikesharing-network```
#### 10.启动REST Server
```composer-rest-server --card admin@bikesharing-network --namespaces "never" --port 3100```
#### 11.在浏览器输入：localhost:3100/exploree即可进入自行车共享网络  


