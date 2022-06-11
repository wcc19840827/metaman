## 1. 部署万纳链 Venachain

- Github repo: https://github.com/Venachain/Venachain
- 开发文档: https://venachain-docs.readthedocs.io/zh/latest/
- 部署文档: https://venachain-docs.readthedocs.io/zh/latest/documents/quick/deploy.html

### 1.1 releases包部署

```bash
wget https://github.com/Venachain/Venachain/releases/download/v1.0.1/Venachain_linux_amd64_v1.0.1.tar.gz
tar -zxvf Venachain_linux_amd64_v1.0.1.tar.gz
```

### 1.2 容器内部署单节点

```bash
#新建容器
docker run -it -v ~/install/tmp/:/opt -p 6791:6791 --name venachain ubuntu:20.04
apt update
apt install curl

	#二次进入容器
docker container start venachain
docker exec -it venachain bash
 
cd /opt/linux
export WORKSPACE=./
cd ${WORKSPACE}/scripts/

# 首次部署并启动节点
./venachainctl.sh one
	# 二次启动节点
./venachainctl.sh start -n 0

# 查看节点状态
./venachainctl.sh status -n 0

# 停止
./venachainctl.sh stop -n 0
# 停止清数据
./venachainctl.sh clear -a
```

### 1.3 与链交互

```bash
cd ${WORKSPACE}/scripts/
./venachainctl.sh console -n 0

eth.accounts
eth.blockNumber
#测试一笔交易
eth.sendTransaction({from:eth.accounts[0],to:eth.accounts[0]})
#查看交易回执
eth.getTransactionReceipt("0xcb1d67354698038e23fe736fd0b6cdd51dd4c7bb3927fdc4fd1774aab06b4040")
#查看交易池状态
txpool.status

#解锁 (默认密码 0)
personal.unlockAccount(eth.accounts[0])
personal.unlockAccount(eth.accounts[0], "0")

```

## 2. 部署NFT合约 MetaMan

注意: 部署前先解锁本地的钱包, 通过命令 `personal.unlockAccount(eth.accounts[0], "0")`

### 2.1 在remix中编译合约并部署

![image-20220611234937481](https://s2.loli.net/2022/06/11/jt4uRylZMTgFwXJ.png)

![image-20220611235015699](https://s2.loli.net/2022/06/11/M1dLcbv8f5rwPXR.png)

![image-20220611235102450](https://s2.loli.net/2022/06/11/qVh5kEvbUxoHfJn.png)

![image-20220611235127861](https://s2.loli.net/2022/06/11/V8GCQJ5e6bgRDKP.png)

![image-20220611235232526](https://s2.loli.net/2022/06/11/1bB3sTClLrZUh5F.png)

![image-20220611235254066](https://s2.loli.net/2022/06/11/CsqHztBVMFbS8lD.png)

### 2.2 部署成功

![image-20220611235721502](https://s2.loli.net/2022/06/12/2FM6TvAKizZOl85.png)

### 2.3 在命令行中查看

![image-20220611235855700](https://s2.loli.net/2022/06/12/mklDH3TxwvCWBg1.png)

## 3. 铸造一个数字人 NFT

