# GitHub Exploration Log
## 参考开源项目
1. Hardhat：https://github.com/NomicFoundation/hardhat
2. Argot Solidity：https://github.com/argotorg/solidity
3. Moss：https://github.com/nishuzumi/moss

## 一、通用项目目录结构（三个项目共性）
1. **仓库根目录**
- `README.md`：项目简介、快速安装、基础使用教程
- `LICENSE`、`CONTRIBUTING.md`：开源协议、外部开发者贡献规范
- `SECURITY.md`：漏洞上报渠道、安全风险边界说明
2. **`.github` 文件夹**
- `workflows`：CI/CD自动化脚本，自动执行构建、代码校验、单元测试
- `ISSUE_TEMPLATE`：固定Bug反馈、功能需求提交模板
- `PULL_REQUEST_TEMPLATE`：PR提交校验清单、代码修改规范
3. `/docs`
存放完整官方教程、API说明、架构设计、协议接入文档
4. **源码目录**
Hardhat、Moss采用monorepo多包分包管理；Solidity按编译器职能分层，划分语法解析、ABI生成等底层模块
5. `/examples`
可直接运行的最小Demo，降低新手入门成本

## 二、GitHub各核心模块作用
1. README：项目首页入口，快速了解项目定位与基础操作
2. Docs：系统化完整文档，解决深度开发、定制化需求问题
3. Issues：用户提交Bug、新增功能诉求，维护者跟进排期讨论
4. Pull Requests：开发者提交代码改动，维护者审核、自动化测试通过后合并入库
5. Discussions：非代码类交流板块，用于技术答疑、生态方案探讨

## 三、感兴趣的 Issue / PR
### 我所感兴趣的是Moss
### 主题：新增 Kuru DEX 协议接入PR
1. 内容：开发者按照仓库统一标准封装DEX交互能力，补充交易模拟校验逻辑、交易回执解析规则
2. 约束规范：新增协议必须复用项目内置模拟器校验流程，禁止跳过前置交易模拟，规避AI Agent误操作资产风险
3. 审核标准：自动化测试全部通过、同步补充配套文档、不存在权限越权漏洞

## 四、我的发现
1. 三款Web3工具类项目标准化程度很高，`.github`自动化流程统一，强制代码检查与测试，过滤低质量代码；
2. 统一区分Issues（代码问题）与Discussions（技术闲聊），仓库讨论分区清晰，便于维护管理；
3. 安全为通用核心约束：编译器、部署工具、AI链上交互框架均单独设立安全说明，严格管控高危链上操作；
4. 新增功能有完整落地要求，必须同步补充示例、文档、单元测试，保障项目长期可维护。

## 五、学习收获
1. 能够快速梳理开源仓库分层结构，精准定位文档、实操示例、自动化配置文件；
2. 理解维护者依靠模板、CI流程、贡献规范，降低大型开源项目管理成本；
3. 学会通过Issues、PR跟踪项目功能迭代，借鉴行业标准化开发思路；
4. 掌握Web3开源项目通用管理逻辑：自动化把控代码质量、优先保障链上资产安全、配套完整新手落地材料。
