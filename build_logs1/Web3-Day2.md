# Web3 Day2｜最小留言板Solidity合约生成、审计、部署交互完整记录
## （一）AI生成Solidity合约 & 人工代码审计
### 1. 本次使用的Prompt
```
你是一位精通 Solidity 的智能合约专家，擅长编写极简、安全的代码用于教学演示。
任务目标：请为我编写一个最小的、可运行的 Solidity 留言板合约。
具体要求：
版本：使用 pragma solidity ^0.8.20;
核心功能：
1. 提供一个 write 函数：允许任何人传入一个字符串（留言内容），并将其存储在链上。不需要检查重复，不需要存入数组，只需要覆盖存储即可（保持最简单）。
2. 提供一个 read 函数（或者 public 变量）：允许任何人读取当前存储的这条留言。
输出完整可编译代码，并简单解释每一段合约结构。
```

### 2. AI生成完整输出内容
#### 2.1 AI给出合约源码初稿
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract MessageBoard {
    string public message;

    constructor(string memory _initialMessage) {
        message = _initialMessage;
    }

    function write(string calldata _newMessage) external {
        message = _newMessage;
    }
}
```
#### 2.2 AI对合约结构的解释
1. `SPDX-License-Identifier: MIT`：开源许可证，Remix编译强制要求，避免编译警告。
2. `pragma solidity ^0.8.20;`：指定编译器版本，^代表兼容0.8.20及以上同大版本。
3. `contract MessageBoard`：合约主体，命名为留言板。
4. `string public message;` 链上状态变量，自动生成只读getter，等价read读取函数。
5. `constructor` 部署构造函数，部署时可以传入初始留言。
6. `write()` 外部写入函数，calldata节省gas，覆盖更新链上留言字符串。

### 3. 最终定稿合约源码（人工校验后无修改，可直接编译部署）
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

/**
 * @title MessageBoard 极简链上留言板合约
 * @dev 单字符串存储，仅覆盖更新，区分读写链上操作，入门教学合约
 */
contract MessageBoard {
    // 链上持久存储留言，public自动生成只读读取接口
    string public message;

    /**
     * @dev 部署构造函数，部署时初始化第一条留言
     * @param _initialMessage 初始留言文本
     */
    constructor(string memory _initialMessage) {
        message = _initialMessage;
    }

    /**
     * @dev 写入留言函数，修改链上存储，消耗Gas
     * @param _newMessage 待覆盖写入的新留言内容
     */
    function write(string calldata _newMessage) external {
        message = _newMessage;
    }
}
```

### 4. 人工修改与判断说明
1. **无功能性代码修改**：AI生成代码完全满足需求，可直接编译、部署、交互。
2. **仅优化补充注释**：给合约、构造函数、write函数增加标准化NatSpec注释，方便新手读懂每一段逻辑，不改变合约执行逻辑。
3. **功能判定**：合约完全符合最小留言板需求，无多余复杂逻辑，无权限漏洞，无安全隐患。

### 5. 3条必须人工检查的AI生成代码关键点
1. **编译器版本与许可证校验**
AI容易漏写`SPDX-License-Identifier`或者版本号写错，会导致Remix编译报错；本次代码包含MIT许可证、`^0.8.20`版本，编译无警告，人工确认通过。
2. **存储读写逻辑与Gas优化校验**
字符串参数使用`calldata`而非`memory`，能降低交互Gas消耗；public变量自动生成read读取接口，无需额外手写读取函数，逻辑极简无冗余，人工确认符合最小化要求。
3. **权限与安全风险校验**
合约无转账、无资产操作，不存在重入、溢出、权限管控漏洞；任何人都可以读写留言是需求规定，无越权风险，无潜在攻击点，人工确认安全。

## （二）合约部署至Monad Testnet + 完整读写交互链路
### 1. 核心交易信息
1. 合约地址：`0xE10B2F8c6352345e851d89e1fCD1Be4796A8E607`
2. 部署Transaction Hash：`0xc9630dcdbf949eac83cdd8376c170cda98d1fe5e813cf4ec7e276958b9cb8b10`
3. Write写入交互Transaction Hash：`0x21fe0a5f7a6c735e3edcafe3996a57b34ae934920d59f7e639a4f90a2342dbc8`

### 2. 完整部署&交互操作流程
#### 2.1 编译合约（Remix IDE）
1. 打开Remix，新建`MessageBoard.sol`粘贴定稿合约代码；
2. 编译器版本切换0.8.20，点击Compile，无报错编译完成。

<div align="center">
<img src="../assets/images/remix-code-ai-generate.png" width="1800">
<p>AI生成合约代码与Remix编译界面</p>
</div>

#### 2.2 连接课程专用钱包部署
1. MetaMask切换Monad Testnet，导入课程钱包地址：`0xD1A61BA21437533401F300FCC122EF263E93dEa8`；
2. Remix部署环境选择`Browser Extension - MetaMask`；
3. 输入初始留言，点击Deploy，钱包确认部署交易，等待区块确认。

<div align="center">
<img src="../assets/images/remix-deploy-page.png" width="1700">
<p>Remix部署合约界面，部署交易确认成功</p>
</div>

<div align="center">
<img src="../assets/images/deploy-tx-detail.png" width="1300">
<p>部署交易区块浏览器详情</p>
</div>

#### 2.3 Write写操作交互（消耗Gas）
1. 展开已部署合约，在write输入框填写内容：`完成今日web3的学习`；
2. 点击Transact发起上链写入交易，等待打包确认。

<div align="center">
<img src="../assets/images/write-function-ui.png" width="1800">
<p>write函数写入留言操作界面</p>
</div>

<div align="center">
<img src="../assets/images/write-tx-explorer.png" width="1800">
<p>区块浏览器合约页面，展示Write交互记录</p>
</div>

#### 2.4 Read读操作交互（零Gas免费读取）
点击合约自带`message`读取按钮，点击Call，直接返回链上存储的留言文本，验证写入成功。

<div align="center">
<img src="../assets/images/read-function-result.png" width="1800">
<p>read读取留言返回结果界面</p>
</div>

#### 2.5 区块浏览器完整验证
将合约地址输入MonadVision浏览器，可查询合约创建地址、部署时间、全部读写交互交易，完整溯源整条链上操作链路。

### 3. 合约功能、部署交互说明（README v0.1内容摘要）
本合约为极简教学留言板，分为两类链上交互：
1. **Write写操作**：修改链上字符串存储，属于状态变更，需要消耗Gas，钱包签名后上链永久留存；
2. **Read读操作**：public变量自动生成只读接口，无Gas消耗，仅读取链上现有数据。
完整链路闭环：AI生成合约代码 → Remix编译校验 → MetaMask连接测试网部署 → 发起Write写入交易 → Read读取验证数据 → 区块浏览器校验所有链上记录。

### 4. 配套文档链接
- AI合约审计任务文档：https://github.com/bb-cmb/-/blob/e6513b867b073c91788bc8364f780e772e633479/README.md
- 合约部署交互完整README：https://github.com/bb-cmb/-/blob/e8b614bb57de5f5a441c114146cc313ddc4282eb/1README.md
