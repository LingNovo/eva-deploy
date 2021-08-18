# eva poa 网络节点示例

## 1. bootnode 节点

使用`bootnode`程序构建，在网络中起数据转发，nat 网络穿透的作用。

### 1.1. bootnode1

- 服务器： `3.129.24.40`
- 端口： `30309`
- 节点地址： ` enode://69ff6cb5929fa6167220211d3695cc46d9138789f09aea2a29c6cd5d996df56570fa8497736b5104adf56aca13ae00b00f697524b4d34b13c331272839f3abd5@3.129.24.40:30309`

### 1.2. bootnode2

- 服务器：`18.117.71.13`
- 端口：`30309`
- 节点地址：`enode://6bf6f0452212ede0ee90d9592b131c876320ceb854421441bdf6f820a32eb51d42054f767a629118b380c203c2a78ac5a7f95978cf249040710de8a282a2505e@18.117.71.13:30309`

### 1.3. bootnode3

- 服务器：`3.138.116.207`
- 端口： `30309`
- 节点地址： `enode://4a9d6e92b314e867e8b291d0cd2e4412b44efcec610aad92524fe4bb6dd9849012d7eb37a961dba0848f708312fe5be4913229382df77645908d8e4a88664788@3.138.116.207:30309`

## 2. rpc 节点

使用`eva`程序构建，用于测试。

### 2.1. rpc node1

- 帐户地址： `ExC71bCF9dA81f42875470947b0e6d07a41278C84D`
- 服务器: `3.129.24.40`
- 端口： `30303`
- http端口： `8545`
- ws端口： `7777`
- 节点地址：`enode://5713969c6e3213318b2e690b3afd9a781ad5bfd9e2325dd8e644dba41181b539d01b049d6e5e8b9506c377d0fb872cd2ae1f8c6b2b346776f61c123e1e0c95ca@3.129.24.40:30303`

### 2.2. rpc node2

- 帐户地址：`Ex30Bbf8632fAf04e5b99c5d98ffD50104126dcf2B`
- 服务器： `18.117.71.13`
- 端口： `30303`
- http端口： `8545`
- ws端口： `7777`
- 节点地址： `enode://f480015255ab489da73b88b4cbb30a5aabcfcc762fcf6edbf78d316d5959ac3db7dd8fe5eda1fd749797cadde1971f5b25d68269ee801fb05810d4d350fa1a13@18.117.71.13:30303`

### 2.3. rpc node3

- 帐户地址：`ExfbBdb1feEd93390098334715e358f867277e044A`
- 服务器： `3.138.116.207`
- 端口： `30303`
- http端口： `8545`
- ws端口： `7777`
- 节点地址： `enode://7d21bcc402b24a5a233bc9d8de2962acf4335b03c7650d66bb840d065a301e29b9a94a670c2b19457d73797bc17960e2c545ccbb08f289d7d3fc30514005a34d@3.138.116.207:30303`

# 3. 本地构建 eva 节点示例

## 3.1. 编译

```bash
# 下载源码
git clone https://github.com/LingNovo/go-evanesco.git
# make
cd go-evanesco
make all
```

## 3.2. 准备部署

*注*：
- 需将路径中的`用户名`替换为自己PC系统的用户名。

```bash
cd $home/用户名/
# 创建部署工作目录
mkdir eva
# 复制编译好的程序至工作目录
cp -r go-evanesco/build/bin $home/用户名/eva/
# 创建节点目录
cd $home/用户名/eva/
mkdir node1
```

## 3.2. 初始化节点

```bash
cd $home/用户名/eva/bin/
# 创建帐户
./eva --datadir $home/用户名/eva/node1 account new
## 此处的回显信息中，`Ex....`为帐户地址，后续步骤要用，建议复制保存 
# 初始化节点
./eva --datadir $home/用户名/eva/node1 init evagenesis.json
```

## 3.3. 节点配置示例

```toml
[Node.P2P]
BootstrapNodes = [
"enode://69ff6cb5929fa6167220211d3695cc46d9138789f09aea2a29c6cd5d996df56570fa8497736b5104adf56aca13ae00b00f697524b4d34b13c331272839f3abd5@3.129.24.40:30309",
"enode://6bf6f0452212ede0ee90d9592b131c876320ceb854421441bdf6f820a32eb51d42054f767a629118b380c203c2a78ac5a7f95978cf249040710de8a282a2505e@18.117.71.13:30309",
"enode://4a9d6e92b314e867e8b291d0cd2e4412b44efcec610aad92524fe4bb6dd9849012d7eb37a961dba0848f708312fe5be4913229382df77645908d8e4a88664788@3.138.116.207:30309"
]
StaticNodes = [
"enode://5713969c6e3213318b2e690b3afd9a781ad5bfd9e2325dd8e644dba41181b539d01b049d6e5e8b9506c377d0fb872cd2ae1f8c6b2b346776f61c123e1e0c95ca@3.129.24.40:30303",
"enode://f480015255ab489da73b88b4cbb30a5aabcfcc762fcf6edbf78d316d5959ac3db7dd8fe5eda1fd749797cadde1971f5b25d68269ee801fb05810d4d350fa1a13@18.117.71.13:30303",
"enode://7d21bcc402b24a5a233bc9d8de2962acf4335b03c7650d66bb840d065a301e29b9a94a670c2b19457d73797bc17960e2c545ccbb08f289d7d3fc30514005a34d@3.138.116.207:30303"
]
TrustedNodes = []
```

# 4. 启动节点

复制本仓库里的`eva.toml `、`evagenesis.json` 文件至 `$home/用户名/eva/bin/`目录。

*注*：
- `--networkid 9527`
- `--unlock 'Ex...'`,`Ex...`为步骤#3.2创建的帐户地址。
- --password `password`，`password`为文件名，是步骤3.2创建帐户时输入的密码，将密码保存进名为`password`的文件。

```bash
cd $home/用户名/eva/bin/
# 启动节点
./eva --datadir $home/用户名/eva/node1  --config $home/用户名/eva/bin/eva.toml --port 30303 --networkid 9527 --http --http.addr 0.0.0.0 --http.port 8545 --http.corsdomain "*" --ws --ws.addr 0.0.0.0 --ws.port 7777 --ws.origins "*" --ws.api "eth,web3,net" --syncmode "full" --allow-insecure-unlock --unlock 'Ex...' --password `password` console
```