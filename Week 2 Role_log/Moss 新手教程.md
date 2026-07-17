# Moss 新人完整入门教程：环境搭建、运行Demo与开源贡献全流程
## 一、教程前言
本教程面向零基础Web3 Builder，完整覆盖Moss本地环境配置、内置Demo运行、MCP客户端接入、新手文档类开源贡献全流程，全程无需私钥、真实资金，降低上手门槛，配套仓库官方规范，可直接复刻操作。
> 风险提示：Moss为Alpha未审计软件，禁止用于真实资产生产环境

## 二、前置环境准备
### 硬件与系统要求
Windows / Mac / Linux 均可，内存 ≥4G
### 软件版本硬性要求
1. Node.js ≥ 22
2. pnpm ≥ 11

#### 环境安装步骤
1. 下载Node 22长期支持版：官网安装，终端校验版本
```bash
node -v
```
2. 全局安装pnpm
```bash
npm install -g pnpm
pnpm -v
```

## 三、拉取源码并构建项目
1. 克隆Moss官方仓库
```bash
git clone https://github.com/nishuzumi/moss
cd moss
```
2. 安装全部依赖
```bash
pnpm install
```
3. 全局构建多包项目（必须执行，否则示例无法运行）
```bash
pnpm build
```
4. 离线测试校验环境是否正常
```bash
pnpm test:offline
```
无报错即代表环境配置完成。

## 四、运行官方内置Demo（无需私钥/余额）
Moss仅做交易模拟，不需要任何钱包私钥，可直接运行两个标准示例：
### Demo1：WMON 包装/解包装模拟
```bash
pnpm --filter @themoss/example-simple-flow wrap
```
执行后会完整走通标准流程 `discover → load → action → simulate`，输出Change变更记录与Receipt校验回执。

### Demo2：Kuru DEX MON兑换USDC模拟
```bash
pnpm --filter @themoss/example-simple-flow swap
```
可查看DEX报价、滑点设置、交易模拟校验全链路输出。

## 五、拓展：MCP Server 对接本地AI客户端
构建完成后，可启动Moss MCP服务，让本地AI拥有Monad链交互能力：
1. 获取本地moss路径，复制cli.js完整路径
2. 在MCP客户端配置文件写入：
```jsonc
{
  "mcpServers": {
    "moss": {
      "command": "node",
      "args": ["你的本地moss路径/packages/mcp-server/dist/cli.js"],
      "env": { "MOSS_RPC_URL": "https://rpc.monad.xyz" }
    }
  }
}
```
3. 重启AI客户端，即可调用`discover/load/action/simulate`四大工具。

## 六、新人低门槛开源贡献实操（落地#77 Issue）
### 1. 可选新手贡献方向（无代码门槛）
- 搭建`docs/faq-zh.md`中文新手问答文档（#77需求）
- 补充Windows系统专属部署避坑指南
- 给示例代码增加中文注释、运行截图
- 完善中文入门文档缺失操作说明

### 2. 标准PR提交完整流程
1. Fork官方仓库至个人GitHub账号
2. 克隆个人Fork仓库，新建独立开发分支
```bash
git checkout -b docs/add-chinese-faq
```
3. 修改docs目录文档，完成内容编写
4. 本地校验代码规范
```bash
pnpm lint
pnpm typecheck
```
5. 提交代码、推送至个人分支
```bash
git add .
git commit -m "docs: add faq-zh.md for chinese newcomers #77"
git push origin docs/add-chinese-faq
```
6. 打开官方仓库，依照项目PULL_REQUEST_TEMPLATE模板提交PR
7. 在#77 Issue下留言同步，等待维护者Review迭代

## 七、配套学习文档索引
仓库内置中文学习资料，修改/查阅均可参考：
1. `docs/getting-started.zh-CN.md` 新手上路文档
2. `docs/mcp-tools.md` MCP工具输入输出契约
3. `docs/protocol-onboarding.md` 新协议接入指南
4. `CONTRIBUTING.md` 开源贡献规范
5. `SECURITY.md` 项目安全约束说明

## 八、新人高频FAQ（配套#77文档建设）(举例)
1. Q：运行报错、命令找不到？
A：必须先执行`pnpm build`完成项目构建，Node、pnpm版本不达标也会触发报错。
2. Q：是否需要导入钱包私钥？
A：完全不需要，Moss仅模拟未签名交易，签名操作交由本地钱包独立完成。
3. Q：Moss支持哪些区块链？
A：当前仅支持Monad主网，chain ID=143。
4. Q：模拟器告警代表什么？
A：代表交易存在风险、状态变更异常，按照规则必须停止，禁止签名。
5. Q：如何新增自定义协议？
A：使用`packages/protocols/_template`模板包，参照协议接入文档开发。

---
### 教程简要说明
本教程为Moss零基础新人指南，分步讲解环境安装、源码构建、官方Demo运行、MCP客户端接入，同时配套低门槛文档类开源贡献实操流程，附带高频问题FAQ，帮助新手快速上手使用并参与Moss开源共建。
