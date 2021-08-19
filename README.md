# eva poa 网络节点示例

## 1. bootnode 节点

使用`bootnode`程序构建，在网络中起数据转发，nat 网络穿透的作用。

### 1.1. bootnode1

- 服务器： `3.129.24.40`
- 端口： `30309`
- 节点地址： ` enode://39553b67cd5e1cc15cf1cc3c5cbbdac9203b45e168b9577e443f74fc192534a949b89489c6662e0054b99648f48736ef372e1a1aa8260f524529e53133512e13@3.129.24.40:30309`

### 1.2. bootnode2

- 服务器：`18.117.71.13`
- 端口：`30309`
- 节点地址：`enode://debe675bdc1bad97a13d8dd4289fe68d0322493cb18134ff60720642a3205629f61702121766ba21a54bd57fa55b0c81fe98ff208ad21c3116e1e38bd98110f2@18.117.71.13:30309`

### 1.3. bootnode3

- 服务器：`3.138.116.207`
- 端口： `30309`
- 节点地址： `enode://48ac70d8dded7922d251804ebb237dff1953805c340bf2352f3436f63debc3cc261a7fe778b4cce7ee0450f7eff6b2cae2814505c05f610a374998cc2ca728ef@3.138.116.207:30309`

## 2. rpc 节点

使用`eva`程序构建，用于测试。

### 2.1. rpc node1

- 帐户地址： `Ex34d6e4A18871c48C0CC1FdFAf7b0c573733de8F1`
- 服务器: `3.129.24.40`
- 端口： `30303`
- http端口： `8545`
- ws端口： `7777`
- 节点地址：`enode://3739f530e91f5b2f7f1c77a282786e8207cacfcf6aeb05dfbab81e4e6fb7752c161cbc1b60cb6e2af2fc1ff52db5abf7bc365863a64ae9cd4a1ca05cfbdbbd54@3.129.24.40:30303`

### 2.2. rpc node2

- 帐户地址：`ExCcdA7ffCA1de169E05422Ffa960a3B5763C734d3`
- 服务器： `18.117.71.13`
- 端口： `30303`
- http端口： `8545`
- ws端口： `7777`
- 节点地址： `enode://d5f3acd84ea725c8465c94abc6e9ca3c3f0d80f548b79a4c512db50b125521e73567e7e28c5255e5da27a1ca4eeb1b7820033b8ec944877b292f6b307ab16a64@18.117.71.13:30303`

### 2.3. rpc node3

- 帐户地址：`Exc20F647e0B173BBb2A6E52dd05ca2Ac9f0c75fDd`
- 服务器： `3.138.116.207`
- 端口： `30303`
- http端口： `8545`
- ws端口： `7777`
- 节点地址： `enode://e732757dd8d2a8ef0fb2b4d8b448164a1a43d0df4842963312b39e8836d95210f3a8fea9dea095545beb1761c1490e69688022ef48e3702790c760648005a2c4@3.138.116.207:30303`

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
"enode://39553b67cd5e1cc15cf1cc3c5cbbdac9203b45e168b9577e443f74fc192534a949b89489c6662e0054b99648f48736ef372e1a1aa8260f524529e53133512e13@172.31.2.142:30309",
"enode://debe675bdc1bad97a13d8dd4289fe68d0322493cb18134ff60720642a3205629f61702121766ba21a54bd57fa55b0c81fe98ff208ad21c3116e1e38bd98110f2@172.31.8.193:30309",
"enode://48ac70d8dded7922d251804ebb237dff1953805c340bf2352f3436f63debc3cc261a7fe778b4cce7ee0450f7eff6b2cae2814505c05f610a374998cc2ca728ef@172.31.14.84:30309"
]
StaticNodes = [
"enode://3739f530e91f5b2f7f1c77a282786e8207cacfcf6aeb05dfbab81e4e6fb7752c161cbc1b60cb6e2af2fc1ff52db5abf7bc365863a64ae9cd4a1ca05cfbdbbd54@3.129.24.40:30303",
"enode://d5f3acd84ea725c8465c94abc6e9ca3c3f0d80f548b79a4c512db50b125521e73567e7e28c5255e5da27a1ca4eeb1b7820033b8ec944877b292f6b307ab16a64@18.117.71.13:30303",
"enode://e732757dd8d2a8ef0fb2b4d8b448164a1a43d0df4842963312b39e8836d95210f3a8fea9dea095545beb1761c1490e69688022ef48e3702790c760648005a2c4@3.138.116.207:30303"
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