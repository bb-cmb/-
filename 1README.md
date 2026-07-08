# MessageBoard 留言板合约部署交互记录 v0.1

## 1. 合约基础信息
- 合约名称：MessageBoard
- 部署网络：Monad Testnet
- Solidity 版本：0.8.20
- 合约地址：`0xE10B2F8c6352345e851d89e1fCD1Be4796A8E607`
- 部署交易Hash：`0xc9630dcdbf949eac83cdd8376c170cda98d1fe5e813cf4ec7e276958b9cb8b10`
- Write交互交易Hash：`0x21fe0a5f7a6c735e3edcafe3996a57b34ae934920d59f7e639a4f90a2342dbc8`

## 2. 合约功能说明

### 合约源码：

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract MessageBoard {
    string public message;

    function write(string calldata _newMessage) external {
        message = _newMessage;
    }
}
```
极简入门合约，区分链上两种交互逻辑：
1. **Write 写入函数 write(string)**
   修改链上持久化存储的字符串，属于状态变更操作，**必须消耗Gas**，需要钱包签名发起交易，打包上链后数据永久留存。
2. **Read 读取函数 message()（自动生成）**
   view只读类型，不修改链上任何数据，**零Gas免费调用**，仅读取当前链存储内容，无需签名。

## 3. 完整部署步骤
### 3.1 编译
1. 打开 Remix IDE，新建 `MessageBoard.sol`
2. 粘贴合约源码，编译器锁定0.8.20及以上，完成编译无报错。

### 3.2 钱包网络配置
MetaMask 添加 Monad Testnet 测试网，导入课程专用学习钱包，领取测试MON代币用于支付Gas。

### 3.3 部署上链
1. Remix 部署环境选择 Browser Extension(MetaMask)
2. 选中 MessageBoard 合约，点击 Deploy，确认钱包交易
3. 等待区块确认，复制合约地址与部署tx hash归档保存。
### 合约成功部署
<img width="1917" height="1052" alt="1cc7251e59b80e33bb6f546c04bd84cd" src="https://github.com/user-attachments/assets/c87b6c7e-082e-4de8-b50a-8856e7615b74" />

<img width="896" height="655" alt="2bc5471ad5a38c0b0ca637fee2694856" src="https://github.com/user-attachments/assets/842f7751-5d71-487d-a098-c95d31937055" />


## 4. 合约交互操作流程
## 第一次Read(后面部分应为空)

<img width="1912" height="970" alt="7c47e1d77c23a4f6b9d642aad4964295" src="https://github.com/user-attachments/assets/1894d8d4-f573-417a-9745-6d16be8d464d" />

### 4.1 Write 写操作
1. 展开已部署合约，找到 `write(string)` 输入框
2. 输入文本 `"完成今日web3的学习"`(注意英文标点)
3. 点击 Transact，MetaMask签名确认交易
4. 交易打包完成，链上数据完成更新，记录交互tx hash。
### Write:合约交易记录
<img width="1803" height="942" alt="3e5835c5f4ce73ea94b8d762cfac7acd" src="https://github.com/user-attachments/assets/6d8144c8-ae29-4e66-8fda-80188970b70f" />

### Write:交易打包完成
<img width="1878" height="997" alt="eb5bd5ea2f77e2471d4d1a08fd60fc11" src="https://github.com/user-attachments/assets/110372fb-2b38-487f-89fc-ce860915799a" />

### 4.2 Read 读验证
1. 点击合约内置 `message` 读取按钮
2. 点击 Call 发起只读调用，无Gas消耗
3. 返回字符串与写入内容完全一致，验证读写链路正常。
### Read验证
<img width="1882" height="996" alt="c94ae9945c9215f22076dc607ca8990f" src="https://github.com/user-attachments/assets/50a6a396-1d26-4f9a-a4d7-914748ca89b5" />

## 5. 区块浏览器校验
访问 Monad Testnet 浏览器，输入合约地址可查看：
- 合约创建时间、创建钱包地址
- 所有历史写入交易记录
- 合约基础信息与链上状态


## 6. 核心学习总结
1. 链上操作分两类：**写操作(耗Gas，存数据)** / **读操作(零Gas，查数据)**
2. 完整流程闭环：代码编译 → 钱包部署上链 → 发起写交易修改存储 → 只读调用验证结果 → 浏览器永久溯源
3. public 状态变量会自动生成免费读取getter函数，简化合约读取逻辑。
