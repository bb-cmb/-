# Web3 Day1｜课程钱包配置 + 首笔链上转账完整记录 v0.1
## 一、任务1：课程专用钱包与 Monad Testnet 环境搭建
### 1. 基础信息
- 钱包工具：MetaMask
- 课程专用钱包地址：`0xD1A61BA21437533401F300FCC122EF263E93dEa8`
- Monad Testnet 配置状态：添加完成，可正常切换网络、领取测试代币、发起链上交易

### 2. Monad Testnet 网络配置流程
1. 新建独立 MetaMask 钱包作为学习专用，不混用持有真实资产的主力钱包，隔离测试操作与自有资产，养成安全钱包使用习惯。
2. 通过 Monad 官方页面导入完整网络参数：
    - 网络名称：Monad Testnet
    - RPC URL：`testnet-rpc.monad.xyz`
    - 链ID：10143
    - 代币符号：MON
    - 区块浏览器：`testnet.monadexplorer.com`
3. 配置完成后切换至测试网，成功领取测试MON用于支付Gas手续费。

<div align="center">
<img width="432" height="757" alt="e4b3fa339f6d0fea48089a3dfb7cbc93" src="https://github.com/user-attachments/assets/93af8381-8799-48a8-8b93-7d0f1bcbf1e6" />
<p>MetaMask Monad Testnet 网络配置截图</p>
</div>


<div align="center">    
<img width="472" height="922" alt="ccd973e32e4a3b518603c83e6d317a0f" src="https://github.com/user-attachments/assets/23a8751d-5573-455f-8233-58b345676667" />
<p>钱包主页：已切换Monad Testnet，持有59.554枚测试MON</p>
</div>

### 3. 区块浏览器地址查询验证
打开MonadVision区块浏览器首页，在搜索框输入课程钱包地址，可完整查看钱包余额、全部历史交易，链上数据与钱包资产完全同步，验证浏览器可正常检索地址信息。

<div align="center">
<img width="1915" height="960" alt="bc42eca3f8b2192b82303b65c66a238a" src="https://github.com/user-attachments/assets/8d0d8aba-488f-4e88-b6da-5e31b72edd86" />
<p>Monad Testnet 区块浏览器首页</p>
</div>


<div align="center">
<img width="1907" height="970" alt="4f4d89189b0119504e9b49446d6c6506" src="https://github.com/user-attachments/assets/2a25d633-2c77-4c81-89d2-6814c6de5297" />
<p>区块浏览器查询课程钱包地址页面</p>
</div>


<div align="center">
<img width="1516" height="905" alt="1de2c57bac3eb9584a59604bc17c7095" src="https://github.com/user-attachments/assets/5ab991ad-0304-4787-8c8e-4baf92663cc4" />
<p>在水龙头取MON</p>
</div>

### 4. 链上产品与普通互联网产品区别
二者核心差异是数据存储与信任逻辑。普通互联网数据存储在企业中心化服务器，平台可随意修改、删除用户数据，交易记录不对外公开；链上资产、合约等核心数据同步上链，全网公开可查、难以篡改，依靠智能合约自动执行规则。页面、图片等普通内容仍存中心化服务器；传统平台由运营制定规则，链上合约部署后规则无法随意修改，可依托合约拓展全新商业模式。

---

## 二、任务2：完成首笔 Monad Testnet 链上转账交易
### 1. 交易基础信息
- Transaction Hash：`0xc15c66ed390a1a1130398d897b8742f6ff96ac23a4d1caa03e1707b26e5518b9`
- 区块浏览器交易详情链接：https://testnet.monadvision.com/tx/0xc15c66ed390a1a1130398d897b8742f6ff96ac23a4d1caa03e1707b26e5518b9

### 2. 完整交易操作流程
1. 访问Monad水龙头领取测试MON，获取交易所需手续费资产；
2. 进入MonadVision MySpace转账页面，发起自转账，向自身钱包地址转账1枚MON；
3. MetaMask弹窗确认交易，等待区块打包，页面弹出交易成功提示；
4. 复制交易哈希，在区块浏览器打开详情页核验全部链上信息。

<div align="center">
<img width="1918" height="1148" alt="ee6a9a3fb03e9a90869faae9babf85bf" src="https://github.com/user-attachments/assets/68ccc53b-103e-4e9f-9143-18e5c07c3164" />
<p>发起1MON自转账确认弹窗</p>
</div>


<div align="center">
<img width="1912" height="1075" alt="9b8640aa473f2a59e8ed40badb36d7d3" src="https://github.com/user-attachments/assets/201ae0ff-3cfe-4f57-a5a5-f58a79e03deb" />
<p>交易上链成功提示页面</p>
</div>


<div align="center">
<img width="1447" height="1018" alt="2628e37964b4ad64d7b0549d7182fccb" src="https://github.com/user-attachments/assets/732900ce-ebd6-40d8-b549-58181da1d924" />
<p>区块浏览器完整交易详情页面</p>
</div>


### 3. 交易内容详细解读
1. **From / To**：发送方、接收方均为本人;
2. 课程钱包地址 `0xD1A61BA21437533401F300FCC122EF263E93dEa8`，本次为钱包自转账操作；
3. **Value**：转账金额为 1 MON，代表本次转移的代币数量；
4. **Gas 相关说明**：Gas Price为102 Gwei，本次总Gas Fee 0.002142 MON。Gas是链上计算资源单位，所有修改链上存储的操作都需要消耗Gas作为节点手续费；即便交易失败，节点已执行计算，Gas手续费仍会扣除；
5. **交易状态**：`Success` 代表交易成功，交易被打包进区块#42809637，生成永久不可篡改的链上记录；
6. 字段释义：Transaction Hash(0xc15c66ed390a1a1130398d897b8742f6ff96ac23a4d1caa03e1707b26e5518b9)是交易唯一标识，等同于线下小票编号，可随时溯源整笔交易全部信息。

### 4. 学习总结
本次完整走完「领取测试代币 → 钱包发起转账 → 区块浏览器核验交易」基础链上流程，弄懂转账核心字段含义，理解Gas手续费、去中心化公开账本、智能合约底层基础逻辑，完成Web3入门的第一步实操。
