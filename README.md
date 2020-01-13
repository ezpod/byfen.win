# Fabric区块链BYFN网络一键启动工具【Windows环境】

**Byfn.win** 是Hyperledger Fabric著名的byfn.sh脚本的Windows版本的移植，用于帮助开发人员在Windows环境中快速搭建Hyperledger Fabric链码及应用开发环境。官方下载地址：[http://sc.hubwiz.com/codebag/byfn-win/](http://sc.hubwiz.com/codebag/byfn-win/)。


## 1、开发包概述

Byfn.win的主要特点如下：

- 使用原生构建的windows版本的Fabric程序，不需要安装虚拟机/Linux子系统/Docker
- 一键复位BYFN网络，一键启动BYFN网络，为开发人员节省大量时间和精力
- 支持TLS安全传输设置，支持solo共识和etcdraft共识
- 支持Hyperledger Fabric官方及第三方提供的各种语言的链码与应用开发包
- 解压即用，绿色软件

Byfn.win采用Golang开发，目前版本是1.0.0，主要文件清单如下：

<table class="table table-striped">
  <thead>
    <tr><th>文件</th><th>说明</th></tr>
  </thead>
  <tbody>
    <tr><td>byfn.exe</td><td>byfn.win主程序</td></tr>
    <tr><td>first-network/</td><td>BYFN网络配置目录</td></tr>
    <tr><td>first-network/crypto-config.yaml</td><td>BYFN密码学资料配置</td></tr>
    <tr><td>first-network/configtx.yaml</td><td>BYFN创世区块配置</td></tr>
    <tr><td>first-network/ccp-template.json</td><td>连接配置文件json模板</td></tr>
    <tr><td>first-network/ccp-template.yaml</td><td>连接配置文件yaml模板</td></tr>
    <tr><td>first-network/orderer.yaml</td><td>Fabric排序节点配置</td></tr>
    <tr><td>first-network/core.yaml</td><td>Fabric对等节点核心配置</td></tr>
    <tr><td>first-network/e2e.cmd</td><td>端到端测试脚本</td></tr>
    <tr><td>chaincode_example02/go/</td><td>Golang链码，演示</td></tr>
    <tr><td>chaincode_example02/node/</td><td>Node.js链码，演示</td></tr>
    <tr><td>chaincode_example02/java/</td><td>Java链码，演示</td></tr>
    <tr><td>fabric/bin/</td><td>Fabric原生程序目录</td></tr>
    <tr><td>byfn.win/</td><td>byfn.win源代码目录</td></tr>
    <tr><td>byfn.win/go.mod</td><td>go module配置文件</td></tr>
    <tr><td>byfn.win/main.go</td><td>入口代码</td></tr>
    <tr><td>byfn.win/pkg/cmd/bygn.go</td><td>命令行处理代码</td></tr>
    <tr><td>byfn.win/pkg/shell/shell.go</td><td>操作系统接口代码</td></tr>
    <tr><td>byfn.win/pkg/shell/generate.go</td><td>BYFN网络资料生成代码</td></tr>
    <tr><td>byfn.win/pkg/shell/network.go</td><td>BYFN网络运行与管理代码</td></tr>
  </tbody>
</table>

## 2、Byfn.win使用说明

### 2.1 生成BYFN网络基础资料

使用`byfn.exe`的`reset`子命令来生成或复位BYFN网络运行所依赖的基础资料：

![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-zcjaXevY-1578879474761)(byfn-for-windows/byfn-reset.png)\]](https://img-blog.csdnimg.cn/2020011309390355.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NoZWJhbzMzMzM=,size_16,color_FFFFFF,t_70)

注意：

1. 每次执行`reset`命令都会清空已有的区块链数据和密码学资料
2. 节点的输出日志在first-network/logs目录下

### 2.2 启动BYFN网络

使用`byfn.exe`的`up`子命令来启动BYFN网络：

![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-poyJCTMC-1578879474763)(byfn-for-windows/byfn-up.png)\]](https://img-blog.csdnimg.cn/20200113093944452.png)

`up`子命令的选项如下：

- --tls：启用tls，默认：false
- --full / -f：是否启动所有节点，默认：false，仅启动一个节点
- --orderer / -o：选择排序器实现，默认：solo，可选：solo或etcdraft。

默认情况下，byfn.win禁用TLS并仅启动一个排序节点和一个对等节点，即：

- orderer.example.com
- peer0.org1.example.com

可以使用上述选项切换启动设置，例如启用tls、etcdraft排序并启动所有peer节点：

![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-8IhZ1vng-1578879474764)(byfn-for-windows/byfn-up-2.png)\]](https://img-blog.csdnimg.cn/2020011309400438.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NoZWJhbzMzMzM=,size_16,color_FFFFFF,t_70)

### 2.3 进入Peer节点管理控制台

使用`byfn.exe`的`admin`子命令进入peer节点的管理控制台：

![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-5j70eteS-1578879474765)(byfn-for-windows/byfn-admin.png)\]](https://img-blog.csdnimg.cn/20200113094010902.png)

`admin`子命令的选项如下：

- --peer / -p：设置节点编号，默认：0
- --org / -o：设置机构编号，默认：1

默认情况下进入peer0.org1.example.com的管理控制台，可以使用上述选项进入不同的peer节点的控制台，例如进入peer1.org2.example.com的管理控制台：

```
byfn admin -p 1 -o 2
```

注意：

1. 当网络启用了TLS时，在进入管理终端时也需要启用tls，例如：

```
byfn admin --tls
```

2. peer命令需要额外的tls相关的参数，例如：

```
> peer channel list --tls --cafile=%ORDERER_CA%
```

其中环境变量`ORDERER_CA`中已经设置了相应的路径，可以直接使用。

### 2.4 执行端到端测试

进入管理控制台后，可以调用`e2e.cmd`来进行基本的测试：

![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-Q3oTwTk4-1578879474766)(byfn-for-windows/byfn-e2e.png)\]](https://img-blog.csdnimg.cn/20200113094025842.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NoZWJhbzMzMzM=,size_16,color_FFFFFF,t_70)

e2e.cmd主要执行如下任务：

- 启动预置的链码chaincode_example02
- 创建通道mychannel
- 将peer0.org1.example.com加入mychannel
- 在peer0.org1.example.com安装链码mycc:0
- 在通道mychannle激活链码mycc:0
- 查询链码mycc:0的状态
- 提交交易修改链码mycc:0的状态
- 再次查询链码mycc:0的状态
- 关闭链码chaincode_example02

### 2.5 在管理控制台使用fabric预置命令

e2e.cmd是一个标准的windows批处理文件，每一个命令都可以在管理控制台单独执行。

例如，下面的三个命令分别用于查询当前所管理节点加入的通道、当前节点安装的链码和指定通道激活的链码：

![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-0VM5mFF8-1578879474767)(byfn-for-windows/peer-cmds.png)\]](https://img-blog.csdnimg.cn/20200113094038310.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NoZWJhbzMzMzM=,size_16,color_FFFFFF,t_70)

## 3、使用byfn.win测试自己开发的链码

首先使用`up`子命令启动网络：

```
byfn up
```

然后启动链码应用，例如启动预置的nodejs链码：

```
cd chaincode_example02/node
npm install
node index.js --peer.address=peer0.org1.examplecom:7052 --peer.id.name=myccjs:0
```

现在进入管理终端，就可以进行链码的安装、激活、查询或交易操作了。

安装链码：

```
> peer chaincode install -n myccjs -v 0 -l node -p ..\chaincode_example02\node
```

激活链码：

```
> peer chaincode instantiate -n myccjs -c "{\"Args\":[\"init\",\"tom\",\"1000\",\"mary\":\"2000\"]}" -C mychannel -o orderer.example.com
```

查询链码状态：

```
> peer chaincode query -n myccjs -c "{\"Args\":[\"invoke\",\"tom\"]}" -C mychannel
```

提交链码交易：

```
> peer chaincode invoke -n myccjs -c "{\"Args\":[\"invoke\",\"tom\",\"mary\",\"100\"]}" -C mychannel -o orderer.example.com
```

注意：

1. 在激活链码之前，需要先启动链码
2. 可以随时修改链码或重新运行链码，不需要重新激活

## 4、使用byfn.win开发应用

在执行`reset`子命令时，会自动生成org1的连接配置文件：

- connection-org1.json
- connection-org1.yaml

Hyperledger Fabric官方提供的SDK可以直接使用上述连接配置文件，
可以根据自己的需要选择json或yaml格式。

---
byfn.win官方下载地址：[byfn for windows](http://sc.hubwiz.com/codebag/byfn-win/)
